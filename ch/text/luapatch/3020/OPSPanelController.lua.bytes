local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local CheckMapAnimator = function(self)
	if self.lastSelectOrder ~= CS.OPSPanelController.currentSelectOrder then
		self.CanClick = false;
	end
	local playGroup = self.leftMain.gameObject:GetComponent(typeof(CS.TweenPlayGroup));
	if playGroup == nil or playGroup:isNull() then
		playGroup = self.leftMain.gameObject:AddComponent(typeof(CS.TweenPlayGroup));
	end
	if self.lastSelectOrder == -1 then
		playGroup.CurrentTweenPlayOrder = (CS.OPSPanelController.currentSelectOrder + 1) * 10 + (CS.OPSPanelController.currentSelectOrder + 1);
		CS.CommonController.Invoke(function()
				playGroup:PlayCurrentAllyOrderTween();
			end,0.3,CS.OPSPanelController.Instance);
	elseif self.lastSelectOrder ~= CS.OPSPanelController.currentSelectOrder then
		playGroup.CurrentTweenPlayOrder = (self.lastSelectOrder + 1) * 10 + (CS.OPSPanelController.currentSelectOrder + 1);
		playGroup:PlayCurrentAllyOrderTween();
	end
	self:CheckMapAnimator();
end

local EndMapAnimator = function(self)
	self:EndMapAnimator();
	self.CanClick = true;
end
local SelectMapAnimatorDefault = function(self)
	self:SelectMapAnimatorDefault();
	self.CanClick = true;
end
local InitBgm = function(self)
	self:InitBgm();
	local bgmname = "Campaion"..tostring(self.campaionId).."-"..tostring(CS.OPSPanelController.currentSelectOrder+1);
	CS.CommonAudioController.PlayBGM(bgmname);
end
local CheckModuleSpine = function(self)
	if self.currentPanelConfig.opsSpineMissions.Keys.Count == 0 then
		return;
	end
	local iter = self.currentPanelConfig.opsSpineMissions:GetEnumerator();     
	while iter:MoveNext() do    
		local code = iter.Current.Key;
		local opsspinemission = iter.Current.Value;
		local currentIndex = opsspinemission:CheckMissionShowOrder();
		if opsspinemission.currentOrder ~= currentIndex then
			opsspinemission.currentOrder = currentIndex;
			local moduleControl = nil;
			for i=0,self.moduleControls.Count -1 do
				if self.moduleControls[i].currentModuleDataName == opsspinemission.moudleName or self.moduleControls[i].gameObject.name == opsspinemission.moudleName then
					moduleControl = self.moduleControls[i];
				end
			end
			if moduleControl ~= nil then
				if currentIndex<0 then
					local trans = moduleControl.transform:Find(code);
					if trans ~= nil  then
						print("隐藏spine"..code);
						trans.gameObject:SetActive(false);
					end
				else
					opsspinemission.moudleIndex = self.moduleControls:IndexOf(moduleControl);
					local aiIndex = opsspinemission:GetAIMissionIndex();
					aiIndex = CS.Mathf.Clamp(aiIndex, 0, opsspinemission.opsSpineAI.Count - 1);
					if opsspinemission.opsSpineAI.Count>0 then
						moduleControl:InitMoveSpine(code,opsspinemission.opsSpineAI[aiIndex]);
					end
				end
			end
		end
	end              
end

local ShowProcess = function(self)
	print("测试ShowProcess");
	if self.processTxt == nil then
		return;
	end
	if self.campaionId == -58 then
		local ClearCount = 0;
		local AllCount = 0;
		for i=0,self.currentPanelConfig.opsBuildMissions.Count-1 do
			local opsBuildMission = self.currentPanelConfig.opsBuildMissions[i];
			ClearCount = ClearCount + opsBuildMission.opsMission:ClearCount();
			AllCount = AllCount + opsBuildMission.opsMission:AllCount();
		end
		local iter = self.currentPanelConfig.opsSpineMissions:GetEnumerator();
		while iter:MoveNext() do    
			local opsspinemission = iter.Current.Value;
			ClearCount = ClearCount + opsspinemission:ClearCount();
			AllCount = AllCount + opsspinemission:AllCount();
		end 
		for i=0,self.currentPanelConfig.towerMissionConfig.opsTowerMissions.Count-1 do
			local towerMission = self.currentPanelConfig.towerMissionConfig.opsTowerMissions[i];
			if towerMission.opsmission ~= nil then
				ClearCount = ClearCount + towerMission.opsmission:ClearCount();
				AllCount = AllCount + towerMission.opsmission:AllCount();	
			elseif towerMission.selectorData ~= nil then
				for j=0,towerMission.selectorData.opsmissions.Count-1 do
					ClearCount = ClearCount + towerMission.selectorData.opsmissions[j]:ClearCount();
					AllCount = AllCount + towerMission.selectorData.opsmissions[j]:AllCount();
				end
			end
		end
		self.processTxt.text = CS.Data.GetLang(30251)..tostring(ClearCount).."/"..tostring(AllCount);
	else
		self:ShowProcess();
	end
end

local Start = function(self)
	CS.ResManager.GetObjectByPath("UGUIPrefabs/SpecialOPS/OPSMissionInfo");
	self:Start();
end

local CheckEndlessPoint = function(self)
	if self.currentPanelConfig.highScoreInfo ~= nil then
		if self.currentPanelConfig.highScoreInfo.opsmission ~= nil then
			if self.currentPanelConfig.highScoreInfo.opsmission.currentMissionInfo == nil then
				self.currentPanelConfig.highScoreInfo.opsmission = nil;
			end
		end
	end
	self:CheckEndlessPoint();
end

opsShowTime = 0;
opsEnterTime = 0;
opsDispearTime = 0;
function CheckOPSTime(self)
	local temp = CS.Data.GetString("2022_bikini_time");
	if CS.System.String.IsNullOrEmpty(temp) then
		return;
	end
	local times =Split(temp,",");
	opsShowTime = tonumber(times[1]);
	opsEnterTime = tonumber(times[2]);
	opsDispearTime = tonumber(times[3]);
	print("opsShowTime"..opsShowTime);
	print("opsEnterTime"..opsEnterTime);
	print("opsDispearTime"..opsDispearTime);
	local stamp = CS.GameData.GetCurrentTimeStamp();
	if stamp>opsShowTime and stamp<opsDispearTime then
		local parent = self.btnTheater.transform.parent;
		local obj = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Prefabs/2022BikiniResultEntrance"), parent, false);
		local unclock = obj.transform:Find("Img_Unlocked");
		unclock.gameObject:SetActive(stamp>opsEnterTime);
		local clock = obj.transform:Find("Img_Locked");
		clock.gameObject:SetActive(stamp<opsEnterTime);
		local btn = obj:GetComponent(typeof(CS.ExButton));
		btn:AddOnClick(function()
				EnterOPS();
			end)
	end
end

function EnterOPS()
	if opsEnterTime<CS.GameData.GetCurrentTimeStamp() then
		CS.OPSConfig.Instance:GoToScene(-52);
	else
		local dateTime = CS.GameData.UnixToDateTime(opsEnterTime);
		local time = tostring(dateTime.Month).."/"..tostring(dateTime.Day);
		local txt = tostring(CS.System.String.Format(CS.Data.GetLang(60348),time));
		CS.CommonController.LightMessageTips(txt);
	end
end
function Split(szFullString, szSeparator)
	local nFindStartIndex = 1
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end
local InitUIElements= function(self)
	self:InitUIElements();
	CheckOPSTime(self);
end

local checkRequestDrawEvent = false;
local RequestDrawEvent = function(self)
	if checkRequestDrawEvent then
		self:RequestDrawEvent();
	end
end
local LoadBackgroundVideo = function(self)
	self:LoadBackgroundVideo();
	checkRequestDrawEvent = true;
	self:RequestDrawEvent();
end
local Awake = function(self)
	util.hotfix_ex(CS.OPSPanelController,'CheckMapAnimator',CheckMapAnimator)
	util.hotfix_ex(CS.OPSPanelController,'EndMapAnimator',EndMapAnimator)
	util.hotfix_ex(CS.OPSPanelController,'SelectMapAnimatorDefault',SelectMapAnimatorDefault)
	util.hotfix_ex(CS.OPSPanelController,'InitBgm',InitBgm)
	util.hotfix_ex(CS.OPSPanelController,'CheckModuleSpine',CheckModuleSpine)
	util.hotfix_ex(CS.OPSPanelController,'ShowProcess',ShowProcess)
	util.hotfix_ex(CS.OPSPanelController,'Start',Start)
	util.hotfix_ex(CS.OPSPanelController,'CheckEndlessPoint',CheckEndlessPoint)
	util.hotfix_ex(CS.OPSPanelController,'RequestDrawEvent',RequestDrawEvent)
	util.hotfix_ex(CS.OPSPanelController,'LoadBackgroundVideo',LoadBackgroundVideo)
	checkRequestDrawEvent = false;
	self:Awake();
end
util.hotfix_ex(CS.OPSPanelController,'Awake',Awake)
util.hotfix_ex(CS.HomeController,'InitUIElements',InitUIElements)
