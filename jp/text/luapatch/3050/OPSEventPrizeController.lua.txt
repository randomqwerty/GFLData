local util = require 'xlua.util'
xlua.private_accessible(CS.OPSEventPrizeController)

local InitLeftUI = function(self)
	if CS.OPSEventPrizeController.eventType == 1 then
		if CS.OPSEventPrizeController.eventprizeId == 0 then
			if CS.OPSPanelController.Instance ~= nil and not CS.OPSPanelController.Instance:isNull() then
				if CS.OPSPanelController.Instance.campaionId == -59 then
					CS.OPSEventPrizeController.eventprizeId = 8;
				end
			end
		end
	end
	self:InitLeftUI();
end


util.hotfix_ex(CS.OPSEventPrizeController,'InitLeftUI',InitLeftUI)

