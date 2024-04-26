local util = require 'xlua.util'
xlua.private_accessible(CS.OPSEventPrizeController)

local InitLeftUI = function(self)
	if CS.OPSEventPrizeController.eventType == 1 then
		self.adapterLayout.localPosition = CS.UnityEngine.Vector3.zero;
		self.left:SetActive(false);
		if CS.OPSEventPrizeController.eventprizeId ~= 0 then
			for i=0,CS.GameData.alleventPrizeData.Count-1 do
				if CS.GameData.alleventPrizeData[i].prizeLevelId == CS.OPSEventPrizeController.eventprizeId then
					self.currentEventPrizeData = CS.GameData.alleventPrizeData[i];
				end
			end
		elseif CS.GameData.eventPrizeData.Count>0 then
			self.currentEventPrizeData = CS.GameData.eventPrizeData[0];
		end
		self:UpdateMainUI();
	else
		self:InitLeftUI();
	end
end

util.hotfix_ex(CS.OPSEventPrizeController,'InitLeftUI',InitLeftUI)
