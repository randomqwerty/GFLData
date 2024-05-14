local util = require 'xlua.util'
xlua.private_accessible(CS.CommonBundleConfirmBoxController)

local OnClickSkinDetail = function(self)        
    self:OnClickSkinDetail();
	if self.SkinDisplayBackground.transform.childCount >0 then
		local pic = self.SkinDisplayBackground.transform:GetChild(0).gameObject:GetComponent(typeof(CS.CommonPicController));
		pic:SwitchDamaged(false);
	end
end

local Init_New = function(self, mallGood, pack)        
    self:Init(mallGood, pack);

    local showPrompt = false
	if mallGood ~= nil then
		local find = false
        local result, gunId, skinId, skinClassTheme = CS.Data.GetMallGoodSkinInfo(mallGood, 0, 0, 0);

        for i = 0,CS.GameData.listGun.Count-1  do
        	if CS.GameData.listGun[i].info.id == gunId 
        		or (CS.GameData.listGun[i].info.isMindupdate and CS.GameData.listGun[i].info.gunInfoOtherMod.id == gunId) then
        		find = true
        		break
        	end
        end
        showPrompt = not find
	end
	self.objPrompt:SetActive(showPrompt)
end

util.hotfix_ex(CS.CommonBundleConfirmBoxController,'OnClickSkinDetail',OnClickSkinDetail)
util.hotfix_ex(CS.CommonBundleConfirmBoxController,'Init',Init_New)

