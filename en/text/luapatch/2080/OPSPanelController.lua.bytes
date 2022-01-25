local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.ImageRotateControl)
xlua.private_accessible(CS.OPSPanelBackGround)

angleDragmax = 0;
angleDragmin = 0;
missionIdrecord = 0;
local selectDiffcluty = false;
local selectTemp = false;
local SelectDiffcluty = function(self)
	selectDiffcluty = true;
	self:SelectDiffcluty();
	selectDiffcluty = false;
end

local CheckSpineMove = function(self)
	self:CheckSpineMove();
	if self.moveSpots.Count == 0 then
		if self.clockSelectRing ~= nil and not self.clockSelectRing:isNull() then
			--local canvasgroup = self.clockSelectRing:GetComponent(typeof(CS.UnityEngine.CanvasGroup))
			--if canvasgroup.alpha == 1 then
			--	CS.OPSPanelBackGround.Instance.CanClick = false;
			--end
			local control = self.clockSelectRing.transform:Find("Ring"):GetComponent(typeof(CS.ImageRotateControl));
			control.checkSelectValue = true;
			--CS.OPSPanelBackGround.Instance:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = true;
			print("check");
		end	
	end	
end

local CheckContainerAngle = function(self)
	local lastAngle = 0;
	if CS.OPSPanelBackGround.currentContainerId ~= 0 then
		if CS.OPSPanelBackGround.Instance.container ~= nil and CS.OPSPanelBackGround.Instance.container.id == CS.OPSPanelBackGround.currentContainerId then
			lastAngle = CS.OPSPanelBackGround.Instance.container.rotateControl.angle;
		end
	end
	self:CheckContainerAngle();
	if CS.OPSPanelBackGround.currentContainerId ~= 0 then
		if CS.OPSPanelBackGround.Instance.container ~= nil and CS.OPSPanelBackGround.Instance.container.id == CS.OPSPanelBackGround.currentContainerId then
			CS.OPSPanelBackGround.Instance.container.rotateControl.angle = lastAngle;
		end
	end
end

local Start = function(self)
	self:Start();
	self.startAngle = -10;
	missionIdrecord = 0;
end

local StopUI = function()
	CS.CommonAudioController.PlayUI("Stop_UI_loop");
	CS.OPSPanelBackGround.Instance.CanClick = true;
end

local PlayTime = function(self,play,forward,hour,min,duration)
	self:PlayTime(play,forward,hour,min,duration);
	if play and duration>0 then
		CS.CommonAudioController.PlayUI("UI_Wheel_Loop");		
		CS.OPSPanelBackGround.Instance.CanClick = false;		
		CS.CommonController.Invoke(StopUI,duration,CS.OPSPanelController.Instance);
	end
end


local CheckCurrentAngle = function(self,order)
	if not self.currentPanelConfig.ContainerClockInfos:ContainsKey(CS.OPSPanelBackGround.currentContainerId) then
		return;
	end
	local info = self.currentPanelConfig.ContainerClockInfos[CS.OPSPanelBackGround.currentContainerId];
	if order < 0 or order > info.missionIds.Count - 1 then
		 return;
	end
	local missionid = info.missionIds[order][CS.OPSPanelController.difficulty];
	if self.clockSelectRing ~= nil and not self.clockSelectRing:isNull() then
		CS.CommonAudioController.PlayUI("UI_Wheel_Lock");
		local title = self.clockSelectRing.transform:Find("CurrentMission");
		title.gameObject:SetActive(false);
		local canvastitle = title.gameObject:GetComponent(typeof(CS.UnityEngine.CanvasGroup));
		if canvastitle == nil then
			canvastitle = title.gameObject:AddComponent(typeof(CS.UnityEngine.CanvasGroup));
		end
		canvastitle:DOFade(1, 0.5);
	end
	CS.OPSPanelController.missionIdTemp = missionid;
	local missionInfo = CS.GameData.listMissionInfo:GetDataById(missionid);
	local parent = self.clockSelectRing.transform:Find("Ring");
	local title = self.clockSelectRing.transform:Find("CurrentMission");
	title.gameObject:SetActive(false);
	title.gameObject:SetActive(true);
	local text = title:Find("MissionName/Tex_MissionName"):GetComponent(typeof(CS.ExText));
	title:Find("StoryOnly").gameObject:SetActive(missionInfo.specialType == CS.MapSpecialType.Story);
	text.text = missionInfo.name;
	local missionBase = parent.gameObject:GetComponent(typeof(CS.OPSPanelMissionBase));
	if missionBase == nil then
		missionBase = parent.gameObject:AddComponent(typeof(CS.OPSPanelMissionBase));
	end
	if self.child ~= nil then
		local Image = self.child.gameObject:GetComponent(typeof(CS.UnityEngine.UI.Image));
		Image:DOKill();
		local mission = self.MissionInfoController.mission;
		if mission ~= nil then
			Image.color = CS.UnityEngine.Color.black;
		else
			Image.color = CS.UnityEngine.Color(0.741, 0.706, 0.651, 1);
		end
		self.child = nil;	
	end
	self.MissionInfoController.gameObject:SetActive(true);
	missionBase.missionIds = info.missionIds[order]:ToArray();	
	self.child = parent:GetChild(order);
	self.Line:ShowLine(self.child, self.MissionInfoController.transform:Find("LinePoint"));
	local image = self.child:GetComponent(typeof(CS.ExImage));
	image:DOKill();
	image.color = CS.UnityEngine.Color.black;
	image:DOColor(CS.UnityEngine.Color(0.741, 0.706, 0.651, 1),0.5):SetLoops(-1,CS.DG.Tweening.LoopType.Yoyo);
	if missionIdrecord == missionid then
		return;
	end
	missionIdrecord = missionid;
	self.MissionInfoController:InitData(missionBase);
	print("CheckCurrent"..missionIdrecord)
end

local CloseMissionInfo = function(self)
	--self:CloseMissionInfo();
	self.MissionInfoController.gameObject:SetActive(false);
	self.Line:CloseLine();
	if self.child ~= nil then
		local Image = self.child.gameObject:GetComponent(typeof(CS.UnityEngine.UI.Image));
		Image:DOKill();
		local mission = self.MissionInfoController.mission;
		if mission ~= nil then
			Image.color = CS.UnityEngine.Color.black;
		else
			Image.color = CS.UnityEngine.Color(0.741, 0.706, 0.651, 1);
		end
		self.child = nil;	
	end
	if self.clockSelectRing ~= nil and not self.clockSelectRing:isNull() then
		CS.CommonAudioController.PlayUI("UI_Wheel_Start");
		local control = self.clockSelectRing.transform:Find("Ring"):GetComponent(typeof(CS.ImageRotateControl));
		control.checkSelectValue = true;
		print("check1");
		local title = self.clockSelectRing.transform:Find("CurrentMission");
		local canvastitle = title.gameObject:GetComponent(typeof(CS.UnityEngine.CanvasGroup));
		if canvastitle == nil then
			canvastitle = title.gameObject:AddComponent(typeof(CS.UnityEngine.CanvasGroup));
		end
		--title.gameObject:SetActive(true);
		canvastitle:DOFade(0, 0.5);     
	end	
end

local InitClockSelect = function(self,show,play)
	self:InitClockSelect(show,play);
	if not self.currentPanelConfig.ContainerClockInfos:ContainsKey(CS.OPSPanelBackGround.currentContainerId) then
		return;
	end
	local parentRing = self.clockSelectRing.transform:Find("Ring");
	local control = parentRing:GetComponent(typeof(CS.ImageRotateControl));
	local info = self.currentPanelConfig.ContainerClockInfos[CS.OPSPanelBackGround.currentContainerId];
	local check = false;
	if selectTemp then
		for i=0,info.missionIds.Count-1 do
			local missionId = info.missionIds[i][CS.OPSPanelController.difficulty];
			if CS.OPSPanelController.missionIdTemp == missionId then
				if not check  then
					check = true;							
					control.currentSelect = i;
					print("选中"..missionId)
				end
			end
		end
	end	
	for i=0,info.missionIds.Count-1 do
		local missionId = info.missionIds[i][CS.OPSPanelController.difficulty];
		local mission = CS.GameData.listMission:GetDataById(missionId);
		if mission ~= nil and mission.UseWinCounter == 0 then
			if not check and not selectDiffcluty then
				check = true;
				CS.OPSPanelController.missionIdTemp = missionId;							
				control.currentSelect = i;
				print("选中"..missionId)
			end
		end
		if mission ~= nil then
			angleDragmin = -self.startAngle - (i)*control.useAverageStopAngle;
		end
	end		
	print("检查select")
	control.addCheck = 1;
	control.posCheck = 0.5;
	control.angle = -self.startAngle - (control.currentSelect)*control.useAverageStopAngle;
	--control.angleMin = -(info.missionIds.Count * info.angle)-1;
	angleDragmax = -self.startAngle;
	--angleDragmin = -self.startAngle - (info.missionIds.Count-1)*control.useAverageStopAngle;
	
	for i=0,parentRing.childCount-1 do
		local btn = parentRing:GetChild(i):GetComponent(typeof(CS.ExButton));
		btn.onClick:RemoveAllListeners();
		btn:AddOnClick(function()
			local checkAngle = -self.startAngle - (i) * control.useAverageStopAngle;
			if checkAngle < angleDragmin then
				return;	
			end
			if self.child ~= nil then
				local image = self.child:GetComponent(typeof(CS.UnityEngine.UI.Image));
				image:DOKill();
				local mission = self.MissionInfoController.mission;
				if mission ~= nil then
					image.color = CS.UnityEngine.Color.black;
				else
					image.color = CS.UnityEngine.Color(0.741, 0.706, 0.651, 1);
				end	
			end
			local parentRing = self.clockSelectRing.transform:Find("Ring");
			local control = parentRing:GetComponent(typeof(CS.ImageRotateControl));
			control.angle = checkAngle;
			self:CheckCurrentAngle(i);
		end);
	end
end

local CheckClockMissionSelect = function(self,container)
	self:CheckClockMissionSelect(container);
	if CS.OPSPanelBackGround.currentContainerId == 0 then
		self:InitClockSelect(false, false);
	else
		if self.currentPanelConfig.ContainerClockInfos:ContainsKey(CS.OPSPanelBackGround.currentContainerId) then
			self:InitClockSelect(true, true);
		else
			self:InitClockSelect(false, false);
		end
	end
end

local InitShowContainer = function(self)
	if CS.OPSPanelController.lastTime == 0 then
		CS.OPSPanelController.lastTime = self.currentPanelConfig.minStart;
	end
	local checkTime = self.currentPanelConfig.minStart;
	for l=1,6 do
		if self.currentPanelConfig.ContainerClockInfos:ContainsKey(l) then
			local info = self.currentPanelConfig.ContainerClockInfos[l];
			for i=0,info.missionIds.Count-1 do
				if info.times[i] ~= 0 then
					for j=0,info.missionIds[i].Count-1 do					
						local missionid = info.missionIds[i][j];
						local mission = CS.GameData.listMission:GetDataById(missionid);
						if mission ~= nil and mission.UseWinCounter>0 then
							--if info.times[i]>checkTime then
							checkTime = info.times[i];
							--print(missionid.."/"..checkTime)
							--end
						end				
					end
				end	
			end
		end	
	end
	CS.OPSPanelController.currentTime = checkTime;
	if CS.OPSPanelController.currentTime ~= CS.OPSPanelController.lastTime then
		CS.OPSPanelBackGround.currentContainerId = 0;
	end
	self:InitShowContainer();
end

local ReturnContainer = function(self)
	CS.OPSPanelBackGround.Instance.CanClick = true;
	missionIdrecord = 0;
	self.lastContainerid = CS.OPSPanelBackGround.currentContainerId;
	self:ReturnContainer();
	local read = CS.OPSPanelBackGround.Instance:ReadRecord();
	if not read then
		if self.lastContainerid ~= 0 then
			self:ReturnContainerPos();
		end
	end
end

local MoveMissionHolder = function(self)
	if self.currentPanelConfig.ContainerClockInfos:ContainsKey(CS.OPSPanelBackGround.currentContainerId) then
		return;
	end
	self:MoveMissionHolder();
end

local ShowContainerReturn = function(self,show,play)
	self:ShowContainerReturn(show,play);
	if self.currentContainer ~= nil and not self.currentContainer:isNull() then
		self.currentContainer:RefreshUI();
	end
end

local SelectContainer = function(self,container,playanim)
	self:SelectContainer(container,playanim);
	if container.clockinfo ~= nil then
		for i=0,CS.OPSPanelBackGround.Instance.spotMissionHolders.Count-1 do
			local holder = CS.OPSPanelBackGround.Instance.spotMissionHolders[i];
			holder:RefreshUI();
		end
	else
		local child = self.containerReturn.transform:Find("ChapterContainer"):GetChild(0);
		if child ~= nil then
			local canvasgroup = child:GetComponent(typeof(CS.UnityEngine.CanvasGroup));
			canvasgroup.alpha = 1;
		end
		self:InitClockSelect(false,playanim);
		CS.OPSPanelBackGround.Instance:ResetClockContainer(playanim);
	end
end

local ShowSpecialReturn = function(self)
	self:ShowSpecialReturn();
	if self.campaionId == -48 then
		local targetMall = self.transform:Find("Left/2021Summer_GotoMall(Clone)");
		local targetPoint = self.transform:Find("Left/2021Summer_PointExchange(Clone)");
		local showPoint = CS.OPSPanelBackGround.currentContainerId == 7;
		if targetMall ~= nil then
			targetMall.gameObject:SetActive(not showPoint);
		end
		if targetPoint ~= nil then
			targetPoint.gameObject:SetActive(showPoint);
		end	
	end
end

function Close()
	selectTemp = false;
end

local SelectProcessInfo = function(self,processInfo)
	if processInfo.mission ~= nil and processInfo.mission.clocked then
		local iter = processInfo.mission.missionInfo.PointCose:GetEnumerator()     
		while iter:MoveNext() do                      
			local item = iter.Current.Key;
			local num = iter.Current.Value;
			local itemInfo = CS.GameData.listItemInfo:GetDataById(item);
			local realNum = CS.OPSPanelController.Instance.item_use[item].itemRealNum;
			if realNum == 0 or realNum < num then
				if self.campaionId == -32 then
					CS.CommonController.ConfirmBox(CS.Data.GetLang(230011),function()
							CS.CommonController.GotoScene("Dorm", 20004)
						end)
					return;
				else
					local txt = CS.System.String.Format(CS.Data.GetLang(60072), itemInfo.name);
					CS.CommonController.LightMessageTips(txt);
					return;
				end
			end                    
		end	
		if processInfo.panelHolder ~= nil then
			if processInfo.panelHolder.currentLabel == nil then
				CS.OPSPanelBackGround.Instance:Move(processInfo.panelHolder.transform.localPosition, true, 0.5);
				processInfo.panelHolder:ShowLable();				
			end
			CS.OPSPanelController.Instance:ShowUnclockMessageBox(processInfo.panelHolder.currentLabel);
		end		
		return;
	end
	selectTemp = true;
	self.currentChoose = nil;
	self.chooseSpot = nil;
	if processInfo.panelHolder == nil then
		self:ShowAllMission();
	end
	for i=0,CS.OPSPanelBackGround.Instance.spotMissionHolders.Count-1 do
		local holder = CS.OPSPanelBackGround.Instance.spotMissionHolders[i];
		if holder.currentLabel ~= nil then
			holder.currentLabel.lastmissioninfo = nil;
		end		
	end	
	self:SelectProcessInfo(processInfo);
	CS.CommonController.Invoke(Close,1,CS.OPSPanelController.Instance);
end

local CheckAnim = function(self)
	missionIdrecord = 0;
	self:CheckAnim();
end

local CheckReturnContainer = function()
	CS.OPSPanelController.Instance.CanClick = true;
	CS.OPSPanelController.Instance:ReturnContainer();
end
local CheckClockTimeDelay = function(self)
	if self.currentPanelConfig.ContainerClockInfos.Keys.Count == 0 then
		return false;
	end
	for i = 0,CS.OPSPanelBackGround.Instance.opsMissionContainers.Count-1 do
		local container = CS.OPSPanelBackGround.Instance.opsMissionContainers[i];
		if not self.order_angle:ContainsKey(container.id) then
			self.order_angle:Add(container.id,0);
		end
	end	
	if CS.OPSPanelController.lastTime == 0 then
		CS.OPSPanelController.lastTime = self.currentPanelConfig.minStart;
	end
	local checkTime = self.currentPanelConfig.minStart;
	for l=1,6 do
		if self.currentPanelConfig.ContainerClockInfos:ContainsKey(l) then
			local info = self.currentPanelConfig.ContainerClockInfos[l];
			for i=0,info.missionIds.Count-1 do
				if info.times[i] ~= 0 then
					for j=0,info.missionIds[i].Count-1 do					
						local missionid = info.missionIds[i][j];
						local mission = CS.GameData.listMission:GetDataById(missionid);
						if mission ~= nil and mission.UseWinCounter>0 then
							--if info.times[i]>checkTime then
							checkTime = info.times[i];
							--print(missionid.."/"..checkTime)
							--end
						end				
					end
				end	
			end
		end	
	end
	CS.OPSPanelController.currentTime = checkTime;
	if CS.OPSPanelController.currentTime ~= CS.OPSPanelController.lastTime then
		print("时间变更")
		if CS.OPSPanelBackGround.currentContainerId ~= 0 then
			CS.OPSPanelController.Instance:ReturnContainer();
			--CS.CommonController.Invoke(CheckReturnContainer,1,CS.OPSPanelController.Instance);
		end
		return true;
	end
	return false;
end

local RequestUnClockCampaigns = function(self)
	self:RequestUnClockCampaigns();
	local mapMission = CS.GameData.listMissionMapInfo:GetDataById(self.panelMissionuse.currentMissionInfo.mapped_mission_id);
	if mapMission ~= nil then
		local missionids = mapMission.missionids;
		for i=0,missionids.Count-1 do
			local mission = CS.GameData.listMission:GetDataById(missionids[i]);
			if mission ~= nil then
				mission.clocked = false;
			end
		end
		for i=0,CS.OPSPanelBackGround.Instance.spotMissionHolders.Count-1 do
			local holder = CS.OPSPanelBackGround.Instance.spotMissionHolders[i];
			if missionids:Contains(holder.CurrentMissionId) and holder.CurrentMissionId ~= self.panelMissionuse.CurrentMissionId then
				if holder.currentLabel ~= nil then
					holder.currentLabel:ShowUnclock();
				end
			end
		end	
	end 
end
local Play3dSpotAnim = function(self,spot)
	local layer0 = spot.transform:Find("layer0");
	if layer0 == nil then
		return;
	end
	self:Play3dSpotAnim(spot);
end
local CheckSpecialAnim = function(self)
	CS.OPSPanelController.selectHolderOrder = -1;
	self:CheckSpecialAnim();
end

local Awake = function(self)
	self:Awake();
	CS.OPSPanelController.diffcluteNum = self.currentPanelConfig.diffclutyNum;
	CS.OPSPanelController.diffclutyRecord = CS.Mathf.Min(CS.OPSPanelController.diffclutyRecord, CS.OPSPanelController.diffcluteNum - 1);
	CS.OPSPanelController.difficulty = CS.OPSPanelController.diffclutyRecord;
end
util.hotfix_ex(CS.OPSPanelController,'SelectDiffcluty',SelectDiffcluty)
util.hotfix_ex(CS.OPSPanelController,'CheckSpineMove',CheckSpineMove)
util.hotfix_ex(CS.OPSPanelController,'CheckContainerAngle',CheckContainerAngle)
util.hotfix_ex(CS.OPSPanelController,'Start',Start)
util.hotfix_ex(CS.OPSPanelController,'PlayTime',PlayTime)
util.hotfix_ex(CS.OPSPanelController,'CheckCurrentAngle',CheckCurrentAngle)
util.hotfix_ex(CS.OPSPanelController,'CloseMissionInfo',CloseMissionInfo)
util.hotfix_ex(CS.OPSPanelController,'InitClockSelect',InitClockSelect)
util.hotfix_ex(CS.OPSPanelController,'CheckClockMissionSelect',CheckClockMissionSelect)
util.hotfix_ex(CS.OPSPanelController,'InitShowContainer',InitShowContainer)
util.hotfix_ex(CS.OPSPanelController,'ReturnContainer',ReturnContainer)
util.hotfix_ex(CS.OPSPanelController,'MoveMissionHolder',MoveMissionHolder)
util.hotfix_ex(CS.OPSPanelController,'ShowContainerReturn',ShowContainerReturn)
util.hotfix_ex(CS.OPSPanelController,'SelectContainer',SelectContainer)
util.hotfix_ex(CS.OPSPanelController,'ShowSpecialReturn',ShowSpecialReturn)
util.hotfix_ex(CS.OPSPanelController,'SelectProcessInfo',SelectProcessInfo)
util.hotfix_ex(CS.OPSPanelController,'CheckAnim',CheckAnim)
util.hotfix_ex(CS.OPSPanelController,'CheckClockTimeDelay',CheckClockTimeDelay)
util.hotfix_ex(CS.OPSPanelController,'RequestUnClockCampaigns',RequestUnClockCampaigns)
util.hotfix_ex(CS.OPSPanelController,'Play3dSpotAnim',Play3dSpotAnim)
util.hotfix_ex(CS.OPSPanelController,'CheckSpecialAnim',CheckSpecialAnim)
util.hotfix_ex(CS.OPSPanelController,'Awake',Awake)