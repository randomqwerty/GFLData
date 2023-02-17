local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)
--修正lanbel显示刷新
local Awake = function(self)
	self:Awake();
	for i=0,self.listCharacterInfoController.Count-1 do
		local label = self.listCharacterInfoController[i];
		label:Awake();
	end
end
local RequestReinforceHandle = function(self,data)
	self:RequestReinforceHandle(data);
	CS.DeploymentController.TriggerPlayPerformanceEndEvent(nil);
end
local RqquestAllyReinforceHandle = function(self,data)
	self:RqquestAllyReinforceHandle(data);
	CS.DeploymentController.TriggerPlayPerformanceEndEvent(nil);
end
local RequestSangvisTeamReinforceHandle = function(self,data)
	self:RequestSangvisTeamReinforceHandle(data);
	CS.DeploymentController.TriggerPlayPerformanceEndEvent(nil);
end
util.hotfix_ex(CS.DeploymentTeamInfoController,'Awake',Awake)
util.hotfix_ex(CS.DeploymentTeamInfoController,'RequestReinforceHandle',RequestReinforceHandle)
util.hotfix_ex(CS.DeploymentTeamInfoController,'RqquestAllyReinforceHandle',RqquestAllyReinforceHandle)
util.hotfix_ex(CS.DeploymentTeamInfoController,'RequestSangvisTeamReinforceHandle',RequestSangvisTeamReinforceHandle)