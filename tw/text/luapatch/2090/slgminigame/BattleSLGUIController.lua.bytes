local util = require 'xlua.util'
xlua.private_accessible(CS.BattleSLGUIController)
local flatSkillCancelFlag = false
local flatSkillCancelCounter = 0
local ShowMainSkillBtn = function(self)
	self:ShowMainSkillBtn()
	if self.mCurSkill ~= nil then
		local skillconfig = CS.GF.Battle.BattleSLGModeController.Instance.battleSLGMinigameSkillCfgs:GetDataById(self.mCurSkill.info.id)	
		if skillconfig ~= nil then
			if skillconfig.cost < 0 then
				self.textGunMainSkillCost.text = "0"
			end
		end
	end
end
--指挥官生成有问题 所以先都干掉了
local InitCommanderSpine = function(self)

	--self:InitCommanderSpine()
	--if self.commanderSpine ~= nil then
	--	self.commanderSpine:SetOrderInLayer(12)
	--	self.commanderSpine.gameObject.transform.localScale = CS.UnityEngine.Vector3(180,180,180)
	--end
end
local InitCommanderSpine_Result = function(self)
	--self:InitCommanderSpine()
	--if self.commanderSpine ~= nil then
	--	self.commanderSpine:SetLayer("MessageBox")
	--	self.commanderSpine:SetOrderInLayer(18)
	--	self.commanderSpine.gameObject.transform.localScale = CS.UnityEngine.Vector3(240,240,240)
	--end
end
local InitCommanderSkill = function(self)
	self:InitCommanderSkill()
	self.commanderSkillGroupB.gameObject:SetActive(false)
end
local SwitchCommanderSkills = function(self)
	if self.curCommanderSkilPage == 1 then
		self.commanderSkillGroupB.gameObject:SetActive(true)
	else
		local obj = self:commanderSkillObject(2,4)
		self:commanderSkillObject(2,4):GetComponent(typeof(CS.TweenPlay)).EndHandle = function()
			self.commanderSkillGroupB.gameObject:SetActive(false)
		end
	end
	self:SwitchCommanderSkills()
end
local SetSelectedGun = function(self,gun)
	self.TransGunPart.gameObject:SetActive(true)
	self:SetAllOff()
	if self.dictGunPic:ContainsKey(gun) then
		self.dictGunPic[gun]:SetActive(true)
	else
		local go = CS.CommonController.LoadSmallPic(gun,self.TransGunPicHolder,CS.UnityEngine.Vector2.zero)
		self:OnLoadPic(go.gameObject,"",gun)
	end
	self:ShowAttackSkillBtn()
	self:ShowMainSkillBtn()
end
local OnClickExitButton = function(self)
	self:OnClickExitButton()
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
local InitTitle = function(self)
	self:InitTitle()
	self.gameObject.transform:Find("UI_Button_Exit").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			self:OnClickExitButton()
		end)
end
util.hotfix_ex(CS.BattleSLGUIController,'ShowMainSkillBtn',ShowMainSkillBtn)
util.hotfix_ex(CS.BattleSLGUIController,'InitCommanderSpine',InitCommanderSpine)
util.hotfix_ex(CS.BattleSLGUIController,'InitCommanderSkill',InitCommanderSkill)
util.hotfix_ex(CS.BattleSLGUIController,'SwitchCommanderSkills',SwitchCommanderSkills)
util.hotfix_ex(CS.BattleSLGUIResultController,'InitCommanderSpine',InitCommanderSpine_Result)
util.hotfix_ex(CS.BattleSLGUIResultController,'OnClickExitButton',OnClickExitButton)
util.hotfix_ex(CS.BattleSLGUIResultController,'InitTitle',InitTitle)
xlua.hotfix(CS.BattleSLGUIController,'SetSelectedGun',SetSelectedGun)
