local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionContainer)

local ShowClock = function(self)
	if self.clockinfo ~= nil then
		for i=0,self.clockinfo.missionIds.Count-1 do
			for j=0,self.clockinfo.missionIds[i].Count-1 do
				local missionId = self.clockinfo.missionIds[i][j];
				local mission = CS.GameData.listMission:GetDataById(missionId);
				if mission ~= nil then
					return false;
				end
			end
		end
		if CS.OPSPanelController.Instance.campaionId == -48 then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(60285));
		end
		return true;
	end
	if self.unclockTime == 0 then
		for i=0,CS.OPSPanelBackGround.Instance.spotMissionHolders.Count-1 do
			local holder = CS.OPSPanelBackGround.Instance.spotMissionHolders[i];
			if holder.containerId == self.id then
				if holder.missionIds.Length > 0 then
					local missionId = holder.missionIds[CS.OPSPanelController.difficulty];
					local mission = CS.GameData.listMission:GetDataById(missionId);
					if mission ~= nil then
						return false;
					end
				end
			end
		end
		if CS.OPSPanelController.Instance.campaionId == -48 then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(60285));
		end
		return true;
	end
	if CS.OPSPanelController.InWaiteList then
		return  false;
	end
	return CS.GameData.GetCurrentTimeStamp() < self.unclockTime;
end

local RefreshClockUI = function(self)
	self:RefreshClockUI();
	if self.txtProcessTrans ~= nil then
		local clock = self.txtProcessTrans.parent:Find("Img_Lock");
		if clock ~= nil then
			for i=0,self.clockinfo.missionIds.Count-1 do
				for j=0,self.clockinfo.missionIds[i].Count-1 do
					local missionId = self.clockinfo.missionIds[i][j];
					local mission = CS.GameData.listMission:GetDataById(missionId);
					if mission ~= nil then
						clock.gameObject:SetActive(false);
						return;
					end
				end
			end
			clock.gameObject:SetActive(true);
		end
	end	
end

local UnClock = function(self)
	if CS.OPSPanelController.Instance.currentPanelConfig.ContainerClockInfos:ContainsKey(self.id) then
		return true;
	end
	for i=0,CS.OPSPanelBackGround.Instance.spotMissionHolders.Count-1 do
		local holder = CS.OPSPanelBackGround.Instance.spotMissionHolders[i];
		if holder.containerId == self.id then
			if holder.missionIds.Length > 0 then
				local missionId = holder.missionIds[CS.OPSPanelController.difficulty];
				local mission = CS.GameData.listMission:GetDataById(missionId);
				if mission ~= nil then
					return true;
				end
			end
		end
	end
	return false;
end

local Awake = function(self)
	self:Awake();
	self.canSelect = true;
end
util.hotfix_ex(CS.OPSPanelMissionContainer,'Awake',Awake)
util.hotfix_ex(CS.OPSPanelMissionContainer,'ShowClock',ShowClock)
util.hotfix_ex(CS.OPSPanelMissionContainer,'UnClock',UnClock)
util.hotfix_ex(CS.OPSPanelMissionContainer,'RefreshClockUI',RefreshClockUI)


