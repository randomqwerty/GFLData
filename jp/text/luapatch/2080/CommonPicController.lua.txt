local util = require 'xlua.util'
xlua.private_accessible(CS.CommonPicController)

local GetCurrentPosData = function(self,sceneName,fatherName,rootName)
	if rootName == "PicHolder/TheaterMissiontSettlement(Clone)/Canvas/BattleController/" then
		rootName = "Pic/Result_New(Clone)/Canvas/BattleController/";
	end
	for i=0,self.posData.Count-1 do
		local data = self.posData[i];
		if data.path == "SkinHolder/Left/SkinDisplay(Clone)/CommodityHolder/SafeRect/Canvas/" then
			data.path = "SkinHolder/Left/SkinDisplay(Clone)/CommodityHolder/SafeRact/Canvas/";
		end
	end
	return self:GetCurrentPosData(sceneName,fatherName,rootName);
end

util.hotfix_ex(CS.CommonPicController,'GetCurrentPosData',GetCurrentPosData)


