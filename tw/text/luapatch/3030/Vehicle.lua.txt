local util = require 'xlua.util'
xlua.private_accessible(CS.Vehicle)

local _GetComponentEffectPoint = function(self)
	local spScore = 0;
	local comScore = 0;
	
	local rankEffectList = self:AnalysisRankEffect();
	for k,v in pairs(self.dictComponent) do
		if v ~= nil then
			local componentScore = 0;
			local basicEffectList = self:AnalysisBasicEffect(v);
			local vceArray = Split(CS.Data.GetString("vehicle_component_exp"),',')
			local maxLv = #vceArray;
			local strengthenEffect = CS.Data.GetInt("vehicle_component_strengthen_effect");
			local afficUnLockCount = CS.Data.GetVehicleComponentUnLockAffixCount(v);
			local basicEffectScore = 0;
			for i=1,afficUnLockCount do
				if i < basicEffectList.Count then
					basicEffectScore = basicEffectScore + basicEffectList[i];
				end
			end
			
			if v.info ~= nil then
				componentScore = basicEffectList[0] * rankEffectList[v.info.rank - 1] * (1 + (v.level / tonumber(maxLv)) * (strengthenEffect / 100.0)) + basicEffectScore;
			end
			
			if k > 5 then
				comScore = comScore + CS.Mathf.FloorToInt(componentScore);
			else
				spScore = spScore + CS.Mathf.FloorToInt(componentScore);
			end
		end
	end
	
	return CS.Mathf.FloorToInt(((spScore * 1.0) / (self.vehicleInfo.SpComponentMaxNum * 1.0)))
	+ CS.Mathf.FloorToInt(((comScore * 1.0) / (self.vehicleInfo.CommonComponentMaxNum * 1.0)));
end


util.hotfix_ex(CS.Vehicle,'GetComponentEffectPoint',_GetComponentEffectPoint)