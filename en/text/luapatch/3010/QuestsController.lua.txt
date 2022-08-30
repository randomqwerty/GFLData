local util = require 'xlua.util'
xlua.private_accessible(CS.QuestsController)
xlua.private_accessible(CS.DailyWeeklyQuestData)
xlua.private_accessible(CS.DailyQuestOverallInfo)
xlua.private_accessible(CS.WeeklyQuestOverallInfo)
xlua.private_accessible(CS.DailyQuestInfo)
xlua.private_accessible(CS.WeekQuestInfo)


local _RefreshRedPoint = function(self)
	self:RefreshRedPoint(); 
	if self.currentQuestType ~= "Daily" and self.goDailyNew.activeSelf then
		local hasMail=false;
		for i=0,CS.GameData.listMail.Count-1 do
			local mail = CS.GameData.listMail:GetDataByIndex(i);
			if mail.type == CS.MailType.dailyQuest or mail.type == CS.MailType.WeeklyQuest then
				hasMail=true;
			end
		end
		if hasMail==false then
			--print("has no mail");
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

				--print("has no daily");
				local week_count = CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo.WeekArr.Length;
				
 				for i=0,week_count-1 do
					local w_id = CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo.WeekArr[i];
					local w_info = CS.GameData.listWeeklyQuestInfo:GetDataById(w_id)
					if w_info ~= nil and w_info.IsAccomplished==true then
						
						if CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo:CheckQuestAccomplish(w_id)==false then
							if CS.DailyWeeklyQuestData.Instance.weeklyQuestAllInfo:IsLockQuest(w_id) and CS.DailyWeekQuestCtrl.Instance.hasOpenPassOrder==false then
								--print("lock");
							else	
								hasQuest=true;
							end
						end
					end
				end
				if hasQuest==false then
					--print("has no week");
					self.goDailyNew:SetActive(false);
				else
					--print("has week");
				end
			end
		end	 
	end
end
util.hotfix_ex(CS.QuestsController,'RefreshRedPoint',_RefreshRedPoint) 

