local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyInfoNew)
xlua.private_accessible(CS.DeploymentEnemyInfoDetail)

local CheckMapSpecialSpotInfo = function(self)
	for i=0,self.currentSpot.spotAction.listSpecialAction.Count-1 do
		local specialspot = self.currentSpot.spotAction.listSpecialAction[i];
		self.currentSpot.effectSepcialSpot:Remove(specialspot);
	end
	return self:CheckMapSpecialSpotInfo();
end

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Right/Img_BattleType/Tex_BattleType");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40505);
		txtPoint = self.transform:Find("Right/BtnLayout/Btn_AIType/Img_AIType/Tex_AIType");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(30256);
		txtPoint = self.transform:Find("Top/Information/InfoList/InfoListContent/Info/Img_Title/Tex_Title");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(33046);
	end
end
local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Windows/Left/Bottom/NoSkill/Tex_NoSkill");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40492);
	end
end
util.hotfix_ex(CS.DeploymentEnemyInfoNew,'CheckMapSpecialSpotInfo',CheckMapSpecialSpotInfo)
util.hotfix_ex(CS.DeploymentEnemyInfoNew,'Awake',Awake)
util.hotfix_ex(CS.DeploymentEnemyInfoDetail,'InitUIElements',InitUIElements)