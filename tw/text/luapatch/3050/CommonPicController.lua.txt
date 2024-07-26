local util = require 'xlua.util'
xlua.private_accessible(CS.CommonPicController)

local GetCurrentPosData = function(self,sceneName,fatherName,rootName)
	if fatherName == "GetKCCO(Clone)" then
		return self:GetCurrentPosData("SangvisGasha",fatherName,"Img_BossPic/AnimaNode/Canvas/GetKCCO(Clone)/");
	end
	if fatherName == "GetParadeus(Clone)" then
		return self:GetCurrentPosData("SangvisGasha",fatherName,"Img_BossPic/AnimaNode/Canvas/GetParadeus(Clone)/");
	end
	if fatherName == "GetSangvis(Clone)" then
		return self:GetCurrentPosData("SangvisGasha",fatherName,"Img_BossPic/AnimaNode/Canvas/GetSangvis(Clone)/");
	end
	if fatherName == "GetOther(Clone)" then
		return self:GetCurrentPosData("SangvisGasha",fatherName,"Img_BossPic/AnimaNode/Canvas/GetOther(Clone)/");
	end
	return self:GetCurrentPosData(sceneName,fatherName,rootName);
end

util.hotfix_ex(CS.CommonPicController,'GetCurrentPosData',GetCurrentPosData)