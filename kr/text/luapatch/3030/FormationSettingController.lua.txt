local util = require 'xlua.util'
xlua.private_accessible(CS.FormationSettingController)
local Init = function(self,teamId,hideTeamTitle,needUseOriginPos)
	self.mainCamera = CS.UnityEngine.Camera.main;
	self:Init(teamId,hideTeamTitle,needUseOriginPos);
end

util.hotfix_ex(CS.FormationSettingController,'Init',Init)