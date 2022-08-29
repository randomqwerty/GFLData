local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBackgroundController)
--修正下背景显示
local CheckSize = function(self)
	local mapsize = CS.DeploymentBackgroundController.currentLayerData.mapSize;
	local size = CS.Mathf.Max(mapsize.x,mapsize.y);
	self.cloudMaterial:SetFloat("_AddDistance",size*2);
end

util.hotfix_ex(CS.DeploymentBackgroundController,'CheckSize',CheckSize)




