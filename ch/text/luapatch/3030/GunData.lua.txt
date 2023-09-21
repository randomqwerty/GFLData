local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BaseTeam)

local Condition3_AllEquipFullReinforce = function(self)
	if self.listGun.Count == 0 then
		return false;
	end
	for i=0,self.listGun.Count-1 do
		if self.listGun[i].equipList.Count < 3 then
			return false;
		end
		for j=0,self.listGun[i].equipList.Count-1 do
			local equip = self.listGun[i].equipList[j];
			if equip.info.max_level ~= 0 then
				if equip.equip_level < CS.Data.GetInt("equip_lv_limit") then
					return false;
				end
			end
		end
	end
	return true;
end

local ConditionBase_AllEquipLevel = function(self,level)
	if self.listGun.Count == 0 then
		return false;
	end
	for i=0,self.listGun.Count-1 do
		if self.listGun[i].equipList.Count < 3 then
			return false;
		end
		for j=0,self.listGun[i].equipList.Count-1 do
			local equip = self.listGun[i].equipList[j];
			if equip.info.max_level ~= 0 then
				if equip.equip_level < level then
					return false;
				end
			end
		end
	end
	return true;
end
util.hotfix_ex(CS.GF.Battle.BaseTeam,'Condition3_AllEquipFullReinforce',Condition3_AllEquipFullReinforce)
util.hotfix_ex(CS.GF.Battle.BaseTeam,'ConditionBase_AllEquipLevel',ConditionBase_AllEquipLevel)
