local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionOperationTeamInfoController)
xlua.private_accessible(CS.CommonSceneManagerController)
local _JumpToFormation = function(self)
	if CS.CommonSceneManagerController.instance.currentSceneName == "Battle" and self.BDTTSC~=nil and self.BDTTSC.gameObject.activeSelf then
		--print("defence trial");
		return;
	else
		self:JumpToFormation();
	end
end
local myOnlyJumpFormation = function(self)
	if CS.CommonSceneManagerController.instance.currentSceneName == "Battle" then
		CS.CommonSceneManagerController.instance:Clear();
	end
	self:OnlyJumpFormation()
end
util.hotfix_ex(CS.MissionSelectionOperationTeamInfoController,'JumpToFormation',_JumpToFormation)
util.hotfix_ex(CS.MissionSelectionOperationTeamInfoController,'OnlyJumpFormation',myOnlyJumpFormation)