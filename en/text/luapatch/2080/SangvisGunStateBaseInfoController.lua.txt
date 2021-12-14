local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGunStateBaseInfoController)

local _MarryPerformance = function(self)
	self:MarryPerformance();
	if CS.UISimulatorFormation.Instance ~= nil then
		CS.UISimulatorFormation.Instance.gameObject:SetActive(false); 
	end 
end

util.hotfix_ex(CS.SangvisGunStateBaseInfoController,'MarryPerformance',_MarryPerformance)



