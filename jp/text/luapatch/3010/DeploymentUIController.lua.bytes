local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

--更改遮罩层级
local Awake = function(self)
	self:Awake();
	local canvasself = self.transform:GetComponent(typeof(CS.UnityEngine.Canvas));
	local canvas = self.goAbove:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = 29;
end

--修正按钮显示
local RefreshText = function(self)
	self:RefreshText();
	if self.btnResultMission.gameObject.activeInHierarchy then
		self.btnAbortMission.gameObject:SetActive(false);
	end
end

local ShowLeftBuildSkillUI = function(self)
	self:ShowLeftBuildSkillUI();
	if self.leftSkills.Count>0 then
		local CurveMove = self.buildSkillUI:GetComponent(typeof(CS.CommonListCurveMove));
		CurveMove.baseorder = 2;
	end
end

local ShowRightBuildSkillUI = function(self)
	self:ShowRightBuildSkillUI();
	if self.rightSkills.Count>0 then
		local CurveMove = self.buildSkillUIRight:GetComponent(typeof(CS.CommonListCurveMove));
		CurveMove.baseorder = 2;
	end
end
util.hotfix_ex(CS.DeploymentUIController,'Awake',Awake)
util.hotfix_ex(CS.DeploymentUIController,'RefreshText',RefreshText)
util.hotfix_ex(CS.DeploymentUIController,'ShowLeftBuildSkillUI',ShowLeftBuildSkillUI)
util.hotfix_ex(CS.DeploymentUIController,'ShowRightBuildSkillUI',ShowRightBuildSkillUI)



