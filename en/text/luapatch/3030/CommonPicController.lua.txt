local util = require 'xlua.util'
xlua.private_accessible(CS.CommonPicController)

local GetCurrentPosData = function(self,sceneName,fatherName,rootName)
	if fatherName == "SkinDisplayGiftUI(Clone)" then
		return self:GetCurrentPosData("Dorm",fatherName,"SkinPreviewHolder/SkinDisplayGiftUI(Clone)/");
	end
	if rootName == "SkinHolder/Skin/Pass(Clone)/Canvas/" then
		return self:GetCurrentPosData("Home",fatherName,rootName);
	end
	return self:GetCurrentPosData(sceneName,fatherName,rootName);
end

util.hotfix_ex(CS.CommonPicController,'GetCurrentPosData',GetCurrentPosData)