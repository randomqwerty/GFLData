local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBackgroundController)

local Init = function(self)
	self:Init();
	if CS.GameData.missionAction ~= nil and CS.DeploymentBackgroundController.currentLayerData ~= nil then
		if CS.DeploymentBackgroundController.currentLayerData.effect == nil then
			CS.DeploymentBackgroundController.currentLayerData:ShowEffect();
		end
	end
end

local OnLevelLoaded = function(self)
	self:OnLevelLoaded();
	--CS.CommonAudioController.PlayUI("UI_Stop");
	--CS.CommonAudioController.PlayBattle("Stop_Battle_loop");
	--CS.CommonAudioController.PlayBattle("AVG_AMB_Rain_Stop");
	CS.CommonAudioController.StopBattleAudioTriggerEvent(CS.AudioSourceType.SoundSource);
end

local OnDestroy = function(self)
	self:OnDestroy();
	--CS.CommonAudioController.PlayUI("UI_Stop");
	--CS.CommonAudioController.PlayBattle("Stop_Battle_loop");
	--CS.CommonAudioController.PlayBattle("AVG_AMB_Rain_Stop");
	CS.CommonAudioController.StopBattleAudioTriggerEvent(CS.AudioSourceType.SoundSource);
end

util.hotfix_ex(CS.DeploymentBackgroundController,'Init',Init)
util.hotfix_ex(CS.DeploymentBackgroundController,'OnLevelLoaded',OnLevelLoaded)
util.hotfix_ex(CS.DeploymentBackgroundController,'OnDestroy',OnDestroy)


