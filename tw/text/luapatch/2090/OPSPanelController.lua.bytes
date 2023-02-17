--local _, LuaDebuggee = pcall(require, 'LuaDebuggee')
--if LuaDebuggee and LuaDebuggee.StartDebug then
	--LuaDebuggee.StartDebug('127.0.0.1', 9826)
--else
	--print('Please read the FAQ.pdf')
--end
local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
local homeController = require("2090/HomeController")

local InitClockSelect = function(self,show,play)
	if CS.GameData.missionAction ~= nil then
		self.selectProcess = true;
		self.missionIdTemp = CS.GameData.missionAction.missionInfo.id;
	end
	if self.clockSelectRing ~= nil and not self.clockSelectRing:isNull() then
		local parentRing = self.clockSelectRing.transform:Find("Ring");
		for i=0,parentRing.childCount-1 do
			local image = parentRing:GetChild(i):GetComponent(typeof(CS.ExImage));
			image:DOKill();
		end
	end
	self:InitClockSelect(show,play);
	if self.currentPanelConfig.ContainerClockInfos:ContainsKey(CS.OPSPanelBackGround.currentContainerId) then
		local info = self.currentPanelConfig.ContainerClockInfos[CS.OPSPanelBackGround.currentContainerId];
		for i=0,info.missionIds.Count-1 do
			local missionid = info.missionIds[i][CS.OPSPanelController.difficulty];
			local mission = CS.GameData.listMission:GetDataById(missionid);
			if mission ~= nil then
				self.control.angleDragmin = -self.startAngle - i * self.control.useAverageStopAngle;
			end
		end
	end
	if self.clockSelectRing ~= nil and not self.clockSelectRing:isNull() then
		local title =  self.clockSelectRing.transform:Find("CurrentMission");
		if title ~= nil then
			local group = title:GetComponent(typeof(CS.UnityEngine.CanvasGroup));
			if group ~= nil and not group:isNull() then
				if show then 
					group.alpha = 1;
				else
					group.alpha = 0;
				end
			end
		end
	end
	self.selectProcess = false;
end
local CheckCurrentAngle = function(self,order)
	self:CheckCurrentAngle(order);
	if self.clockSelectRing ~= nil and not self.clockSelectRing:isNull() then
		local title =  self.clockSelectRing.transform:Find("CurrentMission");
		if title ~= nil then
			local group = title:GetComponent(typeof(CS.UnityEngine.CanvasGroup));
			if group ~= nil and not group:isNull() then
				group:DOKill();
				group.alpha = 1;
			end
		end
	end
end
local ShowContainerReturn = function(self,show,play)
	self:ShowContainerReturn(show,play);
	self:CheckEndlessPoint();
	if self.campaionId == -51 and self.specialItemObj ~= nil and not self.specialItemObj:isNull() then
		self.specialItemObj:SetActive(CS.OPSPanelBackGround.currentContainerId == 5);
	end
	if self.campaionId == -51 and self.btnTitleTrans ~= nil and not self.btnTitleTrans:isNull() then
		local main = self.leftMain:Find("FixedPoint_Left(Clone)/Main");
		if CS.OPSPanelBackGround.currentContainerId ~= 5 and CS.OPSPanelBackGround.currentContainerId ~= 6 then
			self.btnTitleTrans.gameObject:SetActive(true);
			if main ~= nil then
				local mainTrans = main:GetComponent(typeof(CS.UnityEngine.RectTransform));
				main:DOAnchorPosY(420,0.5);
			end
		else
			self.btnTitleTrans.gameObject:SetActive(false);
			if main ~= nil then
				local mainTrans = main:GetComponent(typeof(CS.UnityEngine.RectTransform));
				main:DOAnchorPosY(300,0.5);
			end
		end		
	end
	if self.campaionId == -51 and self.containerBackground ~= nil and not self.containerBackground:isNull() then
		self.containerBackground:SetActive(CS.OPSPanelBackGround.currentContainerId == 0);
		if CS.OPSPanelBackGround.currentContainerId == 0 then
			self.containerBackground.transform:Find("Background").gameObject:SetActive(true);
			self.containerBackground.transform:Find("Img_EyeBG").gameObject:SetActive(true);
			self.containerBackground.transform:Find("Img_Stage1").gameObject:SetActive(false);
			self.containerBackground.transform:Find("Img_Stage2").gameObject:SetActive(false);
			self.containerBackground.transform:Find("Img_Stage3").gameObject:SetActive(false);
			self.containerBackground.transform:Find("Img_Stage4").gameObject:SetActive(false);
			local id = 1;
			for i=0,CS.OPSPanelBackGround.Instance.opsMissionContainers.Count -1 do
				local container = CS.OPSPanelBackGround.Instance.opsMissionContainers[i];
				if container.id ~= 5 and container.id ~= 6 and not container:ShowClock()then
					id = CS.Mathf.Max(id, container.id);
				end
			end
			if id  == 1 then
				self.containerBackground.transform:Find("Img_Stage1").gameObject:SetActive(true);
			elseif id  == 2 then
				self.containerBackground.transform:Find("Img_Stage2").gameObject:SetActive(true);
			elseif id  == 3 then
				self.containerBackground.transform:Find("Img_Stage3").gameObject:SetActive(true);
			elseif id  == 4 then
				self.containerBackground.transform:Find("Img_Stage4").gameObject:SetActive(true);
			end
		end
	end
end

local PlayTime = function(self,play,forward,hour,min,duration)
	if self.campaionId == -51 then
		return;
	end
	self:PlayTime(play,forward,hour,min,duration);
end
local ShowClockTime = function(self,show,play)
	if self.campaionId == -51 then
		return;
	end
	self:ShowClockTime(show,play);
end


local ShowTip = function(self,go)
	local index = go.transform:GetSiblingIndex();
	local iteminfo = CS.GameData.listItemInfo:GetDataById(CS.OPSConfig.Instance.opsShowItems[self.campaionId].showItemIds[index]);
	local posOffset = CS.UnityEngine.Vector3(-300, 100, 0);
	CS.CommonTipsContent.ShowTips(iteminfo.name, iteminfo.introduction, "", 9, go.transform:TransformPoint(posOffset), go.transform.parent, 100);
end

local OpenRuler = function(self)
	if self.highScoreObj~= nil and not self.highScoreObj:isNull() then
		local txt = self.highScoreObj.transform:Find("Main/Btn_Rule/URL"):GetComponent(typeof(CS.ExText));
		if not CS.System.String.IsNullOrEmpty(txt.text) then
			self:OpenAnnouncement(txt.text);
			return;
		end
	end
	self:OpenRuler();
end
local ShowItemRuler = function(self)
	if self.specialItemObj~= nil and not self.specialItemObj:isNull() then
		local txtUrl = self.specialItemObj.transform:Find("MissionItems/Btn_Rule/URL");
		if txtUrl == nil then
			return;
		end
		local txt = txtUrl:GetComponent(typeof(CS.ExText));
		if not CS.System.String.IsNullOrEmpty(txt.text) then
			self:OpenAnnouncement(txt.text);
			return;
		end
	end
	self:ShowItemRuler();
end
checkScale = false;
local ReturnContainer = function(self)
	if not self.CanClick then
		return;
	end
	checkScale = true;
	self:ReturnContainer();
	CS.CommonController.Invoke(function()
		CS.OPSPanelBackGround.Instance:ReadRecord();
		end,0.7,CS.OPSPanelController.Instance);
end
local CheckSpineSpot = function(self)
	if self.currentContainer ~= nil and not self.currentContainer:isNull() then
		if self.currentContainer.clockinfo ~= nil then
			return;
		end
	end
	self:CheckSpineSpot();
end

local CheckIsolateSpots= function(self)
	self:CheckIsolateSpots();
	for	i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
		local spot=CS.OPSPanelBackGround.Instance.all3dSpots[i];
		if spot.mission~=nil and not CS.SpecialActivityController.missionid_State:ContainsKey(spot.mission.missionInfo.id)	then
			if not self.playSpots:Contains(spot) then
				self.playSpots:Add(spot);
			end
		end
	end
end

local LoadTime = function(self)
	if CS.MissionSelectionController.normalActivityCampaion:Contains(self.campaionId) then
		return;
	end
	self:LoadTime();
end

local	LoadProcess=function(self)
	self:LoadProcess();
	if	self.timeProcess~=nil	and	not	self.timeProcess:isNull()	then
		if	self.mLeftTimeCount==nil	then
			local	trans=self.timeProcess:GetComponent(typeof(CS.UnityEngine.RectTransform));
			trans.anchoredPosition=CS.UnityEngine.Vector2(-270,-200);
		end
	end
end

local	ShowAllLabel=function(self)
	for i = 0, CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
		local	spot=CS.OPSPanelBackGround.Instance.all3dSpots[i];
		if spot.mission~=nil	and	spot.difficulty ==CS.OPSPanelController.difficulty	then
			spot:Show(true,0);
		end
	end
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
	self:SelectProcessInfo(processInfo);
end


opsControl=nil;
local gunCode = {"M1903_36_1107_60314_60315_60368_1",
	"WA2000_48_1108_60316_60317_60369_2",
	"FN49_51_4709_60318_60319_60370_3",
	"NTW20_53_1101_60320_60321_60371_4",
	"G41_62_2401_60322_60323_60369_2",
	"G36_64_2407_60324_60325_60372_5",
	"FNFAL_106_2406_60326_60327_60373_6",
	"95type_129_1102_60328_60329_60374_7",
	"FN57_142_1109_60330_60331_60376_9",
	"G28_146_1104_60332_60333_60369_2",
	"AA12_163_2403_60334_60335_60374_7",
	"CBJMS_213_3503_60336_60337_60375_8",
	"UKM2000_254_6106_60338_60339_60369_2",
	"4type_270_3505_60340_60341_60369_2",
	"DP12_282_6102_60342_60343_60374_7",
	"KAC_286_4706_60344_60345_60374_7",
	"PPD40_336_6105_60346_60347_60377_10"}
voteList = {};
local votePanel = nil;
diffcluty = 0;
local missionPanel = nil;
local OPSPanelMissionBase = nil;
local Awake = function(self)
	--print("加载2090");
	opsControl= self;
	CS.OPSPanelController.diffclutyRecord = CS.Mathf.Max(CS.OPSPanelController.diffclutyRecord, 0);
	self:Awake();
	CS.OPSPanelController.diffcluteNum = self.currentPanelConfig.diffclutyNum;
	CS.OPSPanelController.diffclutyRecord = CS.Mathf.Min(CS.OPSPanelController.diffclutyRecord, CS.OPSPanelController.diffcluteNum - 1);
	CS.OPSPanelController.difficulty = CS.OPSPanelController.diffclutyRecord;
	if self.campaionId == -52 then
		print("加载泳装活动界面");	
		opsControl.transform:Find("Top").gameObject:SetActive(false);	
		InitData();
		ShowBackground();		 
		self.gobjWeb:AddComponent(typeof(CS.ImageBufferBlurRefraction));
	end
end
local mat = nil;
local Start = function(self)
	self:Start();
	if self.campaionId == -52 then
		CS.OPSPanelBackGround.Instance.gameObject:SetActive(false);
		if OPSPanelMissionBase == nil or OPSPanelMissionBase:isNull() then
			OPSPanelMissionBase = opsControl.transform:Find("Map").gameObject:AddComponent(typeof(CS.OPSPanelMissionBase));
		end
		local shader = CS.ResManager.GetObjectByPath("Shader/Sprites-Twinkle", ".shader");
		mat = CS.UnityEngine.Material(shader);
	end
end

local InitShowContainer = function(self)
	if self.campaionId == -52 then
		return;
	end
	self:InitShowContainer();	
end
local SelectDiffcluty = function(self)
	local show = opsControl.MissionInfoController.gameObject.activeSelf;
	self:SelectDiffcluty();
	if self.campaionId == -52 and show then
		ShowMissionPanel();
	end
end
local InitBgm=function(self)
	self:InitBgm();
	local request=CS.RequestDrawEvent(CS.OPSPanelController.OpenCompaions);
	request:Request();
	if self.campaionId == -52 then
		ShowBackground();
	end
end

local RefreshUI = function(self,onlyrefreshLabel)
	self:RefreshUI(onlyrefreshLabel);
	if self.currentContainer ~= nil and not self.currentContainer:isNull() then
		self.currentContainer:RefreshUI();
	end
	if self.campaionId == -52 then
		ShowBackground();
	end
end
function InitData()--数据初始化
	voteList = {};
	for i=1,#gunCode do
		local codes =Split(gunCode[i],"_");	
		local vodeInfo = {};
		vodeInfo[1] = 0;--总好人票
		vodeInfo[2] = 0;--总坏人票
		vodeInfo[3] = 0;--自己好人票
		vodeInfo[4] = 0;--自己坏人票
		vodeInfo[5] = tostring(codes[1]);--code
		vodeInfo[6] = tonumber(codes[2]);--id
		vodeInfo[7] = tonumber(codes[3]);--skinid	
		vodeInfo[8] = tonumber(codes[4]);--好人台词id
		vodeInfo[9] = tonumber(codes[5]);--坏人台词id
		vodeInfo[10] = tonumber(codes[6]);--身份
		vodeInfo[11] = tonumber(codes[7])-1;--对应图片order
		table.insert(voteList,vodeInfo);
	end
end

local voteMap = nil;
local CancelMission = function(self)
	self:CancelMission();
	if self.currentContainer ~= nil and not self.currentContainer:isNull() then
		self:InitClockSelect(true, false);
	end
	if voteMap ~= nil then
		local background = voteMap.transform:Find("MissionInfoBG");
		background.gameObject:SetActive(false);
	end
end

function AddMissionBtn(name)
	local Mission = voteMap.transform:Find(name);
	local btnMission = Mission:GetComponent(typeof(CS.ExButton));
	btnMission:AddOnClick(function()
			ClickMission(name);
		end);
end
local currentName = "";

function ClickMission(name)
	CheckIconSeleect(false);
	currentName = name;
	CloseMissionPanel();
	if name == "MissionSpecial" then
		ShowSpecialUI(true);		
		return;
	end
	OPSPanelMissionBase.entranceId = 0;
	if name == "Mission1" then
		OPSPanelMissionBase.missionIds[0] = 11115;
		OPSPanelMissionBase.missionIds[1] = 11115;
	elseif name == "Mission2" then
		OPSPanelMissionBase.missionIds[0] = 0;
		OPSPanelMissionBase.missionIds[1] = 0;
		OPSPanelMissionBase.entranceId = 1110700;
	elseif name == "Mission3" then
		OPSPanelMissionBase.missionIds[0] = 11103;
		OPSPanelMissionBase.missionIds[1] = 11104;
	elseif name == "Mission4" then
		OPSPanelMissionBase.missionIds[0] = 11105;
		OPSPanelMissionBase.missionIds[1] = 11106;
	elseif name == "Mission5" then
		OPSPanelMissionBase.missionIds[0] = 11101;
		OPSPanelMissionBase.missionIds[1] = 11102;
	elseif name == "Mission6" then
		OPSPanelMissionBase.missionIds[0] = 11099;
		OPSPanelMissionBase.missionIds[1] = 11100;
	elseif name == "MissionInfinite" then
		OPSPanelMissionBase.missionIds[0] = 11113;
		OPSPanelMissionBase.missionIds[1] = 11114;
	end
	ShowSpecialUI(false);
	ShowMissionPanel();
end
function CheckIconSeleect(show)
	local MissionTrans = voteMap.transform:Find(currentName);
	if MissionTrans ~= nil then
		for i=0,MissionTrans.childCount-1 do
			local child = MissionTrans:GetChild(i);
			local check = string.find(child.gameObject.name,"Img_Icon");
			if check then
				local image = child:GetComponent(typeof(CS.ExImage));
				if show then
					image.material = mat;
				else
					image.material = nil;
				end
			end
		end
	end
end
function CheckMissionkey(key)
	return  CS.GameData.missionKeyNum:ContainsKey(key) and CS.GameData.missionKeyNum[key] > 0;
end
function ShowSpecialUI(show)
	local Mission = voteMap.transform:Find("MissionSpecial/MissionList");
	Mission.gameObject:SetActive(show);
	local mission0 = CS.GameData.listMission:GetDataById(11098);
	local mission1 = CS.GameData.listMission:GetDataById(11112);
	local text = Mission:Find("MissionVote/Text_MissionName"):GetComponent(typeof(CS.ExText));
	local text1 = Mission:Find("MissionEpilogue/Text_MissionName"):GetComponent(typeof(CS.ExText));	
	local check0 = CheckMissionkey(1109900);
	local check1 = CheckMissionkey(1110100);
	local check2 = CheckMissionkey(1110300);
	local check3 = CheckMissionkey(1110500);
	local check4 = CheckMissionkey(1110700);
	local check5 = CheckMissionkey(1111500);
	local btnVote = Mission:Find("MissionVote"):GetComponent(typeof(CS.ExButton));
	local btnEpilogue = Mission:Find("MissionEpilogue"):GetComponent(typeof(CS.ExButton));		
	if check0 or check1 or check2 or check3 or check4 or check5 then
		text.color = CS.UnityEngine.Color(1,1,1,1);
		Mission:Find("MissionVote/Img_Locked").gameObject:SetActive(false);
		btnVote.enabled = true;
	else
		text.color = CS.UnityEngine.Color(128/255,128/255,128/255,1);
		Mission:Find("MissionVote/Img_Locked").gameObject:SetActive(true);
		btnVote.enabled = false;
	end
	if mission1 ~= nil then
		text1.color = CS.UnityEngine.Color(1,1,1,1);
		Mission:Find("MissionEpilogue/Img_Locked").gameObject:SetActive(false);
		btnEpilogue.enabled = true;
	else
		text1.color = CS.UnityEngine.Color(128/255,128/255,128/255,1);
		Mission:Find("MissionEpilogue/Img_Locked").gameObject:SetActive(true);
		btnEpilogue.enabled = false;
	end
end
local returnobj = nil;
function  ShowBackground()--活动背景
	if voteMap == nil or voteMap:isNull() then
		voteMap= CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2022BikiniMissionMap"), opsControl.transform, false);
		voteMap.transform:SetAsFirstSibling();
		local canvas = voteMap:GetComponent(typeof(CS.UnityEngine.Canvas));
		canvas.overrideSorting = true;
		canvas.sortingLayerName = "Background";
		AddMissionBtn("Mission1");
		AddMissionBtn("Mission2");
		AddMissionBtn("Mission3");
		AddMissionBtn("Mission4");
		AddMissionBtn("Mission5");
		AddMissionBtn("Mission6");
		AddMissionBtn("MissionInfinite");
		AddMissionBtn("MissionSpecial");
		local background = voteMap.transform:Find("MissionInfoBG");
		local btnbackground = background:GetComponent(typeof(CS.ExButton));
		btnbackground:AddOnClick(function()
				ShowSpecialUI(false);
				CheckIconSeleect(false);
				CloseMissionPanel();
			end)
		local startMission=voteMap.transform:Find("MissionSpecial/MissionList/MissionPrologue");
		local startMissionBtn = startMission:GetComponent(typeof(CS.ExButton));
		startMissionBtn:AddOnClick(function()
				OPSPanelMissionBase.entranceId = 0;
				OPSPanelMissionBase.missionIds[0] = 11098;
				OPSPanelMissionBase.missionIds[1] = 11098;
				ShowMissionPanel();
				ShowSpecialUI(false);
			end)
		local endMission=voteMap.transform:Find("MissionSpecial/MissionList/MissionEpilogue");
		local endMissionBtn = endMission:GetComponent(typeof(CS.ExButton));
		endMissionBtn:AddOnClick(function()
				OPSPanelMissionBase.entranceId = 0;
				OPSPanelMissionBase.missionIds[0] = 11112;
				OPSPanelMissionBase.missionIds[1] = 11112;
				ShowMissionPanel();
				ShowSpecialUI(false);
			end)
		local vote=voteMap.transform:Find("MissionSpecial/MissionList/MissionVote");
		local voteBtn = vote:GetComponent(typeof(CS.ExButton));
		voteBtn:AddOnClick(function()
				RequestVoteData();
				--ShowVoto();
				ShowSpecialUI(false);
			end);
	end
	if returnobj == nil or returnobj:isNull() then
		returnobj= CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/Bikini_2022_Return"), opsControl.leftMain, false);
		local btnReturn = returnobj:GetComponent(typeof(CS.ExButton));
		btnReturn:AddOnClick(function()
				CS.CommonController.GotoScene("MissionSelection");
			end);
	end
	ShowSpine("Mission1");	
	ShowSpine("Mission2");
	ShowSpine("Mission3");
	ShowSpine("Mission4");
	ShowSpine("Mission5");
	ShowSpine("Mission6");
	ShowSpine("MissionSpecial");
	ShowSpine("MissionInfinite");
	CheckShowVoteResult();	
end

function CheckShowVoteResult()--显示对应解锁状态
	if  opsEnterTime>CS.GameData.GetCurrentTimeStamp() then
		return;
	end
	print("直接显示最终结果"..opsEnterTime);--显示投票结果
	RequestVoteData();
end
function ShowSpine(name)--小人显示
	local missionid = 0;
	local showSpine = false;
	local showTitle = false;
	local showTip = false;
	local isbattle = false;
	local battleMissionId = 0;
	if CS.GameData.missionAction ~= nil then
		battleMissionId = CS.GameData.missionAction.missionInfo.id;
	end
	local MissionTrans = voteMap.transform:Find(name);
	if name == "Mission1" then
		missionid = 11115;
		if battleMissionId == missionid then
			isbattle = true;
		end 
	elseif name == "Mission2" then		
		missionid = opsControl:GetCurrentMissionId(1110700);
		if battleMissionId == missionid then
			isbattle = true;
		end 	
	elseif name == "Mission3" then
		if CS.OPSPanelController.difficulty == 0 then
			missionid = 11103;
		else
			missionid =11104;
		end
		if battleMissionId == 11103 or battleMissionId == 11104 then
			isbattle = true;
		end 
	elseif name == "Mission4" then
		if CS.OPSPanelController.difficulty == 0 then
			missionid = 11105;
		else
			missionid =11106;
		end
		if battleMissionId == 11105 or battleMissionId == 11106 then
			isbattle = true;
		end 
	elseif name == "Mission5" then
		if CS.OPSPanelController.difficulty == 0 then
			missionid = 11101;
		else
			missionid =11102;
		end
		if battleMissionId == 11101 or battleMissionId == 11102 then
			isbattle = true;
		end 
	elseif name == "Mission6" then
		if CS.OPSPanelController.difficulty == 0 then
			missionid = 11099;
		else
			missionid =11100;
		end
		if battleMissionId == 11099 or battleMissionId == 11100 then
			isbattle = true;
		end 
	elseif name == "MissionInfinite" then
		if CS.OPSPanelController.difficulty == 0 then
			missionid =11113;
		else
			missionid =11114;
		end	
		if battleMissionId == 11113 or battleMissionId == 11114 then
			isbattle = true;
		end 
	elseif name == "MissionSpecial" then
		local mission0 = CS.GameData.listMission:GetDataById(11098);
		local mission1 = CS.GameData.listMission:GetDataById(11112);
		local checkmission0 = mission0 ~= nil and mission0.winCount == 0;
		local checkmission1 = mission1 ~= nil and mission1.winCount == 0;
		local check = false;
		local check0 = CheckMissionkey(1109900);
		local check1 = CheckMissionkey(1110100);
		local check2 = CheckMissionkey(1110300);
		local check3 = CheckMissionkey(1110500);
		local check4 = CheckMissionkey(1110700);
		local check5 = CheckMissionkey(1111500);
		if 	check0 or check1 or check2 or check3 or check4 or check5 then
			if CS.UnityEngine.PlayerPrefs.GetInt("-52-7-1",0) == 0 then
				check = true;
			end
		end
		showSpine = true;
		if checkmission0 or checkmission1 or check then
			showTitle = false;
			MissionTrans:Find("Img_Bubble").gameObject:SetActive(true);
		else
			showTitle = true;
			MissionTrans:Find("Img_Bubble").gameObject:SetActive(false);
		end
	end
	if missionid ~= 0 then
		local mission = CS.GameData.listMission:GetDataById(missionid);
		showSpine = mission~=nil;
		showTitle = mission~=nil;
		if mission~=nil and mission.UseWinCounter == 0 then
			showTip = true;
		end		
	end	
	local spineHolder = MissionTrans:Find("SpineHolder");
	if spineHolder~= nil then
		if showSpine then
			spineHolder:GetChild(0).gameObject:SetActive(true);
			local skeletonAnimation = spineHolder:GetChild(0):GetComponent(typeof(CS.SkeletonAnimation));
			skeletonAnimation.state:SetAnimation(0, "wait", true);	
		else
			spineHolder:GetChild(0).gameObject:SetActive(false);
		end
	end
	local title = MissionTrans:Find("Title");
	local tip = MissionTrans:Find("Title/Img_Tips");
	if showTitle then
		title.gameObject:SetActive(true);
		if name == "MissionInfinite" then
			MissionTrans.gameObject:SetActive(true);
		end
		tip.gameObject:SetActive(showTip);
	else
		title.gameObject:SetActive(false);
		if name == "MissionInfinite" then
			MissionTrans.gameObject:SetActive(false);
		end
	end
	local battleTip = MissionTrans:Find("Title/Battle");
	if battleTip ~= nil then
		battleTip.gameObject:SetActive(isbattle);
	end
end

function CloseMissionPanel()
	local background = voteMap.transform:Find("MissionInfoBG");
	background.gameObject:SetActive(false);
	opsControl.MissionInfoController.gameObject:SetActive(false);
end

function ShowMissionPanel()--显示关卡界面
	if OPSPanelMissionBase.CurrentMissionId == 0 then
		return;
	end
	if OPSPanelMissionBase.currentMissionInfo == nil then
		print("missioninfolist缺少"..OPSPanelMissionBase.CurrentMissionId);
		CS.CommonController.LightMessageTips(CS.Data.GetLang(100045));
		return;
	end
	if OPSPanelMissionBase.currentMission == nil then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(100045));
		return;
	end
	CheckIconSeleect(true);
	local background = voteMap.transform:Find("MissionInfoBG");
	background.gameObject:SetActive(true);
	opsControl.MissionInfoController.gameObject:SetActive(true);
	opsControl.MissionInfoController:InitData(OPSPanelMissionBase);
	--opsControl.MissionInfoController.
end
function RequestVoteData()--获取投票数据
	CS.ConnectionController.CreateConnection("Event/bikiniVoteResult","",function(www)
			print("sucess");
			CheckVoteJson(www)
		end,function(www)
			print("false");
			end,false);	
end
readPlot = false;
function CheckVoteJson(www)
	local jsonData = CS.ConnectionController.DecodeAndMapJson(www.text);
	--print(jsonData:ToJson());
	local total1 = jsonData:GetValue("bikini_vote_type1_total");
	local total2 = jsonData:GetValue("bikini_vote_type2_total");
	local totalplayer1 = jsonData:GetValue("bikini_vote_with_user"):GetValue("type1");
	local totalplayer2 = jsonData:GetValue("bikini_vote_with_user"):GetValue("type2");
	
	for i=1,#gunCode do
		local target = "target_"..tostring(i);
		--print(target);
		voteList[i][1]=total1:GetValue(target).Int;
		voteList[i][2]=total2:GetValue(target).Int;
		voteList[i][3]=totalplayer1:GetValue(target).Int;
		voteList[i][4]=totalplayer2:GetValue(target).Int;
	end	
	if  opsEnterTime>CS.GameData.GetCurrentTimeStamp() then
		ShowVoto();
		if CS.ConfigData.playReplay then
			ShowPlot("-52-7-1");
		else
			local check = CS.UnityEngine.PlayerPrefs.GetInt("-52-7-1",0);
			if check == 0 then
				ShowPlot("-52-7-1");
			end
		end
	else	
		ShowVotoResult();
		local check = CS.UnityEngine.PlayerPrefs.GetInt("-52-e-1",0);
		if check == 0 then
			ShowPlot("-52-e-1");
		end
	end
end
local VoteResult = nil;
function  ShowVotoResult()
	if VoteResult == nil or VoteResult:isNull() then
		VoteResult = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2022BikiniResult"), opsControl.leftMain, false);
		local btnReturn = VoteResult.transform:Find("Top/Btn_Back"):GetComponent(typeof(CS.ExButton));
		btnReturn:AddOnClick(function()
			CS.CommonController.GotoScene("Home");
		end);
		local btnShowPlot = VoteResult.transform:Find("Main/Scroll/List/First/Btn_Review"):GetComponent(typeof(CS.ExButton));
		btnShowPlot:AddOnClick(function()
			ShowPlot("-52-e-1");	
			end);	
		local itemParent = VoteResult.transform:Find("Main/Scroll/List/Grid");
		for i=2,#voteList do
			if itemParent.childCount<=(i-2) then
				CS.UnityEngine.Object.Instantiate(itemParent.transform:GetChild(0).gameObject,itemParent,false);					
			end		
		end
	end
	opsControl.btnTitleTrans.gameObject:SetActive(false);
	local votelistNew = {};
	for i=1,#voteList do
		table.insert(votelistNew,voteList[i]);
	end
	table.sort(votelistNew,function (a,b)
		return (a[1]+a[2])>(b[1]+b[2]);
	end)
	local firstpicTrans = VoteResult.transform:Find("Main/Scroll/List/First/GunHolder");
	if firstpicTrans.childCount>0 then
		CS.UnityEngine.Object.DestroyImmediate(firstpicTrans:GetChild(0).gameObject);
	end
	local pic = CS.CommonController.LoadSmallPic(votelistNew[1][5],firstpicTrans,CS.UnityEngine.Vector2.zero,votelistNew[1][7],nil);
	pic:SwitchDamaged(false);
	local txtRole = VoteResult.transform:Find("Main/Scroll/List/First/Text_Role"):GetComponent(typeof(CS.ExText));
	txtRole.text =  CS.Data.GetLang(votelistNew[1][10]);
	local imageRole = VoteResult.transform:Find("Main/Scroll/List/First/Img_Role"):GetComponent(typeof(CS.ExImage));
	local spriteholder = imageRole.transform:GetComponent(typeof(CS.UGUISpriteHolder));
	imageRole.sprite = spriteholder.listSprite[votelistNew[1][11]];
	local txtName =VoteResult.transform:Find("Main/Scroll/List/First/Text_Name"):GetComponent(typeof(CS.ExText));
	txtName.text = CS.GameData.listGunInfo:GetDataById(votelistNew[1][6]).name;
	local txtTotal =VoteResult.transform:Find("Main/Scroll/List/First/Text_TotalVotesNum"):GetComponent(typeof(CS.ExText));
	txtTotal.text = tostring(votelistNew[1][1]+votelistNew[1][2]);
	local txtGood =VoteResult.transform:Find("Main/Scroll/List/First/Text_GoodyVotesNum"):GetComponent(typeof(CS.ExText));
	txtGood.text = tostring(votelistNew[1][1]);
	local txtBad =VoteResult.transform:Find("Main/Scroll/List/First/Text_BaddyVotesNum"):GetComponent(typeof(CS.ExText));
	txtBad.text = tostring(votelistNew[1][2]);
	if votelistNew[1][1] >= votelistNew[1][2] then
		txtGood.color = CS.UnityEngine.Color(222/255,239/255,5/255,1);
		txtBad.color = CS.UnityEngine.Color(255/255,255/255,255/255,1);
	else
		txtGood.color = CS.UnityEngine.Color(255/255,255/255,255/255,1);
		txtBad.color = CS.UnityEngine.Color(238/255,51/255,0/255,1);		
	end
	local itemParent1 = VoteResult.transform:Find("Main/Scroll/List/Grid");
	for i=2,#votelistNew do
		local item = itemParent1:GetChild(i-2);
		local picTrans = item:Find("GunHolder");
		if picTrans.childCount>0 then
			CS.UnityEngine.Object.DestroyImmediate(picTrans:GetChild(0).gameObject);
		end
		local pic1 = CS.CommonController.LoadSmallPic(votelistNew[i][5],picTrans,CS.UnityEngine.Vector2.zero,votelistNew[i][7],nil);
		pic1:SwitchDamaged(false);
		local txtName1 =item:Find("Text_Name"):GetComponent(typeof(CS.ExText));
		local gunifId = votelistNew[i][6];
		local guninfo = CS.GameData.listGunInfo:GetDataById(gunifId);
		txtName1.text = guninfo.name;
		local good = votelistNew[i][1];
		local bad = votelistNew[i][2];
		local txtRole1 = item:Find("Text_Role"):GetComponent(typeof(CS.ExText));
		txtRole1.text = CS.Data.GetLang(votelistNew[i][10]);
		local imageRole1 = item:Find("Img_Role"):GetComponent(typeof(CS.ExImage));
		imageRole1.sprite = spriteholder.listSprite[votelistNew[i][11]];
		local txtTotal =item:Find("Text_TotalVotesNum"):GetComponent(typeof(CS.ExText));
		txtTotal.text = tostring(good+bad);
		local txtGood =item:Find("Text_GoodyVotesNum"):GetComponent(typeof(CS.ExText));
		txtGood.text = tostring(good);
		local txtBad =item:Find("Text_BaddyVotesNum"):GetComponent(typeof(CS.ExText));
		txtBad.text = tostring(bad);
		if good>= bad then
			txtGood.color = CS.UnityEngine.Color(222/255,239/255,5/255,1);
			txtBad.color = CS.UnityEngine.Color(255/255,255/255,255/255,1);
		else
			txtGood.color = CS.UnityEngine.Color(255/255,255/255,255/255,1);
			txtBad.color = CS.UnityEngine.Color(238/255,51/255,0/255,1);		
		end
	end
end
function  ShowPlot(txt)--显示复盘剧情
	local txtAVG = CS.ResManager.GetObjectByPath("AVGTxt/"..txt, ".txt");
	if txtAVG == nil then		
		CS.NDebug.LogError("剧本不存在");
		return;
	end
	CS.UnityEngine.PlayerPrefs.SetInt(txt,1);
	CS.UnityEngine.PlayerPrefs.Save();
	CS.AVGController.Instance.transform:SetParent(CS.CommonController.MainCanvas.transform, false);
	CS.AVGController.Instance:InitializeData(txtAVG);
end
local currentOrder = 1;
local VoteDeail = nil;
function CloseVotoDetail()
	VoteDeail.gameObject:SetActive(false);
end
function OpenVotoDetail(order)--点击显示投票界面
	currentOrder = order;
	if VoteDeail == nil or VoteDeail:isNull() then
		VoteDeail= CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2022BikiniVoteDetail"), opsControl.leftMain, false);
		local btnBack = VoteDeail.transform:Find("Top/Btn_Back"):GetComponent(typeof(CS.ExButton));
		btnBack:AddOnClick(CloseVotoDetail);
		local btnVoteGood = VoteDeail.transform:Find("Btn_Goody"):GetComponent(typeof(CS.ExButton));
		btnVoteGood:AddOnClick(OnClickVoteGood);
		local btnVoteBad = VoteDeail.transform:Find("Btn_Baddy"):GetComponent(typeof(CS.ExButton));
		btnVoteBad:AddOnClick(OnClickVoteBad);		
	end
	VoteDeail.gameObject:SetActive(true);
	local gunHolder = VoteDeail.transform:Find("Gunholder");
	if gunHolder.childCount>0 then
		CS.UnityEngine.Object.DestroyImmediate(gunHolder:GetChild(0).gameObject);
	end
	local gunifId = voteList[order][6];
	local guninfo = CS.GameData.listGunInfo:GetDataById(gunifId);
	CS.CommonController.Invoke(function()
		local pic = CS.CommonController.LoadBigPic(guninfo,gunHolder,voteList[order][7],false,nil);
		pic:SwitchDamaged(false);
		end,0.1,CS.OPSPanelController.Instance);
	--local pic = CS.CommonController.LoadBigPic(guninfo,gunHolder,voteList[order][7],false,nil);
	--pic:SwitchDamaged(false);
	local txtGunName = VoteDeail.transform:Find("Text_Name"):GetComponent(typeof(CS.ExText));
	txtGunName.text=guninfo.name;
	RefreshVotoDetailUI(order,false);
end
function RefreshVotoDetailUI(order,showdialog)
	local txtVoteNum = VoteDeail.transform:Find("Text_VoteNum"):GetComponent(typeof(CS.ExText));
	txtVoteNum.text = voteList[order][1]+voteList[order][2];
	local txtVoteGoodNum = VoteDeail.transform:Find("Btn_Goody/Text_VoteNum"):GetComponent(typeof(CS.ExText));
	txtVoteGoodNum.text = voteList[order][1];
	local txtVoteBadNum = VoteDeail.transform:Find("Btn_Baddy/Text_VoteNum"):GetComponent(typeof(CS.ExText));
	txtVoteBadNum.text = voteList[order][2];
	local txtGoodNum = VoteDeail.transform:Find("Top/GoodyItem/Text_GoodyItemNum"):GetComponent(typeof(CS.ExText));
	txtGoodNum.text = CS.GameData.GetItem(9013);
	local txtBadNum = VoteDeail.transform:Find("Top/BaddyItem/Text_BaddyItemNum"):GetComponent(typeof(CS.ExText));
	txtBadNum.text =CS.GameData.GetItem(9014);
	local dialague = VoteDeail.transform:Find("Dialogue");
	dialague.gameObject:SetActive(showdialog);
	if voteList[order][3] >0 then
		VoteDeail.transform:Find("Btn_Goody/Img_VotedBG").gameObject:SetActive(true);
		local txtgood = VoteDeail.transform:Find("Btn_Goody/Img_VotedBG/Text_PlayerVoteNum"):GetComponent(typeof(CS.ExText));
		txtgood.text = voteList[order][3];
	else
		VoteDeail.transform:Find("Btn_Goody/Img_VotedBG").gameObject:SetActive(false);
	end
	if voteList[order][4] >0 then
		VoteDeail.transform:Find("Btn_Baddy/Img_VotedBG").gameObject:SetActive(true);
		local txtgood = VoteDeail.transform:Find("Btn_Baddy/Img_VotedBG/Text_PlayerVoteNum"):GetComponent(typeof(CS.ExText));
		txtgood.text = voteList[order][4];
	else
		VoteDeail.transform:Find("Btn_Baddy/Img_VotedBG").gameObject:SetActive(false);
	end
end
function OnClickVoteGood()
	if CS.GameData.GetItem(9013) == 0 then
		local name = CS.GameData.listItemInfo:GetDataById(9013).name;
		local text = CS.System.String.Format(CS.Data.GetLang(60072),name)
		CS.CommonController.LightMessageTips(text);
		return;
	end
	ShowVotoBox(true);
end
function OnClickVoteBad()
	if CS.GameData.GetItem(9014) == 0 then
		local name = CS.GameData.listItemInfo:GetDataById(9014).name;
		local text = CS.System.String.Format(CS.Data.GetLang(60072),name)
		CS.CommonController.LightMessageTips(text);
		return;
	end
	ShowVotoBox(false);
end
local votobox = nil;
votoNum = 1;
local currentgood = false;
function ShowVotoBox(good)
	votoNum = 1;
	currentgood = good; 
	if votobox == nil or votobox:isNull() then
		votobox= CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2022BikiniVoteBox"), opsControl.leftMain, false);
		local btnClose = votobox.transform:Find("Main/Btn_Cancel"):GetComponent(typeof(CS.ExButton));
		btnClose:AddOnClick(function()
				votobox:SetActive(false);
			end);
		local btnComfirm = votobox.transform:Find("Main/Btn_Confirm"):GetComponent(typeof(CS.ExButton));
		btnComfirm:AddOnClick(function()
				RequestVote();
			end);
		local btnAdd = votobox.transform:Find("Main/btnAdd"):GetComponent(typeof(CS.ExButton));
		btnAdd:AddOnClick(function()
				votoNum =votoNum +1;
				if currentgood then
					votoNum = CS.Mathf.Min(votoNum,CS.GameData.GetItem(9013));
				else
					votoNum = CS.Mathf.Min(votoNum,CS.GameData.GetItem(9014));
				end
				RefreshVotoBoxUI();
			end);
		local btnReduce = votobox.transform:Find("Main/btnReduce"):GetComponent(typeof(CS.ExButton));
		btnReduce:AddOnClick(function()
				votoNum =votoNum -1;
				if votoNum == 0 then
					if currentgood then
						votoNum = CS.GameData.GetItem(9013);
					else
						votoNum = CS.GameData.GetItem(9014);
					end
				end
				RefreshVotoBoxUI();
			end);
	end
	votobox:SetActive(true);
	RefreshVotoBoxUI();
end
function RefreshVotoBoxUI()
	local txtTitle = votobox.transform:Find("Main/Text_Introduction"):GetComponent(typeof(CS.ExText));
	local gunifId = voteList[currentOrder][6];
	local txt0 = CS.GameData.listGunInfo:GetDataById(gunifId).name;
	local itemid = 9013;
	if not currentgood then
		itemid = 9014;
	end
	--print(votoNum);
	local txt1 = CS.GameData.listItemInfo:GetDataById(itemid).name.."x"..tostring(votoNum);	
	txtTitle.text=tostring(CS.System.String.Format(CS.Data.GetLang(60312),txt0,txt1));
	local txtShowNum = votobox.transform:Find("Main/InputField/PlaceHolder"):GetComponent(typeof(CS.ExText));
	txtShowNum.text = tostring(votoNum).."/"..tostring(CS.GameData.GetItem(itemid));
	local txt2 = CS.GameData.listItemInfo:GetDataById(itemid).name.."x"..tostring(CS.GameData.GetItem(itemid));		
	local txtItemNum = votobox.transform:Find("Main/Text_Items"):GetComponent(typeof(CS.ExText));
	txtItemNum.text = tostring(CS.System.String.Format(CS.Data.GetLang(60313),txt2));
end
function RequestVote()--投票请求
	local sb = CS.System.Text.StringBuilder();
	local writer = CS.LitJson.JsonWriter(sb);
	writer:WriteObjectStart();
	writer:WritePropertyName("type");
	if currentgood then
		writer:Write(1);
	else
		writer:Write(2);
	end
	writer:WritePropertyName("target");
	writer:Write(currentOrder);
	writer:WritePropertyName("num");
	writer:Write(votoNum);
	writer:WriteObjectEnd();
	CS.ConnectionController.CreateConnection("Event/bikiniVote","",sb,function(www)
			print("sucess");
			ResuestResult(www,votoNum);						
		end,nil,false);
end
function ResuestResult(www,num)--投票结果
	local jsonData = CS.ConnectionController.DecodeAndMapJson(www.text);
	--print(jsonData:ToJson());
	votobox:SetActive(false);
	if currentgood then
		local resnum = CS.GameData.GetItem(9013)-num;
		CS.GameData.SetItem(9013, resnum);
	else
		local resnum = CS.GameData.GetItem(9014)-num;
		CS.GameData.SetItem(9014, resnum);		
	end
	local txtVoteGoodNum = VoteDeail.transform:Find("Top/GoodyItem/Text_GoodyItemNum"):GetComponent(typeof(CS.ExText));
	txtVoteGoodNum.text = CS.GameData.GetItem(9013);
	local txtVoteBadNum = VoteDeail.transform:Find("Top/BaddyItem/Text_BaddyItemNum"):GetComponent(typeof(CS.ExText));
	txtVoteBadNum.text = CS.GameData.GetItem(9014);
	local dialague = VoteDeail.transform:Find("Dialogue");
	local txtdialague = VoteDeail.transform:Find("Dialogue/Text_Dialogue"):GetComponent(typeof(CS.ExText)); 	
	if currentgood then
		voteList[currentOrder][1] = voteList[currentOrder][1]+num;
		voteList[currentOrder][3] = voteList[currentOrder][3]+num;
		txtdialague.text = CS.Data.GetLang(voteList[currentOrder][8]);
	else
		voteList[currentOrder][2] = voteList[currentOrder][2]+num;
		voteList[currentOrder][4] = voteList[currentOrder][4]+num;
		txtdialague.text = CS.Data.GetLang(voteList[currentOrder][9]);		
	end
	RefreshVotoDetailUI(currentOrder,true);
	local txtGoodNum = votePanel.transform:Find("Top/GoodyItem/Text_GoodyItemNum"):GetComponent(typeof(CS.ExText));
	txtGoodNum.text = CS.GameData.GetItem(9013);
	local txtBadNum = votePanel.transform:Find("Top/BaddyItem/Text_BaddyItemNum"):GetComponent(typeof(CS.ExText));
	txtBadNum.text =CS.GameData.GetItem(9014);
end
function CloseVoto()--关闭立绘列表界面
	votePanel:SetActive(false);
	--opsControl.transform:Find("Top").gameObject:SetActive(true);
end
function ShowVoto()--显示立绘列表界面
	opsControl.transform:Find("Top").gameObject:SetActive(false);
	if votePanel == nil or votePanel:isNull() then
		votePanel= CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2022BikiniVote"), opsControl.leftMain, false);
		local upTrans = votePanel.transform:Find("GunList/Scroll/List/ListUp");
		local downTrans = votePanel.transform:Find("GunList/Scroll/List/ListDown");
		local btnBack = votePanel.transform:Find("Top/Btn_Back"):GetComponent(typeof(CS.ExButton));
		btnBack:AddOnClick(CloseVoto);	
		local btnTip = votePanel.transform:Find("GunList/Btn_Tips"):GetComponent(typeof(CS.ExButton));
		local txtNoteTip = votePanel.transform:Find("GunList/Btn_Tips/Text_Tips"):GetComponent(typeof(CS.ExText));
		local txtTip = votePanel.transform:Find("GunList/Btn_Tips/URL"):GetComponent(typeof(CS.ExText));
		txtNoteTip.text = CS.Data.GetLang(60349);
		btnTip:AddOnClick(function()
			opsControl:OpenAnnouncement(txtTip.text);
			--CS.CommonController.ShowRuleBox(CS.Data.GetLang(60368),opsControl.transform);	
			end);
		for i=1,#gunCode do
			local order = i-1;
			local check = order-order%2;			
			if order%2 == 0 then
				if upTrans.childCount<=check then
					CS.UnityEngine.Object.Instantiate(upTrans.transform:GetChild(0).gameObject,upTrans,false);					
				end
			else
				if downTrans.childCount<=check then
					CS.UnityEngine.Object.Instantiate(downTrans.transform:GetChild(0).gameObject,downTrans,false);					
				end		
			end
		end	
		local tex = CS.ResManager.GetObjectByPath("AtlasClips2090/卡牌用的裤子图",".png");	
		for i=1,#gunCode do
			local order = i-1;
			local check = order-order%2;	
			local code = voteList[i][5];
			local gunifId = voteList[i][6];
			local guninfo = CS.GameData.listGunInfo:GetDataById(gunifId);
			local skinid = voteList[i][7];		 		
			if order%2 == 0 then
				local item= upTrans:GetChild(check/2);
				local picTrans = item:Find("SettlementCard/GunHolder");
				local pic = CS.CommonController.LoadSmallPic(code,picTrans,CS.UnityEngine.Vector2.zero,skinid,nil);
				pic:SwitchDamaged(false);
				pic.ArrMat:SetTexture("_AlphaTex",tex);
				pic.transform.localScale = CS.UnityEngine.Vector3(0.9,0.9,1);
				local btn = item:Find("Btn_touchArea"):GetComponent(typeof(CS.ExButton));
				btn:AddOnClick(function()
						OpenVotoDetail(i);
					end);
				local txtName = item:Find("SettlementCard/Rollingtext_gunname/Tex_GunName"):GetComponent(typeof(CS.ExText));
				txtName.text = guninfo.name;
			else
				local item= downTrans:GetChild(check/2);
				local picTrans = item:Find("SettlementCard/GunHolder");
				local pic = CS.CommonController.LoadSmallPic(code,picTrans,CS.UnityEngine.Vector2.zero,skinid,nil);
				pic:SwitchDamaged(false);
				pic.ArrMat:SetTexture("_AlphaTex",tex);
				pic.transform.localScale = CS.UnityEngine.Vector3(0.9,0.9,1);
				local btn = item:Find("Btn_touchArea"):GetComponent(typeof(CS.ExButton));
				btn:AddOnClick(function()
						OpenVotoDetail(i);
					end);
				local txtName = item:Find("SettlementCard/Rollingtext_gunname/Tex_GunName"):GetComponent(typeof(CS.ExText));
				txtName.text = guninfo.name;
			end
		end	
	end
	votePanel:SetActive(true);
	local upTrans1 = votePanel.transform:Find("GunList/Scroll/List/ListUp");
	local downTrans1 = votePanel.transform:Find("GunList/Scroll/List/ListDown");
	for i=1,#gunCode do
		local order = i-1;
		local check = order-order%2;
		local goodNum = voteList[i][1];
		local badNum=voteList[i][2];
		if order%2 == 0 then
			local item= upTrans1:GetChild(check/2);
			local txtNum = item:Find("SettlementCard/VoteNum/Text_Num"):GetComponent(typeof(CS.ExText));
			txtNum.text=goodNum+badNum;
			local goodTrans = item:Find("SettlementCard/VotePercentage/Goody");
			local badTrans = item:Find("SettlementCard/VotePercentage/Baddy");
			if goodNum>=badNum then
				goodTrans.gameObject:SetActive(true);
				badTrans.gameObject:SetActive(false);
				local txtVoteNum = goodTrans:Find("Text_Percentage"):GetComponent(typeof(CS.ExText));
				local total =goodNum+badNum;
				if total ~= 0 then
					txtVoteNum.text = string.format("%0.1f", goodNum/(goodNum+badNum)*100).."%";
				else
					txtVoteNum.text = "50%";
				end
			else
				goodTrans.gameObject:SetActive(false);
				badTrans.gameObject:SetActive(true);
				local txtVoteNum = badTrans:Find("Text_Percentage"):GetComponent(typeof(CS.ExText));
				local total =goodNum+badNum;
				if total ~= 0 then
					txtVoteNum.text = string.format("%0.1f", badNum/(goodNum+badNum)*100).."%";
				else
					txtVoteNum.text = "50%";
				end
			end
		else
			local item= downTrans1:GetChild(check/2);
			local txtNum = item:Find("SettlementCard/VoteNum/Text_Num"):GetComponent(typeof(CS.ExText));
			txtNum.text=goodNum+badNum;
			local goodTrans = item:Find("SettlementCard/VotePercentage/Goody");
			local badTrans = item:Find("SettlementCard/VotePercentage/Baddy");
			if goodNum>=badNum then
				goodTrans.gameObject:SetActive(true);
				badTrans.gameObject:SetActive(false);
				local txtVoteNum = goodTrans:Find("Text_Percentage"):GetComponent(typeof(CS.ExText));
				local total =goodNum+badNum;
				if total ~= 0 then
					txtVoteNum.text = string.format("%0.1f", goodNum/(goodNum+badNum)*100).."%";
				else
					txtVoteNum.text = "50%";
				end
			else
				goodTrans.gameObject:SetActive(false);
				badTrans.gameObject:SetActive(true);
				local txtVoteNum = badTrans:Find("Text_Percentage"):GetComponent(typeof(CS.ExText));
				local total =goodNum+badNum;
				if total ~= 0 then
					txtVoteNum.text = string.format("%0.1f", badNum/(goodNum+badNum)*100).."%";
				else
					txtVoteNum.text = "50%";
				end
			end
		end
	end
	local txtGoodNum = votePanel.transform:Find("Top/GoodyItem/Text_GoodyItemNum"):GetComponent(typeof(CS.ExText));
	txtGoodNum.text = CS.GameData.GetItem(9013);
	local txtBadNum = votePanel.transform:Find("Top/BaddyItem/Text_BaddyItemNum"):GetComponent(typeof(CS.ExText));
	txtBadNum.text =CS.GameData.GetItem(9014);
end

local clearCount = 0;
local allCount = 18;
function CheckMission(missionId)
	local mission = CS.GameData.listMission:GetDataById(missionId);
	if mission ~= nil and mission.UseWinCounter>0 then
		clearCount = clearCount + 1;
	end
end 

local ShowProcess = function(self)
	if self.campaionId == -52 then
		if self.processTxt ~= nil then
			clearCount = 0;
			CheckMission(11098);
			CheckMission(11099);
			CheckMission(11100);
			CheckMission(11101);
			CheckMission(11102);
			CheckMission(11103);
			CheckMission(11104);
			CheckMission(11105);
			CheckMission(11106);
			CheckMission(11107);
			CheckMission(11108);
			CheckMission(11109);
			CheckMission(11110);
			CheckMission(11111);
			CheckMission(11112);
			CheckMission(11113);
			CheckMission(11114);
			CheckMission(11115);
			self.processTxt.text = CS.Data.GetLang(30251)..tostring(clearCount).."/"..tostring(allCount);
		end
		return;
	end
	self:ShowProcess();	
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

local RefreshItemNum = function(self)
	if CS.OPSPanelController.showItemId == nil then
		return;
	end
	self:RefreshItemNum();
end

util.hotfix_ex(CS.OPSPanelController,'InitClockSelect',InitClockSelect)
util.hotfix_ex(CS.OPSPanelController,'ShowContainerReturn',ShowContainerReturn)
util.hotfix_ex(CS.OPSPanelController,'CheckCurrentAngle',CheckCurrentAngle)
util.hotfix_ex(CS.OPSPanelController,'PlayTime',PlayTime)
util.hotfix_ex(CS.OPSPanelController,'ShowClockTime',ShowClockTime)
util.hotfix_ex(CS.OPSPanelController,'Awake',Awake)
util.hotfix_ex(CS.OPSPanelController,'Start',Start)
util.hotfix_ex(CS.OPSPanelController,'ShowTip',ShowTip)
util.hotfix_ex(CS.OPSPanelController,'OpenRuler',OpenRuler)
util.hotfix_ex(CS.OPSPanelController,'ShowItemRuler',ShowItemRuler)
util.hotfix_ex(CS.OPSPanelController,'ReturnContainer',ReturnContainer)
util.hotfix_ex(CS.OPSPanelController,'CheckSpineSpot',CheckSpineSpot)
util.hotfix_ex(CS.OPSPanelController,'RefreshUI',RefreshUI)
util.hotfix_ex(CS.OPSPanelController,'CancelMission',CancelMission)
util.hotfix_ex(CS.OPSPanelController,'CheckIsolateSpots',CheckIsolateSpots)
util.hotfix_ex(CS.OPSPanelController,'LoadTime',LoadTime)
--util.hotfix_ex(CS.OPSPanelController,'LoadProcess',LoadProcess)
util.hotfix_ex(CS.OPSPanelController,'ShowAllLabel',ShowAllLabel)
util.hotfix_ex(CS.OPSPanelController,'SelectProcessInfo',SelectProcessInfo)
util.hotfix_ex(CS.OPSPanelController,'InitShowContainer',InitShowContainer)
util.hotfix_ex(CS.OPSPanelController,'SelectDiffcluty',SelectDiffcluty)
util.hotfix_ex(CS.OPSPanelController,'ShowProcess',ShowProcess)
util.hotfix_ex(CS.OPSPanelController,'RefreshItemNum',RefreshItemNum)