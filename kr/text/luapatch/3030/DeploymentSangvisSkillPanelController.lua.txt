local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSangvisSkillPanelController)

local RefreshVehicleSkill1 = function(self)
	self:RefreshVehicleSkill1();
	if self.vehicleTeam == nil then
		return;
	end
	local missionSkillCfg = self.vehicleTeam:GetMissionSkill(1);
	if missionSkillCfg ~= nil then
		local icon = CS.CommonController.InstantiateSkillIcon(missionSkillCfg.code);
		local parent = self.skill1Trans:Find("Img_IconBg/Img_Icon");
		parent:DestroyChildren();
		if icon ~= nil then
			icon.transform:SetParent(parent, false);
			local rectTrans = icon:GetComponent(typeof(CS.UnityEngine.RectTransform));
			rectTrans.sizeDelta = CS.UnityEngine.Vector2(80, 80);
		end
	end
	self.skill1Trans:Find("Level").gameObject:SetActive(false);
	self.skill1Trans:Find("NoLevel").gameObject:SetActive(true);
end

local RefreshVehicleSkill2 = function(self)
	self:RefreshVehicleSkill2();
	if self.vehicleTeam == nil then
		return;
	end
	local missionSkillCfg = self.vehicleTeam:GetMissionSkill(2);
	if missionSkillCfg ~= nil then
		local icon = CS.CommonController.InstantiateSkillIcon(missionSkillCfg.code);
		local parent = self.skill2Trans:Find("Img_IconBg/Img_Icon");
		parent:DestroyChildren();
		if icon ~= nil then
			icon.transform:SetParent(parent, false);
			local rectTrans = icon:GetComponent(typeof(CS.UnityEngine.RectTransform));
			rectTrans.sizeDelta = CS.UnityEngine.Vector2(80, 80);
		end
	end
	self.skill2Trans:Find("Level").gameObject:SetActive(false);
	self.skill2Trans:Find("NoLevel").gameObject:SetActive(true);
end

local RefreshVehicleSkill3 = function(self)
	self:RefreshVehicleSkill3();
	self.skill3Trans:Find("Level").gameObject:SetActive(false);
	self.skill3Trans:Find("NoLevel").gameObject:SetActive(true);
end
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'RefreshVehicleSkill1',RefreshVehicleSkill1)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'RefreshVehicleSkill2',RefreshVehicleSkill2)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'RefreshVehicleSkill3',RefreshVehicleSkill3)

