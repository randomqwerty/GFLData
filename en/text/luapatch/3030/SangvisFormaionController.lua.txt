local _, LuaDebuggee = pcall(require, 'LuaDebuggee')
if LuaDebuggee and LuaDebuggee.StartDebug then
	LuaDebuggee.StartDebug('127.0.0.1', 9826)
else
	print('Please read the FAQ.pdf')
end
local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisFormaionController)
local myRequestGunSangvisPresetHandler = function(self,www)
		print("myRequestGunSangvisPresetHandler");
		if CS.ConnectionController.CheckONE(www.text) then
			for i = 0, self.teamBefore.Length - 1 do
				if (self.teamBefore[i] ~= nil) then
					self.teamBefore[i].teamId = 0;
				end
			end
			for i = 0, self.gunTeamAfter.Length - 1 do
				if self.gunTeamAfter[i] ~= nil then
					self.gunTeamAfter[i].teamId = self.currentSelectedTeam;
					self.gunTeamAfter[i].location = i + 1;
					self.gunTeamAfter[i].pos = CS.GF.Battle.GridPos(self.teamPosId3After[i]);
				end
			end
			CS.GameData.UpdateTeamList();
			for i = 0, CS.GameData.dictTeam[self.currentSelectedTeam].Count - 1 do
				CS.GameData.dictTeam[self.currentSelectedTeam][i]:UpdateData();
			end
			CS.FormationController.Instance:UpdateTotalPoint();
			CS.FormationController.Instance:InitNormalFormaionView(self.currentSelectedTeam);
			CS.FormationController.Instance:UpdateTeamLabel();
			if CS.FormationSettingController.Instance ~= nil and CS.FormationSettingController.Instance.gameObject.activeInHierarchy then
				CS.FormationSettingController.Instance:Init(self.currentSelectedTeam);
				CS.FormationSettingController.Instance.hasUsedTemplate = true;
				CS.CommonCharacterRecord.InstanceUse:ShowOrHide();
				if CS.FormationSettingController.Instance.currentControllerType == CS.FormationSettingControllerType.ChoseSangvis then
					CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.leftPanel);
					CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.rightPanel);
					CS.CommonCharacterRecord.InstanceUse:ShowOrHide(false);
				end
				self.teamRecord = nil;
			end	
			if CS.SwithFormationWindowController.Instance ~= nil then
				CS.SwithFormationWindowController.Instance:Close();
			end						
			if(CS.OneClickFormationWindonwController.Instance ~= nil) then
				CS.OneClickFormationWindonwController.Instance:Close();
			end
			if(CS.NoTypeGunWindowController.Instance ~= nil) then
				CS.NoTypeGunWindowController.Instance:Close();
			end
		end
end
local myRequestUseSangvisPresetHandler = function(self,www)
	print("myRequestUseSangvisPresetHandler");
	if CS.ConnectionController.CheckONE(www.text) then
		for i = 0, self.teamBefore.Length - 1 do
			if (self.teamBefore[i] ~= nil) then
				self.teamBefore[i].teamId = 0;
			end
		end
		for i = 0, self.teamAfter.Length - 1 do
			if (self.teamAfter[i] ~= nil) then
				self.teamAfter[i].teamId = self.currentSelectedTeam;
				self.teamAfter[i].location = i + 1;
				self.teamAfter[i].pos = CS.GF.Battle.GridPos(self.teamPosId3After[i]);
				if(self.teamAfter[i] ~= nil) then
					if (CS.FormationSettingController.Instance ~= nil) then
						if (CS.FormationSettingController.Instance.sangvisLocationMap:ContainsKey(self.teamAfter[i].id)) then
							CS.FormationSettingController.Instance.sangvisLocationMap[self.teamAfter[i].id] = self.teamPosId3After[i];
						else
							CS.FormationSettingController.Instance.sangvisLocationMap:Add(self.teamAfter[i].id, self.teamPosId3After[i]);
						end
					end
				end
			end
		end
		CS.GameData.UpdateTeamList();
		for i = 0, CS.GameData.dictTeam[self.currentSelectedTeam].Count - 1 do
			CS.GameData.dictTeam[self.currentSelectedTeam][i]:UpdateData();
		end
		self:InitView(self.currentSelectedTeam);
		CS.FormationController.Instance:UpdateTotalPoint();
		if CS.FormationSettingController.Instance ~= nil and CS.FormationSettingController.Instance.gameObject.activeInHierarchy then
			CS.FormationSettingController.Instance:Init(self.currentSelectedTeam);
			CS.FormationSettingController.Instance.hasUsedTemplate = true;
			CS.CommonCharacterRecord.InstanceUse:ShowOrHide();
			if CS.FormationSettingController.Instance.currentControllerType == CS.FormationSettingControllerType.ChoseSangvis then
				CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.leftPanel);
				CS.UITweenManager.KillTween(CS.CommonCharacterRecord.InstanceUse.rightPanel);
				CS.CommonCharacterRecord.InstanceUse:ShowOrHide(false);
			end
			self.teamRecord = nil;
		end	
		if CS.SwithFormationWindowController.Instance ~= nil then
			CS.SwithFormationWindowController.Instance:Close();
		end						
		if(CS.OneClickFormationWindonwController.Instance ~= nil) then
			CS.OneClickFormationWindonwController.Instance:Close();
		end
		if(CS.NoTypeGunWindowController.Instance ~= nil) then
			CS.NoTypeGunWindowController.Instance:Close();
		end
	end
end
util.hotfix_ex(CS.SangvisFormaionController,'RequestGunSangvisPresetHandler',myRequestGunSangvisPresetHandler)
util.hotfix_ex(CS.SangvisFormaionController,'RequestUseSangvisPresetHandler',myRequestUseSangvisPresetHandler)