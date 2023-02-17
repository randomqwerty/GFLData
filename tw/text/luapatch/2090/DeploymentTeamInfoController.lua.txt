local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)

local OnClickTeam = function(self,spot)
	for i=0,self.labelControllers.Length-1 do
		local label = self.labelControllers[i];
		label.gun = nil;
		label.teamid = 0;
		label:Init(i);
	end
	self:OnClickTeam(spot);
end
local OnClickButton = function(self,button)
	if button=="Deploy" then
		if CS.DeploymentTeamInfoController.currentSelectedTeamId>0 then
			if CS.GameData.currentSelectedMissionInfo.limitTeam ~= 0 and not CS.GameData.currentSelectedMissionInfo.basesquadCanTotalTeam then
				local count = CS.DeploymentController.Instance.PlayTeamsCount+CS.DeploymentController.Instance.SangvisTeamsCount;
				if count>= CS.GameData.currentSelectedMissionInfo.totalTeamLimitBase then
					CS.CommonController.LightMessageTips(CS.Data.GetLang(30083));
					return;
				end
			end	
		end
	end
	self:OnClickButton(button);
end	
util.hotfix_ex(CS.DeploymentTeamInfoController,'OnClickTeam',OnClickTeam)
util.hotfix_ex(CS.DeploymentTeamInfoController,'OnClickButton',OnClickButton)


