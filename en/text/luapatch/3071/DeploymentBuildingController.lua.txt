local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local InitCode = function(self,code)
	self:InitCode(code);
	if self.spineHolder ~=nil then
		self.spineHolder.transform.localPosition = CS.UnityEngine.Vector3(self.spineHolder.transform.localPosition.x,self.spineHolder.transform.localPosition.y,81);
	end
end

util.hotfix_ex(CS.DeploymentBuildingController,'InitCode',InitCode)