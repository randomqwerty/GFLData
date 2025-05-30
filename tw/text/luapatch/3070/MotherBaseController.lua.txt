local util = require 'xlua.util'
xlua.private_accessible(CS.MotherBaseController)

local CheckOnClickObj = function(self,obj)
	if CS.OrganizationMapController.Instance ~= nil and not CS.OrganizationMapController.Instance:isNull() then
		return;
	end
	self:CheckOnClickObj(obj);
end


util.hotfix_ex(CS.MotherBaseController,'CheckOnClickObj',CheckOnClickObj)
