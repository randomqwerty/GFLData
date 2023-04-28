local util = require 'xlua.util'
xlua.private_accessible(CS.HomeUserInfoNewController)
xlua.private_accessible(CS.AdjutantChooseController)
xlua.private_accessible(CS.AdjutantChooseLabel)
local myOnClickAdjustant = function(self)
    self:OnClickAdjustant()
	CS.AdjutantChooseController.Instance:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingLayerName = "UI";
end
local myOnAddBtnClicked = function(self)
	self:OnAddBtnClicked()
	CS.AdjutantListController.Instance:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingLayerName = "UI";
end
local myOnChangeBtnClicked = function(self)
	self:OnChangeBtnClicked()
	CS.AdjutantListController.Instance:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingLayerName = "UI";
	print("----")
end
util.hotfix_ex(CS.HomeUserInfoNewController,'OnClickAdjustant',myOnClickAdjustant)
util.hotfix_ex(CS.AdjutantChooseLabel,'OnAddBtnClicked',myOnAddBtnClicked)
util.hotfix_ex(CS.AdjutantChooseLabel,'OnChangeBtnClicked',myOnChangeBtnClicked)