local util = require 'xlua.util'
xlua.private_accessible(CS.GameData)
local PlayBgm = function()
	--露尼西亚战斗中avg结束时不重置bgm
	if CS.GameData.currentSelectedMissionInfo ~= nil and CS.GameData.currentSelectedMissionInfo.campaign == -78 and CS.Utility.loadedLevelName == "Battle" then
		local spot = CS.GameData.engagedSpot
		if spot ~= nil and spot.spotInfo.id == 89490 then
			return
		end
	end
	CS.DeploymentController.PlayBgm()
end

 
local BuildCastSkillOnDeathHandler = function(self,data)
	self.playBuildAnim = false;
	local move = false;
	for i=0,data.builddatas.Count-1 do
		if data.builddatas[i].cameramove and not move then
			move = true;
			local pos = data.builddatas[i].buildAction.buildController.spot.transform.localPosition;
			CS.DeploymentController.TriggerMoveCameraEvent(CS.UnityEngine.Vector2(pos.x,pos.y),true);
		end
	end
	if CS.GameData.AnalysisMissionResult(data.jsonData, true) then
	elseif CS.GameData.AnalysisMissionResult(data.jsonData, false) then
	end
	self:InsertSomePlayPerformances(function()
		self:AddAllCanPlayPerformanceLayer();
	end);
	if self:HasTeamCanTrans() then
		CS.DeploymentController.hasTeamTraning = true;
		self:InsertSomePlayPerformances(function()
				self:CheckTeamTrans();
			end,true);
	end
	self:AddAndPlayPerformance(function()
		self:CheckBattle();
	end);
	self:PlayNext();
	CS.DeploymentController.TriggerRefreshUIEvent();
end
util.hotfix_ex(CS.DeploymentController,'PlayBgm',PlayBgm)
util.hotfix_ex(CS.DeploymentController,'BuildCastSkillOnDeathHandler',BuildCastSkillOnDeathHandler)
