local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local CheckMapAnimator = function(self)
	if self.lastSelectOrder ~= CS.OPSPanelController.currentSelectOrder then
		self.CanClick = false;
	end
	local playGroup = self.leftMain.gameObject:GetComponent(typeof(CS.TweenPlayGroup));
	if playGroup == nil or playGroup:isNull() then
		playGroup = self.leftMain.gameObject:AddComponent(typeof(CS.TweenPlayGroup));
	end
	if self.lastSelectOrder == -1 then
		playGroup.CurrentTweenPlayOrder = (CS.OPSPanelController.currentSelectOrder + 1) * 10 + (CS.OPSPanelController.currentSelectOrder + 1);
		CS.CommonController.Invoke(function()
				playGroup:PlayCurrentAllyOrderTween();
			end,0.3,CS.OPSPanelController.Instance);
	elseif self.lastSelectOrder ~= CS.OPSPanelController.currentSelectOrder then
		playGroup.CurrentTweenPlayOrder = (self.lastSelectOrder + 1) * 10 + (CS.OPSPanelController.currentSelectOrder + 1);
		playGroup:PlayCurrentAllyOrderTween();
	end
	self:CheckMapAnimator();
end

local EndMapAnimator = function(self)
	self:EndMapAnimator();
	self.CanClick = true;
end
local SelectMapAnimatorDefault = function(self)
	self:SelectMapAnimatorDefault();
	self.CanClick = true;
end
local InitBgm = function(self)
	self:InitBgm();
	local bgmname = "Campaion"..tostring(self.campaionId).."-"..tostring(CS.OPSPanelController.currentSelectOrder+1);
	CS.CommonAudioController.PlayBGM(bgmname);
end
local CheckModuleSpine = function(self)
	if self.currentPanelConfig.opsSpineMissions.Keys.Count == 0 then
		return;
	end
	local iter = self.currentPanelConfig.opsSpineMissions:GetEnumerator();     
	while iter:MoveNext() do    
		local code = iter.Current.Key;
		local opsspinemission = iter.Current.Value;
		local currentIndex = opsspinemission:CheckMissionShowOrder();
		if opsspinemission.currentOrder ~= currentIndex then
			opsspinemission.currentOrder = currentIndex;
			local moduleControl = nil;
			for i=0,self.moduleControls.Count -1 do
				if self.moduleControls[i].currentModuleDataName == opsspinemission.moudleName or self.moduleControls[i].gameObject.name == opsspinemission.moudleName then
					moduleControl = self.moduleControls[i];
				end
			end
			if moduleControl ~= nil then
				if currentIndex<0 then
					local trans = moduleControl.transform:Find(code);
					if trans ~= nil  then
						print("隐藏spine"..code);
						trans.gameObject:SetActive(false);
					end
				else
					opsspinemission.moudleIndex = self.moduleControls:IndexOf(moduleControl);
					local aiIndex = opsspinemission:GetAIMissionIndex();
					aiIndex = CS.Mathf.Clamp(aiIndex, 0, opsspinemission.opsSpineAI.Count - 1);
					if opsspinemission.opsSpineAI.Count>0 then
						moduleControl:InitMoveSpine(code,opsspinemission.opsSpineAI[aiIndex]);
					end
				end
			end
		end
	end              
end
util.hotfix_ex(CS.OPSPanelController,'CheckMapAnimator',CheckMapAnimator)
util.hotfix_ex(CS.OPSPanelController,'EndMapAnimator',EndMapAnimator)
util.hotfix_ex(CS.OPSPanelController,'SelectMapAnimatorDefault',SelectMapAnimatorDefault)
util.hotfix_ex(CS.OPSPanelController,'InitBgm',InitBgm)
util.hotfix_ex(CS.OPSPanelController,'CheckModuleSpine',CheckModuleSpine)
