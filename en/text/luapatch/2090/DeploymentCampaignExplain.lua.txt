local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentCampaignExplain)
xlua.private_accessible(CS.CommonIconController)
local CheckNightText = function(self,textSCondition)
	local txt;
	if CS.GameData.currentSelectedMissionInfo.expectedFriendlyDieNumber == 0 then		
		txt = CS.Data.GetLang(30488);
	else
		txt = CS.System.String.Format(CS.Data.GetLang(30489), CS.GameData.currentSelectedMissionInfo.expectedFriendlyDieNumber);
	end
	if CS.GameData.currentSelectedMissionInfo.expectedTurn ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30490), CS.GameData.currentSelectedMissionInfo.expectedTurn);
	end
	if CS.GameData.currentSelectedMissionInfo.expectedEnemyDieNumber ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30491), CS.GameData.currentSelectedMissionInfo.expectedEnemyDieNumber);
	end
	if CS.GameData.currentSelectedMissionInfo.hostageTotalNum ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30492), CS.GameData.currentSelectedMissionInfo.hostageTotalNum);
	end
	if CS.GameData.currentSelectedMissionInfo.expectLineTurn ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30493), CS.GameData.currentSelectedMissionInfo.expectLineTurn);
	end
	textSCondition.text = txt;
end
local _IconInit = function(self)
	local txt1 = self.transform:Find("HaveDropGun/Image/UI_Text"):GetComponent(typeof(CS.ExText));
	if txt1~=nil then 
		txt1.text = CS.Data.GetLang(30494);
	end 
end
local _InitUIElements = function(self)
	self:InitUIElements(); 
	xlua.hotfix(CS.CommonIconController,'Awake',_IconInit)
end
local _OnDestroy = function(self)
	xlua.hotfix(CS.CommonIconController,'Awake',nil)
	self:OnDestroy();
end
util.hotfix_ex(CS.DeploymentCampaignExplain,'CheckNightText',CheckNightText)
util.hotfix_ex(CS.DeploymentCampaignExplain,'InitUIElements',_InitUIElements)
util.hotfix_ex(CS.DeploymentCampaignExplain,'OnDestroy',_OnDestroy)


