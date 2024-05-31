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

util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)