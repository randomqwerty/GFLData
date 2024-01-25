local util = require 'xlua.util'
xlua.private_accessible(CS.AdjutantGunListController)

local mGunFilter2 = function(self,afInfo)        
    if afInfo.skinInfo == nil then
        afInfo.skinInfo=CS.GameData.listSkinInfo:GetDataByIndex(0);
        local result = self:GunFilter(afInfo);
        afInfo.skinInfo=nil;
        return result;
    else
        return self:GunFilter(afInfo);  
    end        
end

util.hotfix_ex(CS.AdjutantGunListController,'GunFilter',mGunFilter2)
