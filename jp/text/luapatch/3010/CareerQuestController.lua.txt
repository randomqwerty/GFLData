local util = require 'xlua.util'
xlua.private_accessible(CS.CareerQuestController)
local myStart = function(self)
	self.starObj:GetComponent(typeof(CS.UnityEngine.RectTransform)).sizeDelta = CS.UnityEngine.Vector2(797.3, 707);
	self.diamondObj:GetComponent(typeof(CS.UnityEngine.RectTransform)).sizeDelta = CS.UnityEngine.Vector2(700, 700);
    self:Start()
end
util.hotfix_ex(CS.CareerQuestController,'Start',myStart)