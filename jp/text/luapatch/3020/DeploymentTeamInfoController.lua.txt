local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)

local ReinforceSquadTeam = function(self,squadDataController)
	if squadDataController.squad.status ~= CS.SquadStatus.normal then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(1413));
		return;
	end
	self:ReinforceSquadTeam(squadDataController);
end
local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
		local txtP = self.transform:Find("TeamPanel/btnSwitch/Text_TeamSet"):GetComponent(typeof(CS.ExText));
		txtP.text = CS.Data.GetLang(30551);
		txtP.rectTransform.anchorMin = CS.UnityEngine.Vector2(0.5,0.5);
		txtP.rectTransform.anchorMax = CS.UnityEngine.Vector2(0.5,0.5);
		txtP.rectTransform.sizeDelta = CS.UnityEngine.Vector2(215,72);
	end
end
util.hotfix_ex(CS.DeploymentTeamInfoController,'ReinforceSquadTeam',ReinforceSquadTeam)
util.hotfix_ex(CS.DeploymentTeamInfoController,'InitUIElements',InitUIElements)
