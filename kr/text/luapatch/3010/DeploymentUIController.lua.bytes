local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)
xlua.private_accessible(CS.DeploymentController)

local showrouge = false;
--更改遮罩层级
local Awake = function(self)
	self:Awake();
	local canvasself = self.transform:GetComponent(typeof(CS.UnityEngine.Canvas));
	local canvas = self.goAbove:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = 29;
	showrouge = false;
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

local OnSelectTeamSkillUI = function(self,team)
	if team ~= nil then
		if team.currentSpot.currentTeam ~= team then
			self:OnSelectTeamSkillUI(nil);
			return;
		end
	end
	self:OnSelectTeamSkillUI(team);
end

local ShowBuildSkill = function(self,missionskills)
	self.skills = self:showUseMissionSkills(missionskills);
	self.leftSkills:Clear();
	self.rightSkills:Clear();
	local skillOthers = CS.System.Collections.Generic.List(CS.BuildSkillDetail)();
	for i=0,self.skills.Count-1 do
		local skill = self.skills[i];
		if skill.uicfg == nil then
			skill.isLeft = false;
			self.rightSkills:Add(skill);
		elseif skill.uicfg.is_manual_target == 3 then
			skillOthers:Add(skill);
		else			
			if skill.uicfg.use_fairy_ui == 0 then
				skill.isLeft = true;
				self.leftSkills:Add(skill);
			else
				skill.isLeft = false;
				self.rightSkills:Add(skill);		
			end			
		end
	end
	self:ShowLeftBuildSkillUI();
	self:ShowRightBuildSkillUI();
	self.show = true;
	if CS.DeploymentUIController.unfoldvertical then
		self:ClickMessage();
	end
	if skillOthers.Count == 0 then
		return;
	end
	print("技能总数"..skillOthers.Count);
	local useSkills = CS.System.Collections.Generic.List(CS.BuildSkillDetail)();
	for i=0,3 do
		if skillOthers.Count>0 then
			local index = CS.UnityEngine.Random.Range(0,skillOthers.Count-1);
			index = CS.Mathf.RoundToInt(index);
			print("index"..index);
			local skill = skillOthers[index];
			print("选择技能"..skill.skill.id);
			useSkills:Add(skill);
			skillOthers:Remove(skill);
		end
	end
	if useSkills.Count>0 then
		if not showrouge then
			ShowRougeUI(useSkills);
		end
	else
		CloseRougeUI();
	end
end
local rougeUI;
function ShowRougeUI(skills)
	if rougeUI == nil or  rougeUI:isNull() then
		rougeUI = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2023RougeSpring_BuffSelector"), CS.DeploymentUIController.Instance.transform, false);
	end
	CS.CommonAudioController.PlayUI("UI_23Spring_Card_Show");
	showrouge = true;
	rougeUI.gameObject:SetActive(true);
	local parent = rougeUI.transform:Find("MainFrame/CardList/CardLayout");
	while parent.childCount < skills.Count do
		local child = CS.UnityEngine.Object.Instantiate(parent:GetChild(0).gameObject);
		child.transform:SetParent(parent,false);
	end
	for i=0,parent.childCount-1 do
		local child = parent:GetChild(i);
		if i<skills.Count then
			child.gameObject:SetActive(true);
			local txtName = child:Find("Name/Tex_Name"):GetComponent(typeof(CS.ExText));
			txtName.text = skills[i].skill.name;
			local imageIcon = child:Find("Img_Icon"):GetComponent(typeof(CS.ExImage));
			imageIcon.sprite = CS.CommonController.LoadPngCreateSprite("Pics/Icons/Enemy/"..skills[i].uicfg.iconCode);
			local txtDec = child:Find("Description/Tex_Description"):GetComponent(typeof(CS.ExText));
			txtDec.text = skills[i].skill.description;
			local btnBg = child:Find("Img_Bg"):GetComponent(typeof(CS.ExButton));
			child:Find("OnSelect").gameObject:SetActive(false);
			child:Find("TouchArea").gameObject:SetActive(false);
			btnBg.onClick:RemoveAllListeners();
			btnBg:AddOnClick(function()
				for j=0,parent.childCount-1 do
					parent:GetChild(j):Find("OnSelect").gameObject:SetActive(false);
				end
				child:Find("OnSelect").gameObject:SetActive(true);	
				child:Find("TouchArea").gameObject:SetActive(true);
				CS.CommonAudioController.PlayUI("UI_23Spring_Card_Select");
			end)
			local btnSelect = child:Find("TouchArea"):GetComponent(typeof(CS.ExButton));
			btnSelect.onClick:RemoveAllListeners();
			btnSelect:AddOnClick(function()
					skills[i]:RequestGameCastSkill(true);
					CloseRougeUI();
					CS.CommonAudioController.PlayUI("UI_23Spring_Card_Get");
				end)
		else
			child.gameObject:SetActive(false);
		end
	end
end
function CloseRougeUI()
	if rougeUI ~= nil and not rougeUI:isNull() then
		rougeUI.gameObject:SetActive(false);
	end
	showrouge = false;
end

local CheckMove = function()
	print("CheckMove");
	if rougeUI ~= nil and not rougeUI:isNull() then
		if rougeUI.gameObject.activeInHierarchy then
			CS.DeploymentPlanModeController.CancelPlan();		
			return;
		end
	end
	CS.DeploymentController.Instance:RequestMoveTeam();
end
local TriggerMoveTeamEvent = function()
	CS.DeploymentController.AddAction(CheckMove,0.1);
end

local CheckCanUseBuild = function(self,team)
	if team == nil then
		CS.DeploymentUIController.Instance:CloseBuildControlUI();
	else
		if team:CanPlayerHandControl() then
			self:CheckTeamBuff(team);
		else
			CS.DeploymentUIController.Instance:CloseBuildControlUI();
		end
	end
end
util.hotfix_ex(CS.DeploymentUIController,'Awake',Awake)
util.hotfix_ex(CS.DeploymentUIController,'RefreshText',RefreshText)
util.hotfix_ex(CS.DeploymentUIController,'ShowLeftBuildSkillUI',ShowLeftBuildSkillUI)
util.hotfix_ex(CS.DeploymentUIController,'ShowRightBuildSkillUI',ShowRightBuildSkillUI)
util.hotfix_ex(CS.DeploymentUIController,'OnSelectTeamSkillUI',OnSelectTeamSkillUI)
util.hotfix_ex(CS.DeploymentUIController,'ShowBuildSkill',ShowBuildSkill)
util.hotfix_ex(CS.DeploymentController,'TriggerMoveTeamEvent',TriggerMoveTeamEvent)
util.hotfix_ex(CS.DeploymentController,'CheckCanUseBuild',CheckCanUseBuild)



