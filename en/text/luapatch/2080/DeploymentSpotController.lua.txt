local util = require 'xlua.util'
local panelController = require("2080/DeploymentController")
xlua.private_accessible(CS.DeploymentSpotController)


local UpdateCurrentInformation = function(self)
	if self.maplistRoute.Count == 0 then
		return;
	end
	self:UpdateCurrentInformation();
end

local UpdateColor = function(self,targetBelong,play)
	local alpha = self.currentColor.a;
	self:UpdateColor(targetBelong,play);
	if self.currentColor.a ~= alpha then
		if self.spotAction ~= nil then
			self.spotAction.hasRouteChange = true;
		end
	end
end

local OnPointerUp = function(self,eventData)
	if CS.DeploymentController.playAniming then
		return;
	end
	self:OnPointerUp(eventData);
end

local PlayCaptureRecord = function(self,record,isLastRecord,play)
	CS.GameData.missionAction.spotid_TransBelongInfo:Remove(record.spotAction.spotInfo.id);
	self:PlayCaptureRecord(record,isLastRecord,play);
end

local OnFinishAnimationEvent = function(self)
	if playSpotTeamCapture == 1 then
		CS.DeploymentController.Instance:PlaySpotTeamCapture();
	elseif playSpotTeamCapture == 2 then
		CS.DeploymentController.Instance:PlaySpotSurroundCapture();
	end
end

local Initialize = function(self)
	if self.spotAction == nil then
		if self.spotInfo.type == CS.SpotType.LimitedSupply and self.spotInfo.supplyTime == 0 then
			self.type = CS.SpotType.CA;
		end
	end
	self:Initialize();
end  
util.hotfix_ex(CS.DeploymentSpotController,'UpdateCurrentInformation',UpdateCurrentInformation)
util.hotfix_ex(CS.DeploymentSpotController,'UpdateColor',UpdateColor)
util.hotfix_ex(CS.DeploymentSpotController,'OnPointerUp',OnPointerUp)
util.hotfix_ex(CS.DeploymentSpotController,'PlayCaptureRecord',PlayCaptureRecord)
util.hotfix_ex(CS.DeploymentSpotController,'OnFinishAnimationEvent',OnFinishAnimationEvent)
util.hotfix_ex(CS.DeploymentSpotController,'Initialize',Initialize)
