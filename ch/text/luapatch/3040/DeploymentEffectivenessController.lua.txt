local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEffectivenessController)
local mGotoStoreRoomSquad = function(self)

	if CS.Utility.loadedLevelName ~= "StoreRoom" then
		CS.CommonSceneManagerController.instance:Clear();
	end
    self:GotoStoreRoomSquad();
end
local mGotoStroeRoomVehicle = function(self)
	if CS.Utility.loadedLevelName ~= "StoreRoom" then
		CS.CommonSceneManagerController.instance:Clear();
	end
    self:GotoStroeRoomVehicle();
end
util.hotfix_ex(CS.DeploymentEffectivenessController,'GotoStoreRoomSquad',mGotoStoreRoomSquad)
util.hotfix_ex(CS.DeploymentEffectivenessController,'GotoStroeRoomVehicle',mGotoStroeRoomVehicle)
