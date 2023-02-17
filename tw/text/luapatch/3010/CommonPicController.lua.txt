local util = require 'xlua.util'
xlua.private_accessible(CS.CommonPicController)
local CheckPath = function(self,path)
	if path == "PicHolder/TheaterCombatSettlement(Clone)/" then
		return "Pic/Result_New(Clone)/Canvas/BattleController/";
	end
	return self:CheckPath(path);
end

local GetCurrentPosData = function(self,sceneName,fatherName,rootName)
	if fatherName == "SkinShow(Clone)" then
		return self:GetCurrentPosData("Mall",fatherName,rootName);
	end
	return self:GetCurrentPosData(sceneName,fatherName,rootName);
end
util.hotfix_ex(CS.CommonPicController,'CheckPath',CheckPath)
util.hotfix_ex(CS.CommonPicController,'GetCurrentPosData',GetCurrentPosData)