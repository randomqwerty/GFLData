local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.OPSPanelBackGround)
xlua.private_accessible(CS.OPSPanelSpot)
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
	if self.campaionId == -69 or self.campaionId == -70 then
		return false;
	end
	if self.currentChoose ~= nil then
		return false;
	end
	return true;
end

local ShowProcessAllMission = function(self)
	local choose = self.currentChoose;
	local spot = self.chooseSpot;
	self.currentChoose = nil;
	self.chooseSpot = nil;
	self:ShowProcessAllMission();
	self.currentChoose = choose;
	self.chooseSpot = spot;
end

local MoveSelectDiskMission = function(self,missionholder)
	self:CancelMission();
	local index = self.currentPanelConfig.oPSDiskMissions:IndexOf(missionholder.opsDiskMission);
	self:MoveToDiskMission(missionholder.opsDiskMission,0.5,function()		
		self:SeletDiskMission(index);
	end)
end
local MoveSpine = function(self,spot)
	if self.lastSpot ~= nil then
		local select = self.lastSpot.transform:Find("Img_Selected");
		if select~= nil then
			select.gameObject:SetActive(false);
		end
	end
	self:MoveSpine(spot);
	if self.chooseSpot ~= nil then
		local select = self.chooseSpot.transform:Find("Img_Selected");
		if select~= nil then
			select.gameObject:SetActive(true);
		end
	end
end
local CancelMission = function(self)
	if self.chooseSpot ~= nil then
		local select = self.chooseSpot.transform:Find("Img_Selected");
		if select~= nil then
			select.gameObject:SetActive(false);
		end
	end
	self:CancelMission();
end
local newUIObj;

local CheckNewsPos = function(self)
	self:CheckNewsPos();
	if CS.OPSPanelController.Instance.campaionId == -71 then
		if newUIObj == nil or newUIObj:isNull() then
			newUIObj = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/202408Activity_NewTips"), CS.OPSPanelController.Instance.leftMain, false);
		end
		local showleft = false;
		local showright = false;
		local showup = false;
		local showdown = false;
		for i=0,self.all3dSpots.Count-1 do
			local spot = self.all3dSpots:GetDataByIndex(i);
			if spot.CanShow and spot.mission ~= nil and spot.mission.showNewTag then
				local wtvPos = self.mainCamera:WorldToViewportPoint(spot.transform.position);
				if wtvPos.x<0 then
					showleft = true;
				end
				if wtvPos.x>1 then
					showright = true;
				end
				if wtvPos.y<0 then
					showdown = true;
				end
				if wtvPos.y>1 then
					showup = true;
				end
			end
		end
		newUIObj.transform:Find("Left").gameObject:SetActive(showleft);
		newUIObj.transform:Find("Right").gameObject:SetActive(showright);
		newUIObj.transform:Find("Bottom").gameObject:SetActive(showdown);
		newUIObj.transform:Find("Top").gameObject:SetActive(showup);
	end
end
local ShowNewTag = function(self)
	self:ShowNewTag();
	local newTag = self.transform:Find("New");
	if newTag ~= nil then
		if self.mission ~= nil and self.mission.showNewTag then
			newTag.gameObject:SetActive(true);
		else
			newTag.gameObject:SetActive(false);
		end
	end
end
local CheckIsolateSpots = function(self)
	self:CheckIsolateSpots();
	for i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
		local spot = CS.OPSPanelBackGround.Instance.all3dSpots:GetDataByIndex(i);
		if spot.holder == nil then
			spot:Show();
		end
	end
end
local Init = function(self)
	self.difficulty = self.info.difficulty;
	self:Init();
end

local Show = function(self,play,delay)
	if not self.CanShow then
		--CS.NDebug.Log("HideSpot",self.index);
		self.gameObject:SetActive(false);
		return;
	end
	self:Show(play,delay);
end
util.hotfix_ex(CS.OPSPanelController,'ReturnContainerPos',ReturnContainerPos)
util.hotfix_ex(CS.OPSPanelController,'CanChooseDrag',CanChooseDrag)
util.hotfix_ex(CS.OPSPanelController,'ShowProcessAllMission',ShowProcessAllMission)
util.hotfix_ex(CS.OPSPanelController,'MoveSelectDiskMission',MoveSelectDiskMission)
util.hotfix_ex(CS.OPSPanelController,'MoveSpine',MoveSpine)
util.hotfix_ex(CS.OPSPanelController,'CancelMission',CancelMission)
util.hotfix_ex(CS.OPSPanelController,'CheckIsolateSpots',CheckIsolateSpots)
util.hotfix_ex(CS.OPSPanelBackGround,'CheckNewsPos',CheckNewsPos)
util.hotfix_ex(CS.OPSPanelSpot,'ShowNewTag',ShowNewTag)
util.hotfix_ex(CS.OPSPanelSpot,'Init',Init)
util.hotfix_ex(CS.OPSPanelSpot,'Show',Show)

