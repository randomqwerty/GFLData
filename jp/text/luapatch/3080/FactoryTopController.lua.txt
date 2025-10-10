local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryTopController)
xlua.private_accessible(CS.DevelopEquipmentController)

local RefreshResource = function(self)
	self:RefreshResource();
	if CS.FactoryFairyBuildController.Instance ~= nil and not CS.FactoryFairyBuildController.Instance:isNull() then
		CS.FactoryFairyBuildController.Instance.textEquipCore.text = tostring(CS.GameData.userInfo.core);
	end
	if CS.DevelopEquipmentController.inst ~= nil and not CS.DevelopEquipmentController.inst:isNull() then
		CS.DevelopEquipmentController.inst.textEquipCore.text = tostring(CS.GameData.userInfo.core);
	end
end


util.hotfix_ex(CS.FactoryTopController,'RefreshResource',RefreshResource)

