local util = require 'xlua.util'
xlua.private_accessible(CS.AVGController)

local DestoryAVG = function(self)
	self:DestoryAVG();
	if CS.OPSPanelController.Instance ~= nil and not CS.OPSPanelController.Instance:isNull() then
		CS.OPSPanelController.Instance:InitBgm();
		CS.OPSPanelController.Instance:RefreshUI();
		CS.OPSPanelController.Instance:CheckAnim();
	end
end
local DialogueShowContentEmpty = function(self)
	
end
local OnClickHideUi = function(self)
	if not self.isHidingUI then
		xlua.hotfix(CS.AVGController,'DialogueShowContent',DialogueShowContentEmpty);
		self:OnClickHideUi();
		xlua.hotfix(CS.AVGController,'DialogueShowContent',nil);
	else
		self:OnClickHideUi();
	end
end
local _PlayAudioAVGEffect = function(self,name)
	if name == 'Stop_AVG_loop' then
		if CS.ConfigData.playEffect == true then
			CS.CommonAudioController.StopAVGSEAudio();
		end
	else
		self:PlayAudioAVGEffect(name);
	end
end
--util.hotfix_ex(CS.AVGController,'DestoryAVG',DestoryAVG)
util.hotfix_ex(CS.AVGController,'OnClickHideUi',OnClickHideUi)
util.hotfix_ex(CS.AVGController,'PlayAudioAVGEffect',_PlayAudioAVGEffect)