local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local InitCode = function(self,code)
	self:InitCode(code);
	if self.spineHolder ~= nil then
		local pos = self.spineHolder.transform.localPosition;
		self.spineHolder.transform.localPosition = CS.UnityEngine.Vector3(pos.x,pos.y,80);
	end
end
local OnClickButton = function(self,Button)
	if CS.CommonConfirmBoxControllerNew.hasOpen then
		return;
	end
	self:OnClickButton(Button);
end
local OnClickTeam = function(self,spot)
	if CS.CommonConfirmBoxControllerNew.hasOpen then
		return;
	end
	self:OnClickTeam(spot);
end
util.hotfix_ex(CS.DeploymentBuildingController,'InitCode',InitCode)
util.hotfix_ex(CS.DeploymentUIController,'OnClickButton',OnClickButton)
util.hotfix_ex(CS.DeploymentTeamInfoController,'OnClickTeam',OnClickTeam)