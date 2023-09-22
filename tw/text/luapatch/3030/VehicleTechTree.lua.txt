local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleTechTreeNodeInfo)

local _GetUnitAttrLanguage = function(self,type)
	if type == CS.VehicleAttrType.atkSpeed then
		return CS.Data.GetLang(30385)
	end
	return self:GetUnitAttrLanguage(type);
end


util.hotfix_ex(CS.VehicleTechTreeNodeInfo,'GetUnitAttrLanguage',_GetUnitAttrLanguage)