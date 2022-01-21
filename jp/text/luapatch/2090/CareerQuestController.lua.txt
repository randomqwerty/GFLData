local util = require 'xlua.util'
xlua.private_accessible(CS.CareerQuestController)
local myStart = function(self)
    self:Start()
	if CS.CareerQuestUnitController.Instance ~= nil then
		CS.CareerQuestUnitController.Instance.infoTweenPlay:DoKill();
        CS.CareerQuestUnitController.Instance.infoTweenPlay:GetComponent(typeof(CS.UnityEngine.CanvasGroup)).alpha = 1;
	end
end
util.hotfix_ex(CS.CareerQuestController,'Start',myStart)