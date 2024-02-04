local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local InitShowContainer = function(self)
	self:InitShowContainer();
	if CS.OPSPanelBackGround.currentContainerId == 0 then
		if CS.OPSPanelBackGround.Instance.opsMissionContainers.Count == 0 then
			if self.firstCamerapanelmission == nil and self:CanPlayAllSpots() then
				if CS.OPSPanelController.loginTime:ContainsKey(self.campaionId) and CS.OPSPanelController.loginTime[self.campaionId] == CS.GameData.loginServerTime then
					if not CS.OPSPanelBackGround.Instance:ReadRecord() then
						self:CheckSpineSpot();
						self:ReturnContainerPos();
					end
				end
			end
		end
	end
end

local CanPlayAllSpots = function(self)
	if self.playHolders.Count>0 or self.playSpots.Count > 0 then
		return false;
	end
	return self:CanPlayAllSpots();
end

local Load = function(self,campaion)
	self:Load(campaion);
	if self.currentPanelConfig ~= nil and self.currentPanelConfig.highScoreInfo ~= nil then
		if self.currentPanelConfig.highScoreInfo.opsmission ~= nil and self.currentPanelConfig.highScoreInfo.opsmission.CurrentMissionId == 0 then
			self.currentPanelConfig.highScoreInfo.opsmission = nil;
		end
	end
end
util.hotfix_ex(CS.OPSPanelController,'InitShowContainer',InitShowContainer)
util.hotfix_ex(CS.OPSPanelController,'CanPlayAllSpots',CanPlayAllSpots)
util.hotfix_ex(CS.OPSPanelController,'Load',Load)
