local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUITheaterConditionsController)

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		self.transform.gameObject:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2080/评分条件 1");
	end
end

util.hotfix_ex(CS.BattleUITheaterConditionsController,'InitUIElements',InitUIElements)

