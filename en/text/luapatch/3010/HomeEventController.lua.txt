local util = require 'xlua.util'
xlua.private_accessible(CS.HomeEventController) 
xlua.private_accessible(CS.HomeEventListItemController)
xlua.private_accessible(CS.OPSEventPrizeData)
 
local _CheckTimeLimitRedPoint = function(self)
	self:CheckTimeLimitRedPoint(); 
	
	local existRed = CS.HomeEventData.ExistDrawEventsPrize();
	if existRed == false then
		local count =self.listTimiLimitLeftLabals.Count;
		for i=0,count-1 do 
			if self.listTimiLimitLeftLabals[i].newType==CS.HomeAnnouncementEventType.draw then
				self.listTimiLimitLeftLabals[i]:ShowTips(false);
			end
		end
	end
end
local _ExistPointExchangePrize = function()

	if CS.HomeEventData.CheckExistEventPrizeExchange() then

		local count =CS.GameData.eventPrizeData.Count;
		if count==0 then
			return false;
		else 
			local existDraw = false;
			for i=0,count-1 do  
				local prize = CS.GameData.eventPrizeData[i];
				

				local ids = CS.System.Collections.Generic.List(CS.System.Int32)(prize.prizeLevelInfo.num_prizeId.Keys);
				local p_count = ids.Count;

				if prize.hasGet.Count < p_count then
					for j=0,p_count-1 do
						if prize.hasGet:Contains(j)==false and prize.Num >= ids[j] then
							existDraw=true;
						end
					end
				end
				ids=nil;
				prize=nil;
			end
			return existDraw;
		end 
	else 
		return false;
	end 
end
util.hotfix_ex(CS.HomeEventController,'CheckTimeLimitRedPoint',_CheckTimeLimitRedPoint)
util.hotfix_ex(CS.HomeEventData,'ExistPointExchangePrize',_ExistPointExchangePrize)


