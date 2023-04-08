local util = require 'xlua.util'
xlua.private_accessible(CS.HomeUserInfoNewController)
xlua.private_accessible(CS.AdjutantChooseController)
local myOnClickAdjustant = function(self)
    self:OnClickAdjustant()
	CS.AdjutantChooseController.Instance:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingLayerName = "UI";
end
util.hotfix_ex(CS.HomeUserInfoNewController,'OnClickAdjustant',myOnClickAdjustant)