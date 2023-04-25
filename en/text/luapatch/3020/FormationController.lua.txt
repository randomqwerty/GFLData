local util = require 'xlua.util'
xlua.private_accessible(CS.FormationController)
local myRequestChangeTeamTotalHandle = function(self,request)
	print("myRequestChangeTeamTotalHandle");
	for i = 0, 4 do
		self.arrCharacterLabel[i].gun = CS.GameData.dictTeam[self.currentSelectedTeam].dictLocation[i + 1];
		self.arrCharacterLabel[i]:UpdateInfo(-1);
		self.arrEquipInfo[i]:Init(self.arrCharacterLabel[i].gun, self.isShowEquipInfo);
	end
	CS.FormationController.Instance:UpdateTotalPoint();
	if(CS.FormationSettingController.Instance ~= nil and CS.FormationSettingController.Instance.gameObject.activeInHierarchy and (CS.SwithFormationWindowController.Instance == nil or (CS.SwithFormationWindowController.Instance ~= nil and CS.SwithFormationWindowController.Instance.gameObject.activeInHierarchy == false))) then
		CS.FormationSettingController.Instance:Init(self.currentSelectedTeam);
		CS.FormationSettingController.Instance.hasUsedTemplate = true;
		CS.CommonCharacterRecord.InstanceUse:ShowOrHide();
		if (CS.FormationSettingController.Instance.currentControllerType == CS.FormationSettingControllerType.ChoseGun) then
			CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.leftPanel);
			CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.rightPanel);
			CS.CommonCharacterRecord.InstanceUse:ShowOrHide(false);
			CS.AutoFormationTeamNodeController.Instance:OnClickCancel();
		end
	end
	if (CS.SwithFormationWindowController.Instance ~= nil) then
		CS.SwithFormationWindowController.Instance:Close();
	end
	if (CS.OneClickFormationWindonwController.Instance ~= nil) then
		CS.OneClickFormationWindonwController.Instance:Close();
	end
	if (CS.NoTypeGunWindowController.Instance ~= nil) then
		CS.NoTypeGunWindowController.Instance:Close();
	end
	self.teamRecord = nil;
end
local myRequestChangeSangvisPresetHandler = function(self, request)
	print("myRequestChangeSangvisPresetHandler");
	if (self.currentSelectedTeamType == CS.CurrentTeamType.GunTeam) then
		self.currentSelectedTeamType = CS.CurrentTeamType.SangvisTeam;
		self:ChangeToSangvisTeamUI(self.currentSelectedTeam);
		self:UpdateTeamLabel();
	end
	if(CS.FormationSettingController.Instance ~= nil and CS.FormationSettingController.Instance.gameObject.activeInHierarchy) then
		CS.FormationSettingController.Instance:Init(self.currentSelectedTeam);
		CS.FormationSettingController.Instance.hasUsedTemplate = true;
		CS.CommonCharacterRecord.InstanceUse:ShowOrHide();
		CS.SangvisFormaionController.Instance.gameObject:SetActive(false);
		if (CS.FormationSettingController.Instance ~= nil and (CS.SwithFormationWindowController.Instance == nil or (CS.SwithFormationWindowController.Instance ~= nil and CS.SwithFormationWindowController.Instance.gameObject.activeInHierarchy == false))) then
			if (CS.FormationSettingController.Instance.currentControllerType == CS.FormationSettingControllerType.ChoseSangvis )then
				CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.leftPanel);
				CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.rightPanel);
				CS.CommonCharacterRecord.InstanceUse:ShowOrHide(false);
			end
		end
	end
	if (CS.SwithFormationWindowController.Instance ~= nil)then
		CS.SwithFormationWindowController.Instance:Close();
	end
	if (CS.OneClickFormationWindonwController.Instance ~= nil)then
		CS.OneClickFormationWindonwController.Instance:Close();
	end
	if (CS.NoTypeGunWindowController.Instance ~= nil)then
		CS.NoTypeGunWindowController.Instance:Close();
	end
	self.teamRecord = nil;
end
util.hotfix_ex(CS.FormationController,'RequestChangeTeamTotalHandle',myRequestChangeTeamTotalHandle)
util.hotfix_ex(CS.FormationController,'RequestChangeSangvisPresetHandler',myRequestChangeSangvisPresetHandler)