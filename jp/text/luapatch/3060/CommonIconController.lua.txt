local util = require 'xlua.util'
xlua.private_accessible(CS.CommonIconController.CommonIconControllerBuilder)
xlua.private_accessible(CS.CommonPictureFileController)
local SetSangvisGun = function(self,sangvisGunInfo)
	if sangvisGunInfo ~= nil then
		self:AddOrSetValue("introduction", CS.System.String.Format(CS.Data.GetLang(260162), sangvisGunInfo.name))
	end
	return self:SetSangvisGun(sangvisGunInfo)
end

local GetSpriteToleranceByCode = function(self,code)
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local obj = CS.ResManager.GetObjectByPath("ImgTolerance/"..code,".jpg");
		if obj == nil then
			obj = CS.UnityEngine.Texture2D(1,1);
			obj:SetPixel(0, 0, CS.UnityEngine.Color.black);
			obj:Apply(false);
		end
		return obj;
	else
		return self:GetSpriteToleranceByCode(code);
	end
end
util.hotfix_ex(CS.CommonIconController.CommonIconControllerBuilder,'SetSangvisGun',SetSangvisGun)
util.hotfix_ex(CS.CommonPictureFileController,'GetSpriteToleranceByCode',GetSpriteToleranceByCode)

