local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local InitPos = function(self)
	if CS.GameData.missionAction == nil then
		if not self:LoadStartMissionScale() then
			CS.DeploymentMapDragController.scale = CS.GameData.currentSelectedMissionInfo.originalmapScale;
			local deployspot = nil;
			local hpspot = nil;
			local teamspot = nil;
			for i=0,CS.DeploymentBackgroundController.currentLayerData.spots.Count-1 do
				local spot = CS.DeploymentBackgroundController.currentLayerData.spots[i];
				if spot.type == CS.SpotType.headQuarter and spot.belong == CS.Belong.friendly then
					hpspot = spot;
				end
				if teamspot == nil and spot:HasFriendlyTeam() then
					teamspot = spot;
				end
				if deployspot == nil and CS.DeploymentController.CanDeploy(spot) then
					deployspot = spot;
				end
			end
			local pos = CS.DeploymentBackgroundController.currentLayerData.offset;
			if hpspot ~= nil then
				pos = CS.UnityEngine.Vector2(hpspot.transform.localPosition.x,hpspot.transform.localPosition.y);
			elseif deployspot ~= nil then
				pos = CS.UnityEngine.Vector2(deployspot.transform.localPosition.x,deployspot.transform.localPosition.y);
			elseif teamspot ~= nil then
				pos = CS.UnityEngine.Vector2(teamspot.transform.localPosition.x,teamspot.transform.localPosition.y);
			end
			self:StartCameraFollow(pos);
			return;
		end
	end
	self:InitPos();
end

util.hotfix_ex(CS.DeploymentMapDragController,'InitPos',InitPos)