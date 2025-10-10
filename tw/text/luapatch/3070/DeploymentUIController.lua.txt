local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)


local RefreshItemUI = function(self)
	self:RefreshItemUI();
	if self.itemShowObj == nil or self.itemShowObj:isNull() then
		return;
	end
	local name = self.itemShowObj.name;
	if self:Is1ItemObj(name) or self:IsItemsObj(name) then
		return;
	end
	local ButtonTrans = self.itemShowObj.transform:Find("TipsButton");
	if ButtonTrans == nil then
		return;
	end
	local button = ButtonTrans:GetComponent(typeof(CS.ExButton));
	local url = ButtonTrans:Find("URL"):GetComponent(typeof(CS.ExText)).text;
	button.onClick:RemoveAllListeners();
	button:AddOnClick(function()
		CS.OPSWebWindows.Show(url);
	end)
end

local skills = nil;
local canShowFightBuffUI = function(self)
	for i=0,self.buffCurrentLayerSkills.Count-1 do
		if self.buffCurrentLayerSkills[i].info.isShow then
			return true;
		end
	end
	return false;
end
local CheckFightBuff = function(self)
	self:CheckFightBuff();
	skills = CS.System.Collections.Generic.List(CS.DeploymentUIController.BattleEnvironmentData)(self.buffCurrentLayerSkills);
	self.buffCurrentLayerSkills:Clear();
	for i=0,skills.Count-1 do
		if skills[i].info.isShow then
			self.buffCurrentLayerSkills:Add(skills[i]);
		end
	end
end
local ShowFightBuffUI = function(self)
	self:ShowFightBuffUI();
	self.buffCurrentLayerSkills = CS.System.Collections.Generic.List(CS.DeploymentUIController.BattleEnvironmentData)(skills);
end

local ShowTheaterGroup = function(self)
	self:ShowTheaterGroup();
	if self.buffParent~=nil and not self.buffParent:isNull() then
		for i=0,self.buffParent.childCount-1 do
			local child = self.buffParent:GetChild(i);
			if i<self.skills.Count then
				if self.skills[i].isShow then
					child.gameObject:SetActive(true);
					local image = child:Find("Img_Buff"):GetComponent(typeof(CS.UnityEngine.UI.Image));
					local skill = CS.ResManager.GetObjectByPath("Pics/Icons/Skill/" .. skills[i].code);
					if skill ~= nil then
						image.sprite = skill:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
					end
					local tip = child:Find("Img_Buff"):GetComponent(typeof(CS.CommonShowTip));
					tip.strTitle = skills[i].name;
					tip.strIntroduction = skills[i].description;
				else
					child.gameObject:SetActive(false);
				end
			else
				child.gameObject:SetActive(false);
			end
		end
	end
end

local UpDateGunsEnemy = function(self)
	self:UpDateGuns();
	for i=0,self.enemyGuns.Count-1 do
		local AttackPower = self.enemyGuns[i].AttackPower;
		local DefencePower = self.enemyGuns[i].DefencePower;
	end
end
local UpDateGunsAlly = function(self)
	self:UpDateGuns();
	if self:CurrentTeamBelong() ~= CS.TeamBelong.friendly then
		for i=0,self.allyTeam.EnemyGuns.Count-1 do
			local AttackPower = self.allyTeam.EnemyGuns[i].AttackPower;
			local DefencePower = self.allyTeam.EnemyGuns[i].DefencePower;
		end
	end
end
util.hotfix_ex(CS.DeploymentUIController,'RefreshItemUI',RefreshItemUI)
util.hotfix_ex(CS.DeploymentUIController,'canShowFightBuffUI',canShowFightBuffUI)
util.hotfix_ex(CS.DeploymentUIController,'CheckFightBuff',CheckFightBuff)
util.hotfix_ex(CS.DeploymentUIController,'ShowFightBuffUI',ShowFightBuffUI)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowTheaterGroup',ShowTheaterGroup)
util.hotfix_ex(CS.DeploymentEnemyTeamController,'UpDateGuns',UpDateGunsEnemy)
util.hotfix_ex(CS.DeploymentAllyTeamController,'UpDateGuns',UpDateGunsAlly)