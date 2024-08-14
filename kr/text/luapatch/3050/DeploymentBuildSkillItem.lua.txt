local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildSkillItem)

local RefreshLeftUI = function(self)
	self:RefreshLeftUI();
	local holder = self.transform:Find("Img_SpecialHolder");
	if self.buildSkill.uicfg.is_manual_target == 4 then
		if holder ~= nil then
			holder.gameObject:SetActive(true);
			local image = holder:GetComponent(typeof(CS.ExImage));
			local btn = holder:Find("Btn_TargetInfo"):GetComponent(typeof(CS.ExButton));
			image.sprite = CS.CommonController.LoadPngCreateSprite("Pics/Icons/Enemy/"..self.buildSkill.uicfg.iconCode);
			btn.onClick:RemoveAllListeners();
			btn:AddOnClick(function()
				self:CheckSkillTipContent();
			end);
		end
	else
		if holder ~= nil then
			holder.gameObject:SetActive(false);
		end
	end
end

local CastSkill = function(self)
	local missionskilliid = self:CheckMissionSkillId();
	if missionskilliid == 0 then
		return;
	end
	if self.playanim then
		return;
	end
	local buildSkill = nil;
	for i=0,CS.DeploymentUIController.Instance.leftSkills.Count-1 do
		local skill = CS.DeploymentUIController.Instance.leftSkills[i];
		if skill.skillItem.gameObject.name == "610001" then
			buildSkill = skill;
		end
	end
	if buildSkill == nil then
		return;
	end
	buildSkill.skillItem.RougeSummerObj = self.RougeSummerObj;
	buildSkill.skillItem.selectItems = self.selectItems;
	buildSkill.skillItem.playanim = true;
	buildSkill.skill = CS.GameData.listMissionSkillCfg:GetDataById(missionskilliid);
	buildSkill.otherskills:Clear();
	self:PlayRougeAnim(true);
	self.playanim = true;
	CS.CommonController.Invoke(function()
		buildSkill:RequestCastSkill();
		end,5,CS.DeploymentController.Instance);
end

local CheckCastRougeEnd = function(self)
	for i=0,CS.DeploymentUIController.Instance.leftSkills.Count-1 do
		local skill = CS.DeploymentUIController.Instance.leftSkills[i];
		if skill.skillItem ~= nil then
			skill.skillItem.playanim = false;
			skill.skillItem.selectItems:Clear();
		end
	end
	self:CheckCastRougeEnd();
end
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'CastSkill',CastSkill)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'CheckCastRougeEnd',CheckCastRougeEnd)