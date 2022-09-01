local util = require 'xlua.util'
xlua.private_accessible(CS.DormExplorationFormationController)

local _OnRequestExploreGetAdaptiveTeam = function(self,request)
	self:OnRequestExploreGetAdaptiveTeam(request);
	self:RefreshAdaptivePanel(); 
	self:RefreshTimeTypeItems();
	self.exploreBtns:RefreshUIState();
end
local _Start = function(self)
	self:Start();
	if CS.GameData.explorationAdaptiveConfig == nil or CS.GameData.GetCurrentTimeStamp() > CS.GameData.explorationAdaptiveConfig.endTime then
	else
		self:RefreshAdaptivePanel();
		self:RefreshTimeTypeItems();
		self.exploreBtns:RefreshUIState();
	end
end

util.hotfix_ex(CS.DormExplorationFormationController,'OnRequestExploreGetAdaptiveTeam',_OnRequestExploreGetAdaptiveTeam)
util.hotfix_ex(CS.DormExplorationFormationController,'Start',_Start)
