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

util.hotfix_ex(CS.DeploymentTeamInfoController,'Awake',Awake)
