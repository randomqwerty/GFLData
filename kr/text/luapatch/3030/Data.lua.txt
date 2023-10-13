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

local GetComponentAffixName_New = function(bounsType)
    local attrName = CS.Data.GetComponentAffixName(bounsType)

    if bounsType == CS.VehicleAttrType.heavyArmorPierce then
        attrName = CS.Data.GetLang(1808);
    end

    if bounsType == CS.VehicleAttrType.lightArmorPierce then
        attrName = CS.Data.GetLang(1809);
    end

    if bounsType == CS.VehicleAttrType.atkSpeed then
        attrName = CS.Data.GetLang(160016);
    end

    return attrName
end

local mInitForbidWords = function()
    CS.GameData.listForbidWordChar = CS.System.Collections.Generic.List(CS.System.String)();

    local textAsset = CS.ResManager.GetObjectByPath("TextData/ForbidWords/words_normal", ".txt");
    if textAsset == nil then
        return;
    end
    local lineTxt = Split(textAsset.text,"\r\n");
    for i = 0, #lineTxt do
        if not CS.System.String.IsNullOrEmpty(lineTxt[i]) then
            CS.GameData.listForbidWordChar:Add(lineTxt[i]);
        end
    end
    textAsset=nil;
    --local num = CS.GameData.listForbidWordChar.Count;
    --print("words_normal exist"..num);
end
function Split(szFullString, szSeparator)
    local nFindStartIndex = 1
    local nSplitIndex = 1
    local nSplitArray = {}
    while true do
        local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
        if not nFindLastIndex then
            nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
            break
        end
        nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
        nFindStartIndex = nFindLastIndex + string.len(szSeparator)
        nSplitIndex = nSplitIndex + 1
    end
    return nSplitArray
end
util.hotfix_ex(CS.Data,'GetComponentPropertyName',GetComponentPropertyName_New)
util.hotfix_ex(CS.Data,'GetComponentAffixName',GetComponentAffixName_New)

if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then 
    util.hotfix_ex(CS.Data,'InitForbidWords',mInitForbidWords)
end
