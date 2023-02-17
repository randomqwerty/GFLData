local util = require 'xlua.util'
xlua.private_accessible(CS.Badge)
xlua.private_accessible(CS.DailyWeeklyQuestData)
xlua.private_accessible(CS.DailyQuestOverallInfo)
xlua.private_accessible(CS.WeeklyQuestOverallInfo)
xlua.private_accessible(CS.DailyQuestInfo)
xlua.private_accessible(CS.WeekQuestInfo)

local _UpdateBadge = function(self)
	self:UpdateBadge(); 
	if self.isActive and self.type==CS.Badge.BadgeType.ExistsNewQuest then
		local hasMail=CS.DailyWeeklyQuestData.ExistQuestPrize();
		if hasMail==false then
			print("badge has no mail");
 			local hasQuest=false;
 			local daily_count = CS.DailyWeeklyQuestData.Instance.dailyQuestAllInfo.DailyArr.Length

 			for i=0,daily_count-1 do
				local d_id = CS.DailyWeeklyQuestData.Instance.dailyQuestAllInfo.DailyArr[i];
				local d_info = CS.GameData.listDailyQuestInfo:GetDataById(d_id)
				if d_info ~= nil and d_info.IsAccomplished==true then

					if CS.DailyWeeklyQuestData.Instance.dailyQuestAllInfo:CheckQuestAccomplish(d_id)==false then
						hasQuest=true;
					end 
				end
			end
			if hasQuest==false then

				--print("badge has no daily");
				local week_count = CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo.WeekArr.Length;
				

				local pass = CS.PassOrderUserData.Instance:HasActivePassOrder();
				local hasOpenPassOrder =false;
				if pass~=nil and CS.PassOrderUserData.Instance:UnlockLevel(pass.id) ~= CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeNone then
					hasOpenPassOrder=true;
				end
				-- if hasOpenPassOrder then
				-- print("has open pass");	
				-- else
				-- print("not open pass");	
				-- end
 				for i=0,week_count-1 do
					local w_id = CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo.WeekArr[i];
					local w_info = CS.GameData.listWeeklyQuestInfo:GetDataById(w_id)
					if w_info ~= nil and w_info.IsAccomplished==true then
						
						if CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo:CheckQuestAccomplish(w_id)==false then
							if CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo:IsLockQuest(w_id) and hasOpenPassOrder==false then
								--print("badge week lock");
							else	
								hasQuest=true;
							end
						end
					end
				end
				if hasQuest==false then
					--print("badge has no week");
					self.GoBadge:SetActive(false);
        			self.isActive = false; 
				--else
					--print("badge has week");
				end
			end
		end	 
	end
end 
util.hotfix_ex(CS.Badge,'UpdateBadge',_UpdateBadge) 
