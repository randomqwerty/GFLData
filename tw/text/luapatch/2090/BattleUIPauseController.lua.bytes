local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUIPauseController)



local OnClickRestartBattle = function(self)
	if CS.BattleFrameManager.IsStopTime() then
		return
	end
	self:OnClickRestartBattle()
end

local InitUIElements= function(self)
	self:InitUIElements();
	local topTime = self.transform:Find("InPause/ButtonFightAgainImg");
	local obj1 = CS.ResManager.GetObjectByPath("AtlasClips2090/重新战斗");
	if obj1 ~= nil then
		print("载入图片");
		topTime:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
	end
end
util.hotfix_ex(CS.BattleUIPauseController,'OnClickRestartBattle',OnClickRestartBattle)
util.hotfix_ex(CS.BattleUIPauseController,'InitUIElements',InitUIElements)
