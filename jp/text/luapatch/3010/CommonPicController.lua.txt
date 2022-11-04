local util = require 'xlua.util'
xlua.private_accessible(CS.CommonPicController)
local CheckPath = function(self,path)
	if path == "PicHolder/TheaterCombatSettlement(Clone)/" then
		return "Pic/Result_New(Clone)/Canvas/BattleController/";
	end
	return self:CheckPath(path);
end
util.hotfix_ex(CS.CommonPicController,'CheckPath',CheckPath)