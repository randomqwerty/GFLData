local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleComponentTipContent)

local SetSkillInfo_New = function(com)
    local inst = CS.VehicleComponentTipContent._inst
	inst.objSkill:SetActive(false)

	local vehicleSkill = com.componentMainSkill
	if vehicleSkill == nil then
		return
	end
    
	if vehicleSkill.currentSkillType == CS.VehicleSkillType.battleSkill then     
     
        local BSkill = vehicleSkill:battleSkillCfg();
        if BSkill ~= nil then                
            inst.txtSkillName.text = BSkill.name;
            inst.txtSkillContent.text = BSkill.description;
            local objIcon = CS.CommonController.InstantiateSkillIcon(BSkill.code);
            objIcon.transform:SetParent(inst.iconHolder, false);
            inst.objSkill:SetActive(true);  
        end
    else  

        local MSkill = vehicleSkill:missionSkillCfg();
        if MSkill ~= nil then        
            inst.txtSkillName.text = MSkill.name;
            inst.txtSkillContent.text = MSkill.description;          
            local objIcon = CS.CommonController.InstantiateSkillIcon(MSkill.code);
            objIcon.transform:SetParent(inst.iconHolder, false);
            inst.objSkill:SetActive(true);                
        end            
    end	
end


util.hotfix_ex(CS.VehicleComponentTipContent,'SetSkillInfo',SetSkillInfo_New)

