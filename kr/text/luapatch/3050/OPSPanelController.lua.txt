local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local ReturnContainerPos = function(self)
	if CS.OPSPanelBackGround.currentContainerId ~= 0 then
		for i=0,CS.OPSPanelBackGround.Instance.opsMissionContainers.Count-1 do
			local container = CS.OPSPanelBackGround.Instance.opsMissionContainers[i];
			if container.id == CS.OPSPanelBackGround.currentContainerId then
				local pos = container.transform.localPosition;
				CS.OPSPanelBackGround.Instance:Move(CS.UnityEngine.Vector2(pos.x,pos.y),false);
			end
		end
	else
		local holderShow = nil;
		for i=0,CS.OPSPanelBackGround.Instance.spotMissionHolders.Count-1 do
			local holder = CS.OPSPanelBackGround.Instance.spotMissionHolders[i];
			if holderShow == nil and holder.CanShow then
				holderShow = holder;
				local pos = holder.transform.localPosition;
				CS.OPSPanelBackGround.Instance:Move(CS.UnityEngine.Vector2(pos.x,pos.y),false);
			end
		end
	end
	CS.OPSPanelBackGround.Instance:SaveRecord();
end

local CanChooseDrag = function(self)
	if self.campaionId == -69 then
		return false;
	end
	if self.currentChoose ~= nil then
		return false;
	end
	return true;
end

local MoveSelectDiskMission = function(self,missionholder)
	self:CancelMission();
	local index = self.currentPanelConfig.oPSDiskMissions:IndexOf(missionholder.opsDiskMission);
	self:MoveToDiskMission(missionholder.opsDiskMission,0.5,function()		
		self:SeletDiskMission(index);
	end)
end
util.hotfix_ex(CS.OPSPanelController,'ReturnContainerPos',ReturnContainerPos)
util.hotfix_ex(CS.OPSPanelController,'CanChooseDrag',CanChooseDrag)
--util.hotfix_ex(CS.OPSPanelController,'MoveToDiskMission',MoveToDiskMission)
util.hotfix_ex(CS.OPSPanelController,'MoveSelectDiskMission',MoveSelectDiskMission)
