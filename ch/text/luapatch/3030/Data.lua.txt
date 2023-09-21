local util = require 'xlua.util'
xlua.private_accessible(CS.Data)

local GetComponentPropertyName_New = function(typeName)
    local attrName = CS.Data.GetComponentPropertyName(typeName)

    if typeName == "H_armor_piercing" then
        attrName = CS.Data.GetLang(1808);
    end

    if typeName == "L_armor_piercing" then
        attrName = CS.Data.GetLang(1809);
    end

    if typeName == "atk_speed" then
        attrName = CS.Data.GetLang(160016);
    end

    return attrName
end


util.hotfix_ex(CS.Data,'GetComponentPropertyName',GetComponentPropertyName_New)

