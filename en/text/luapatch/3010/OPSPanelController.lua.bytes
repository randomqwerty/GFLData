local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.OPSConfig)
xlua.private_accessible(CS.OPSPanelBackGround)
xlua.private_accessible(CS.CommonSceneManagerController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ExButton)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.OPSPanelConfig)
xlua.private_accessible(CS.OPSSpineMission)
xlua.private_accessible(CS.DeploymentController)
xlua.private_accessible(CS.OPSEventPrizeController)

local FindPanelMission = function(self)
	if CS.GameData.missionAction ~= nil then
		local missionid = CS.GameData.missionAction.missionInfo.id;
		for i=0,CS.OPSPanelBackGround.Instance.spotMissionHolders.Count-1 do
			local holder = CS.OPSPanelBackGround.Instance.spotMissionHolders[i];
			if holder.groupInfo ~= nil then
				if holder.groupInfo.missionids:Contains(missionid) then
					return holder;
				end
			elseif holder.opsMission ~= nil then
				local entranceId = holder.opsMission.entranceId;
				if entranceId ~= 0 then
					if CS.OPSConfig.missionEntranceInfos:ContainsKey(entranceId) then
						local info = CS.OPSConfig.missionEntranceInfos[entranceId];
						for j=0,info.missionids.Count-1 do
							for l=0,info.missionids[j].Count-1 do
								local id = info.missionids[j][l];
								if missionid == id then
									CS.OPSConfig.missionEntranceSelectOrder[entranceId] = j;
									CS.OPSConfig.missionEntranceSelectDiffcluty[entranceId] = l;
									return holder;
								end
							end		
						end
					end	
				else
					for j=0,holder.opsMission.missionIds.Count-1 do
						local id =holder.opsMission.missionIds[j];
						if missionid == id then
							CS.OPSPanelController.diffclutyRecord = j;
							CS.OPSPanelController.difficulty = j;
							return holder;
						end
					end
				end
			end
		end
	end
	return nil;
end

local SelectContainer = function(self,container,playanim)
	self:RefreshContainerUI();
	self.canvasContainerGroup.alpha = 1;
	self:SelectContainer(container,playanim);
end
local SelectModuleSpine = function(self,spinecontrol)
	print("选中小人"..spinecontrol.spinecode);
	self:CancelSelectMoudleSpine();
	self:SelectModuleSpine(spinecontrol);
end
local checkcode;
local ShowOPSSpineMissionUI = function(self,code)
	self:ShowOPSSpineMissionUI(code);
	if not self.currentPanelConfig.opsSpineMissions:ContainsKey(code) then
		return;
	end
	checkcode = code;
	print(code);
	local spineMission = self.currentPanelConfig.opsSpineMissions:get_Item(code);
	if not self.moudleSpineUIObj.gameObject.activeInHierarchy then
		local childItem = self.moudleSpineUIObj.transform:Find(self.currentPanelConfig.moudleSpineUI.itemPath);
		for i=0,childItem.parent.childCount-1 do
			if i> spineMission.opsMissions.Count then
				childItem.parent:GetChild(i).gameObject:SetActive(false);
			end
		end
		self.useOPSmissions:Clear();
		local trans = self.panalMissionTrans:GetEnumerator();
		while trans:MoveNext() do
			local key = trans.Current.Key;
			local value = trans.Current.Value;
			self:CheckOPSMissionItem(key,value);
			if key.currentMission ~= nil then
				self.useOPSmissions:Add(key);
			end
		end
		self.num = self.useOPSmissions.Count;
		self.checkPosMax = self.currentPanelConfig.moudleSpineUI.selectPosX;
		self.distance = self.currentPanelConfig.moudleSpineUI.eachDistance;
		self.moudleSpineUIObj.gameObject:SetActive(true);
	end
	self:CheckEndlessPoint();
	CS.CommonAudioController.PlayUI("UI_Train_Click");
end
local HideOPSSpineMissionUI = function(self)
	self:HideOPSSpineMissionUI();
	self:CheckEndlessPoint();
end
local CanGetPoint = function(self,itemid)
	if CS.MissionSelectionController.normalActivityCampaion:Contains(self.campaionId) then
		return true;
	end
	return self:CanGetPoint(itemid);
end
local myLoadReturn = function(self)
	if (CS.OPSConfig.Instance.OPSCamapionReturn:ContainsKey(self.campaionId)) then
		return self:LoadReturn();
	else
		local Obj = CS.ResManager.GetObjectByPath(string.format("Pics/ActivityMap/%s", CS.OPSConfig.Instance.OPSReturn));
		if (Obj ~= nil) then
			local returnObject = CS.UnityEngine.Object.Instantiate(Obj):GetComponent(typeof(CS.ExButton));
			returnObject.transform:SetParent(self.Top, false);
			returnObject.transform:SetAsLastSibling();
			returnObject:AddOnClickBack(function ()
					CS.OPSPanelBackGround.Instance:SaveRecord();
					CS.CommonSceneManagerController.instance:PopController();
					CS.CommonController.GotoScene("MissionSelection");
			end);
		end
	end
end

local noticeElse;
local CheckEndlessPoint = function(self)
	if self.campaionId == -54 then
		if self.moudleSpineUIObj ~= nil and self.moudleSpineUIObj.activeInHierarchy and checkcode == "NPC-TD_Porter"then
			self:CheckEndlessPoint();
			if self.highScoreObj ~= nil then
				self.highScoreObj:SetActive(true);
			end
			if self.highScoreTotalObj ~= nil then
				self.highScoreTotalObj:SetActive(true);
			end
			if noticeElse == nil then
				noticeElse = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/2022Summer_HoleNotice"), self.leftMain, false);	
				local txt = noticeElse.transform:Find("URL"):GetComponent(typeof(CS.ExText));
				local url = txt.text;
				local btn = noticeElse:GetComponent(typeof(CS.ExButton));
				btn:AddOnClick(function ()
					self:OpenAnnouncement(url);
				end);	
			end
			if noticeElse ~= nil and not noticeElse:isNull() then
				noticeElse:SetActive(true);
			end
		else
			if self.highScoreObj ~= nil then
				self.highScoreObj:SetActive(false);
			end
			if self.highScoreTotalObj ~= nil then
				self.highScoreTotalObj:SetActive(false);
			end
			if noticeElse ~= nil and not noticeElse:isNull() then
				noticeElse:SetActive(false);
			end
		end
	else
		self:CheckEndlessPoint();
	end
end

local CancelSelectMoudleSpine = function(self)
	self:CancelSelectMoudleSpine();
	self:CancelMission();
end

local CheckMoudleUiTween = function(self)
	local title = self.toggleTitle;
	self.toggleTitle = self.transform;
	self:CheckMoudleUiTween();
	self.toggleTitle = title;
end

local RefreshMoudleBuildUI = function(self)
	local missionnum = 0;
	local trans = self.panalMissionTrans:GetEnumerator();
	while trans:MoveNext() do
		local key = trans.Current.Key;
		local value = trans.Current.Value;		
		if key.currentMission ~= nil then
			self.missionBaseFinal = value;
			missionnum = missionnum+1;
		end
	end
	self.num = missionnum;
	self:RefreshMoudleBuildUI();	
end

local order = -1;
local CheckMoudleUi = function(self)
	if self.toggleTitle ~= nil then
		for i=0,self.currentPanelConfig.moudleMoveData.num do
			local child = self.toggleTitle:GetChild(i);
			local extoogle = child:GetComponent(typeof(CS.ExToggle));
			local check = i == CS.OPSPanelController.currentSelectOrder;
			extoogle:Switch(check);
			local active = self:CheckMoudleMissionTip(i);
			child:Find("Img_New").gameObject:SetActive(active);
		end
	end
	self:CheckMoudleUiTween();
	if order ~= CS.OPSPanelController.currentSelectOrder then
		order = CS.OPSPanelController.currentSelectOrder;
		CS.CommonAudioController.PlayUI("UI_Train_Switch");
	end
end

local CheckMoudleMissionTip = function(self,order)
	print(order.."检查对应车厢进度");
	for i=0,self.currentPanelConfig.opsBuildMissions.Count -1 do
		local buildMission = self.currentPanelConfig.opsBuildMissions[i];
		if buildMission.moudleIndex == order then
			--print(order.."missionid"..buildMission.opsMission.missionIds[0]);
			if buildMission.opsMission:HasUnBattleMission() then
				print("buildactive进度"..buildMission.opsMission.missionIds[0]);
				return true;
			end
		end
	end
	local trans = self.currentPanelConfig.opsSpineMissions:GetEnumerator();
	while trans:MoveNext() do
		local code = trans.Current.Key;
		local opsspineMission = trans.Current.Value;		
		if opsspineMission.moudleIndex == order then
			for i=0,opsspineMission.opsMissions.Count-1 do
				local opsMission = opsspineMission.opsMissions[i];
				if opsMission:HasUnBattleMission() then
					print("code"..code.."进度"..i);
					return true;
				end
			end
		end
	end
	return false;
end

local PlayMoudleBackgroundRailMove = function(self,trans)
	self:PlayMoudleBackgroundRailMove(trans);
	if self.leftrail ~= nil then
		self.leftrail:GetChild(0).gameObject:SetActive(false);
	end
end

function LoadStart()
	local bg = CS.UnityEngine.GameObject.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/2022SummerStart"));
	CS.OPSPanelController.Instance:SetCanvasLayerName(bg);
	bg.transform:SetParent(CS.OPSPanelController.Instance.module.transform, false);
end

local RefreshCurrentDiffcluty = function(self)
	for i=0,CS.OPSPanelController.diffcluteNum -1 do
		if self.btnTitleTrans ~= nil then
			local child = self.btnTitleTrans.transform:Find(tostring(i));
			if child ~= nil then
				child.gameObject:SetActive(i == CS.OPSPanelController.difficulty);
			end
		end
		if self.background ~= nil then
			local child = self.background.transform:Find("Change"..tostring(i));
			if child ~= nil then
				child.gameObject:SetActive(i == CS.OPSPanelController.difficulty);
			end
		end
	end
	self:HideAllLabel();
	self:CloseEchoInfo();
	self:RefreshUI();
	self:SetLightColor();
	self:CheckModelPos(true);
	self:ShowAllLabel();
	self:CheckMoudleUi();
	self:RefreshMoudleBuildUI();
	if self.MissionInfoController.gameObject.activeInHierarchy then
		if self.MissionInfoController.opsMission ~= nil then
			self.MissionInfoController:InitOPSMission(self.MissionInfoController.opsMission);
		else
			self:CancelMission();
		end
	end
end

local playtrain = false;
local PlayMoudleBackgroundMove = function(self,addspeed)
	local datetime = CS.GameData.UnixToDateTime(CS.GameData.GetCurrentTimeStamp());
	local day = datetime.Day;
	local check = CS.UnityEngine.PlayerPrefs.GetInt("moudleday",0);
	if check ~= day then
		CS.CommonAudioController.PlayUI("UI_Train_Leaving");
		CS.CommonController.Invoke(LoadStart,0.3,CS.OPSPanelController.Instance);
		self:PlayMoudleBackgroundMove(addspeed);
		CS.UnityEngine.PlayerPrefs.SetInt("moudleday",day);
		CS.UnityEngine.PlayerPrefs.Save();
	else
		if self.currentPanelConfig.moudleMoveBackgroundConfig.configs.Count == 2 then
			CS.OPSPanelController.backgroundOrder = 0;
			self.currentPanelConfig.moudleMoveBackgroundConfig.configs:RemoveAt(0);
		end
		if CS.AVGController.inst == nil or CS.AVGController.inst:isNull() then
			CS.CommonAudioController.PlayUI("UI_Train_Onrail");
			playtrain = true;
		else
			if playtrain then
				playtrain = false;
				CS.CommonAudioController.PlayUI("Stop_UI_loop");
			end
		end
		self:PlayMoudleBackgroundMove(addspeed);
	end
end

local CheckModuleSpine = function(self)
	if self.currentPanelConfig.moudleMoveData == nil then
		return;
	end
	local trans = self.currentPanelConfig.opsSpineMissions:GetEnumerator();
	while trans:MoveNext() do
		local code = trans.Current.Key;
		local opsspinemission = trans.Current.Value;		
		local currentIndex = opsspinemission:CheckMissionShowOrder();
		opsspinemission.currentOrder = currentIndex;
		local moduleControl = nil;
		for i=0,self.moduleControls.Count -1 do
			if self.moduleControls[i].gameObject.name == opsspinemission.moudleName then
				moduleControl = self.moduleControls[i];
				opsspinemission.moudleIndex = i;
			end
		end
		if spineMInfo[code] == nil then
			print(code.."MoudleSpineAIMission未配置");
		else
			print(code.."检查spineAI进度");
			local index = GetMissionIndex(spineMInfo[code]);
			index = CS.Mathf.Clamp(index,0,opsspinemission.opsSpineAI.Count - 1);
			print(code.."行为逻辑"..index);
			moduleControl:InitMoveSpine(code, opsspinemission.opsSpineAI[index]);
		end
	end
end
spineMInfo = {};
opsControl = nil;
endMissionIds = nil;
local Load = function(self,campaion)
	opsControl = self;
	self:Load(campaion);
	if self.currentPanelConfig ~= nil then
		CS.OPSPanelController.diffclutyRecord = CS.Mathf.Clamp(CS.OPSPanelController.diffclutyRecord,0,self.currentPanelConfig.diffclutyNum-1);
		CS.OPSPanelController.difficulty = CS.OPSPanelController.diffclutyRecord;
	end
	if campaion ~= -54 and campaion ~= -57 then
		return;
	end
	CS.OPSPanelController.currentSelectOrder = -1;
	personinfo = {};
	avgshowinfo = {};
	endMissionIds = CS.System.Collections.Generic.List(CS.System.Int32)();
	local textAsset = CS.ResManager.GetObjectByPath("ProfilesConfig/OPSPanel/Campion"..tostring(campaion), ".txt");
	if textAsset == nil then
		return;
	end
	local lineTxt = Split(textAsset.text,"\n");
	for i = 1, #lineTxt do
		local index = string.find(lineTxt[i],"/");
		if index == nil then
			local temp = Split(lineTxt[i],"|");
			if temp[1] == "ModuleSpineAIMission" then
				local code = temp[2];
				if not self.currentPanelConfig.opsSpineMissions:ContainsKey(code) then
					local opsspinemission = CS.OPSSpineMission();
					opsspinemission.spineCode = code;
					opsspinemission.moudleName = tostring(temp[3]);
					self.currentPanelConfig.opsSpineMissions:Add(code,opsspinemission);
				else
					local opsspinemission = self.currentPanelConfig.opsSpineMissions:get_Item(code);
					opsspinemission.spineCode = code;
					opsspinemission.moudleName = tostring(temp[3]);
				end
				local missiontxt = Split(temp[4],",");
				local opsmissions = CS.System.Collections.Generic.List(CS.OPSMission)();
				for j=1,#missiontxt do
					local mtxt = missiontxt[j];
					local missionid1 = tonumber(Split(mtxt,"-")[1]);
					local missionid2 = tonumber(Split(mtxt,"-")[2]);
					local missionid3 = tonumber(Split(mtxt,"-")[3]);
					local opsmission = CS.OPSMission();
					opsmission.missionIds:Add(missionid1);
					opsmission.missionIds:Add(missionid2);
					opsmission.missionIds:Add(missionid3);
					opsmissions:Add(opsmission);
				end
				print(code.."添加ModuleSpineAIMission")
				spineMInfo[code] = opsmissions;
			end
			if temp[1] == "MissionShowCondition" then	
				--print(lineTxt[i]);
				local mInfo = {};
				mInfo[1] = tonumber(temp[2]);--missionid
				mInfo[2] = GetList(temp[3]);--type,1-3
				mInfo[3] = GetList(temp[4]);--dayTime,1-4
				mInfo[4] = GetList(temp[5]);--stage,1-7
				mInfo[5] = GetMissionKeyListOr(temp[6]);--missionkey判断
				mInfo[6] = GetMissionKeyListOr(temp[7]);--itemid_num,先且后或
				mInfo[7] = GetMissionKeyListOr(temp[8]);--itemid_num,
				mInfo[8] = tonumber(temp[9]);--未解说语言包
				if mInfo[2]:Contains(3) then
					endMissionIds:Add(mInfo[1]);
				end
				--print("添加数据"..mInfo[1]);
				spotshowinfo[mInfo[1]] = mInfo;
			end
			if temp[1] == "MissionPersonUI" then
				local info = {};
				info[1] = tonumber(temp[2]);
				info[2] = GetList(temp[3]);
				table.insert(personinfo,info);		
			end
			if temp[1] == "MissionAvgShow" then
				local info = {};
				info[1] = tonumber(temp[2]);--missionid
				info[2] = temp[3];--avg
				info[3] = Split(temp[4],",");--Pic 
				info[4] = tonumber(temp[5]);--day
				info[5] = tonumber(temp[6]);--stage
				table.insert(avgshowinfo,info);
			end
		end
	end
end

function GetMissionIndex(opsmissions)
	local index = 0;
	local checkmissionid = 0;
	for i=0,opsmissions.Count-1 do
		local opsmission = opsmissions[i];
		for j=0,opsmission.missionIds.Count -1 do
			local missionid = opsmission.missionIds[j];
			local mission = CS.GameData.listMission:GetDataById(missionid);
			if mission ~= nil and mission.UseWinCounter>0 then
				index = i+1;
				checkmissionid = missionid;
			end
		end
	end
	print("最新AI关卡进度"..checkmissionid);
	return index;
end

local RefreshMoudleUI = function(self,spineMission)
	local txtName = self.moudleSpineUIObj.transform:Find("NamePlate/Tex_Name"):GetComponent(typeof(CS.ExText));
	txtName.text = CS.Data.GetLang(spineMission.codeName);
	local txtTip = self.moudleSpineUIObj.transform:Find("NamePlate/Tex_Name/Tex_Dialogue"):GetComponent(typeof(CS.ExText));
	local code = spineMission.spineCode;
	if spineMInfo[code] == nil then
		print(code.."MoudleSpineAIMission未配置");
		txtTip.text = "";
	else
		local index = GetMissionIndex(spineMInfo[code]);
		print(code.."当前index"..index);
		index = CS.Mathf.Clamp(index,0,spineMission.tips.Count - 1);
		print(code.."对应语言包"..spineMission.tips[index]);
		txtTip.text = CS.Data.GetLang(spineMission.tips[index]);
	end
end

local OpenRuler = function(self)
	if self.highScoreObj == nil then
		return;
	end
	local txt = self.highScoreObj.transform:Find("Main/Btn_Rule/URL"):GetComponent(typeof(CS.ExText));
	if not CS.System.String.IsNullOrEmpty(txt.text) then
		self:OpenAnnouncement(txt.text);
	else
		self.highScoreRule.gameObject:SetActive(true);
	end
end
local missionavgs = {};
local SuccessJsonHandleData = function(self,jsonData)
	self:SuccessJsonHandleData(jsonData);
	missionavgs = {}
	if jsonData:Contains("mission_avg") then
		local data = jsonData:GetValue("mission_avg");
		CS.NDebugJson.Log("mission_avg", data);
		if CS.Data.IsJsonArrayNull(data) then
			return;
		end
		local ids = CS.System.Collections.Generic.List(CS.System.String)(data.Keys);
		for i=0,ids.Count-1 do
			local temp = data:GetValue(ids[i]);
			local missionid = tonumber(ids[i]);
			missionavgs[missionid] = CS.System.Collections.Generic.List(CS.System.String)();
			local avg = temp:GetValue("avg").String;
			local avgs = Split(avg,",");
			for j=1,#avgs do
				missionavgs[missionid]:Add(avgs[j]);
			end
		end
	end
end

--local LoadTitle = function(self)
--	self:LoadTitle();
--	self:CheckConfigTip();
--end

local findSpot = true;
local RequestSetDrawEvent = function(self,data)
	findSpot = true;
	self:RefreshUI(false);
	self:CheckAnim();
	self:CheckModuleSpine();
	self:RefreshMoudleBuildUI();
	self:CheckMoudleUi();	
end
local GetAllGroupTotalHighScore = function(self)
	if self.campaionId == -54 then
		local mission = CS.GameData.listMission:GetDataById(11118);
		if mission ~= nil then
			return mission.type5_score;
		end
		return 0;
	end
	return self:GetAllGroupTotalHighScore();
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


spotshowinfo = {};
personinfo = {};
avgshowinfo = {};
currentSetType = 1;--当前类型
currentSetDay = 1;--自由行动当前天数
currentSetSatge = 1;--自由行动当前阶段 0代表1且2 5代表3且4 
startMissionkeyId = 1126100;
checkMissionkeyId = 1126200;
function CheckAllTypeStage()	
	if CurrentType() == 1 then
		--进入可切换界面
		currentSetType = 1;
	elseif CurrentType() == 3 then
		currentSetType = 3;
		currentSetDay = 8;
		currentSetSatge = 3;
	elseif CurrentType() == 4 then
		currentSetDay = CS.UnityEngine.PlayerPrefs.GetInt("currentSetDay",8);
		currentSetSatge = CS.UnityEngine.PlayerPrefs.GetInt("currentSetSatge",5);
		if currentSetDay>7 then
			currentSetType = 3;
		else
			currentSetType = 2;
		end	
	else
		--进入固定界面
		currentSetType = CurrentType();
		currentSetDay = CurrentDay();
		currentSetSatge = CurrentStage();
	end	
	Refresh57UI(false);
end
function Refresh57UI(check)
	print("Type"..currentSetType);
	print("day"..currentSetDay);
	print("Stage"..currentSetSatge);
	LoadMainUI();
	LoadStoryUI();
	LoadCapacityMap();
	opsControl:CheckSpecialAnim();
	CheckForceAvg();
	--CheckSpotsShow();
	CheckGuide();
	Checkbackground(check);
end
function Checkbackground(check)
	if opsControl.background3d ~= nil then
		local dayObj = opsControl.background3d.transform:Find("model/GameObject/Day");
		--local nightObj = opsControl.background3d.transform:Find("model/GameObject/Night");
		dayObj.gameObject:SetActive(true);
		--nightObj.gameObject:SetActive(currentSetSatge>2);
		local mat = dayObj:GetComponent(typeof(CS.UnityEngine.SpriteRenderer)).material;
		if currentSetDay == 7 then
			if check then
				mat:DOFloat(1, "_texlerp", 0.3);
				mat:DOFloat(0, "_texlerp", 0.3):SetDelay(0.3);
			else
				mat:DOFloat(0, "_texlerp", 0.3);
				--mat:SetFloat("_texlerp",0);
			end
		elseif currentSetDay == 8 then
			if check then
				mat:DOFloat(0, "_texlerp", 0.3);
				mat:DOFloat(1, "_texlerp", 0.3):SetDelay(0.3);
			else
				mat:DOFloat(1, "_texlerp", 0.3);
				--mat:SetFloat("_texlerp",1);
			end
		else
			if currentSetSatge>2 then
				if check then
					mat:DOFloat(0, "_texlerp", 0.3);
					mat:DOFloat(1, "_texlerp", 0.3):SetDelay(0.3);
				else
					mat:DOFloat(1, "_texlerp", 0.3);
					--mat:SetFloat("_texlerp",1);
				end
			else
				if check then
					mat:DOFloat(1, "_texlerp", 0.3);
					mat:DOFloat(0, "_texlerp", 0.3):SetDelay(0.3);
				else
					mat:DOFloat(0, "_texlerp", 0.3);
					--mat:SetFloat("_texlerp",0);
				end
			end
		end
	end
end
function CheckGuide()
	--序章通关
	if CurrentType() == 2 then
		local read = CS.UnityEngine.PlayerPrefs.GetInt("CampaionType2",0);
		if read == 0 then
			PlayGuide("CampaionType2");
		end
	end
	--第一次结局
	if CurrentType() == 4 then
		local read = CS.UnityEngine.PlayerPrefs.GetInt("CampaionType4",0);
		if read == 0 then
			PlayGuide("CampaionType4");
		end
	end
end

function PlayGuide(guidename)
	print("播放教程"..guidename);
	CS.UnityEngine.PlayerPrefs.SetInt(guidename,1);
	CS.UnityEngine.PlayerPrefs.Save();
	local textAsset = CS.ResManager.GetObjectByPath("ProfilesConfig/TutorialsConfig", ".txt");
	if textAsset == nil then
		return;
	end
	local datas = CS.System.Collections.Generic.List(CS.System.String)();
	local lineTxt = Split(textAsset.text,"\r\n");
	for i = 1, #lineTxt do
		local temp = Split(lineTxt[i],",");
		if temp[1] == guidename then
			for j=2,#temp do
				datas:Add(temp[j]);
			end
		end
	end
	CS.GriffinEntryMessageBoxController.OpenGuide(datas, CS.GuideType.End);
end
function CheckSpotsShow()
	for i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
		local spot = CS.OPSPanelBackGround.Instance.all3dSpots:GetDataByIndex(i);
		spot:Show();
	end
end
local mainUI = nil;
local sliderleft;
local sliderright;
local btnReast;
local btnShowRank;
local btnGuide;
function LoadMainUI()
	if mainUI == nil or mainUI:isNull() then
		mainUI = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/ZLSR_Time"), opsControl.leftMain, false);
		sliderleft = mainUI.transform:Find("Date/DateSlider"):GetComponent(typeof(CS.UnityEngine.UI.Slider));
		sliderleft.onValueChanged:AddListener(function(value)
			DragChangeDay(value);
		end)
		local dataParent = mainUI.transform:Find("Date/DateSlider/DateList");
		for i=0,dataParent.childCount-1 do
			local btn = dataParent:GetChild(i):GetComponent(typeof(CS.ExButton));
			btn:AddOnClick(function()
				DragChangeDay(i);
			end);
		end
		sliderright = mainUI.transform:Find("Time/TimeSlider"):GetComponent(typeof(CS.UnityEngine.UI.Slider));
		sliderright.onValueChanged:AddListener(function(value)
			DragChangeTime(value);
		end)
		local timeParent = mainUI.transform:Find("Time/TimeSlider/TimeList");
		for i=0,timeParent.childCount-1 do
			local btn = timeParent:GetChild(i):GetComponent(typeof(CS.ExButton));
			btn:AddOnClick(function()
					DragChangeTime(i);
				end);
		end
		btnReast = mainUI.transform:Find("Btn_Restart"):GetComponent(typeof(CS.ExButton));
		btnReast:AddOnClick(OnClickReast);
	end
	btnReast.gameObject:SetActive(ShowRestBtn());
	if currentSetDay<8 then
		if currentSetDay == 7 then
			mainUI.transform:Find("Time/TimeSlider").gameObject:SetActive(false);
			mainUI.transform:Find("Time/NightLocked").gameObject:SetActive(false);
			mainUI.transform:Find("Time/DayLocked").gameObject:SetActive(true);
			--mainUI.transform:Find("Time").gameObject:SetActive(currentSetSatge<3);
		else
			mainUI.transform:Find("Time/TimeSlider").gameObject:SetActive(true);
			mainUI.transform:Find("Time/NightLocked").gameObject:SetActive(false);
			mainUI.transform:Find("Time/DayLocked").gameObject:SetActive(false);
		end
	else
		mainUI.transform:Find("Time/TimeSlider").gameObject:SetActive(false);
		mainUI.transform:Find("Time/NightLocked").gameObject:SetActive(true);
		mainUI.transform:Find("Time/DayLocked").gameObject:SetActive(false);
	end
	if CurrentType() == 4 then
		mainUI.gameObject:SetActive(true);
		mainUI.transform:Find("Date/DateSlider/Fill_Area").gameObject:SetActive(false);
		sliderleft.interactable = true;
		sliderright.interactable = true;		
	else
		mainUI.transform:Find("Date/DateSlider/Fill_Area").gameObject:SetActive(true);
		sliderleft.interactable = false;
		sliderright.interactable = false;
		if CurrentType() == 1 then
			mainUI.gameObject:SetActive(false);
		else
			mainUI.gameObject:SetActive(true);
		end
	end
	sliderleft.value = currentSetDay-1;
	if currentSetSatge<3 then
		sliderright.value = 0;
	else
		sliderright.value = 1;
	end
	local txt = sliderleft.transform:Find("Handle_Slide_Area/Handle/Day/Text_CurrentDay"):GetComponent(typeof(CS.ExText));
	if currentSetDay == 1 then
		txt.text = CS.Data.GetLang(60662);
	elseif currentSetDay == 2 then
		txt.text = CS.Data.GetLang(60663);
	elseif currentSetDay == 3 then
		txt.text = CS.Data.GetLang(60664);
	elseif currentSetDay == 4 then
		txt.text = CS.Data.GetLang(60665);
	elseif currentSetDay == 5 then
		txt.text = CS.Data.GetLang(60666);
	elseif currentSetDay == 6 then
		txt.text = CS.Data.GetLang(60667);
	elseif currentSetDay == 7 then
		txt.text = CS.Data.GetLang(60668);
	end
	local leftDay = sliderleft.transform:Find("Handle_Slide_Area/Handle/Day");
	local leftPlay = sliderleft.transform:Find("Handle_Slide_Area/Handle/Live");
	local leftarrow_l = sliderleft.transform:Find("Handle_Slide_Area/Handle/Img_LeftArrow");
	local leftarrow_r = sliderleft.transform:Find("Handle_Slide_Area/Handle/Img_RightArrow");
	leftDay.gameObject:SetActive(currentSetDay ~= 8);
	leftPlay.gameObject:SetActive(currentSetDay == 8);
	if CurrentType() == 4 then
		leftarrow_l.gameObject:SetActive(currentSetDay ~= 1);
		leftarrow_r.gameObject:SetActive(currentSetDay ~= 8);
	else
		leftarrow_l.gameObject:SetActive(currentSetDay == 8);
		leftarrow_r.gameObject:SetActive(currentSetDay ~= 8);
	end
	local timeday = sliderright.transform:Find("Handle_Slide_Area/Handle/Day");	
	local timearrow_l = sliderright.transform:Find("Handle_Slide_Area/Handle/Img_LeftArrow");
	local timenight = sliderright.transform:Find("Handle_Slide_Area/Handle/Night");
	local timearrow_r = sliderright.transform:Find("Handle_Slide_Area/Handle/Img_RightArrow");
	timeday.gameObject:SetActive(currentSetSatge<3);
	timearrow_l.gameObject:SetActive(currentSetSatge>2);
	timenight.gameObject:SetActive(currentSetSatge>2);
	timearrow_r.gameObject:SetActive(currentSetSatge<3);
	if btnShowRank == nil or btnShowRank:isNull() then
		btnShowRank = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/ZLSR_RankingEntrance"), opsControl.leftMain, false);
		local btn = btnShowRank:GetComponent(typeof(CS.ExButton));
		btn:AddOnClick(function()
			RequestRankData();
			end);
	end
	btnShowRank:SetActive(CurrentType() ~= 1);
	btnShowRank.transform:Find("Img_New").gameObject:SetActive(checkCanGetPrize());
	if btnGuide == nil or btnGuide:isNull() then
		btnGuide = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/ZLSR_Guide"), opsControl.leftMain, false);
		local btn = btnGuide:GetComponent(typeof(CS.ExButton));
		btn:AddOnClick(function()
				PlayGuide("Campaion57Explain");	
			end);
	end
end

function ShowRestBtn()
	for i=0,endMissionIds.Count-1 do
		local missionid = endMissionIds[i];
		if missionid ~= 11269 then
			local mission = CS.GameData.listMission:GetDataById(missionid);
			if mission ~= nil and mission.winCount>0 then
				return true;
			end
		end
	end
	return false;
end

function DragChangeDay(value)--手动改变天数	
	if CurrentType() == 4 then		
		currentSetDay = value +1;
		if currentSetDay>7 then
			currentSetType = 3;
		else
			currentSetType = 2;
		end
		Refresh57UI(true);
		CS.UnityEngine.PlayerPrefs.SetInt("currentSetDay",currentSetDay);
		CS.UnityEngine.PlayerPrefs.Save();
	end
end

function DragChangeTime(value)--手动改变时间
	if CurrentType() == 4 then
		if value == 0 then
			currentSetSatge = 0;	
		elseif value == 1 then
			currentSetSatge = 5;
		end
		CS.UnityEngine.PlayerPrefs.SetInt("currentSetSatge",currentSetSatge);
		CS.UnityEngine.PlayerPrefs.Save();
		Refresh57UI(true);
	end
end
local personStoryUI = nil;
local clickpersonChild = nil;
local orderlast;
function LoadStoryUI()--右边人物故事UI	
	if personStoryUI == nil or personStoryUI:isNull() then
		personStoryUI = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/ZLSR_PersonalStory"), opsControl.leftMain, false);
		local listparent = personStoryUI.transform:Find("StoryList");
		for i=1,#personinfo do
			local index = personinfo[i][1];
			local clickChild = listparent:GetChild(index);
			local btn = clickChild:GetComponent(typeof(CS.ExButton));
			btn:AddOnClick(function()
				local clock = clickChild:Find("Img_Locked");
				if clock.gameObject.activeInHierarchy then
					CS.CommonController.LightMessageTips(CS.Data.GetLang(60695));	
					return;
				end
				ClickPerson(clickChild,i);
			end);
			for j=0,personinfo[i][2].Count-1 do
				local missionid = personinfo[i][2][j];
				local item = clickChild:Find("MissionList"):GetChild(j);
				local missionbtn = item:GetComponent(typeof(CS.ExButton));
				missionbtn:AddOnClick(function()
					local clockTrans = item:Find("Img_Locked");
					if clockTrans.gameObject.activeInHierarchy then
						CS.CommonController.LightMessageTips(CS.Data.GetLang(60695));	
						return;
					end	
					OpenMission(missionid,item);
					ClickPerson(clickChild,i);	
				end);
			end
		end
	end
	--if clickpersonChild ~= nil then
	--	ClickPerson(clickpersonChild,orderlast);
	--	clickpersonChild = nil;
	--end
	personStoryUI.gameObject:SetActive(CurrentType() ~= 1);
	--上层new lock状态
	local listparent = personStoryUI.transform:Find("StoryList");
	for i=1,#personinfo do
		local index = personinfo[i][1];
		local clickChild = listparent:GetChild(index);
		local item = personStoryUI.transform:Find("StoryList"):GetChild(index);
		item:Find("Img_Locked").gameObject:SetActive(true);
		item:Find("Img_New").gameObject:SetActive(false);
		local canvasGroup = clickChild:Find("Left"):GetComponent(typeof(CS.UnityEngine.CanvasGroup));
		if canvasGroup ~= nil and not canvasGroup:isNull() then
			canvasGroup.alpha = 1;
		end
		for j=0,personinfo[i][2].Count-1 do
			local missionid = personinfo[i][2][j]; 
			local imageCheck =  clickChild:Find("Left"):GetChild(j):GetComponent(typeof(CS.ExImage));
			local mission = CS.GameData.listMission:GetDataById(missionid);
			local tween = imageCheck.transform:GetComponent(typeof(CS.TweenPlay));
			imageCheck.transform:DOKill();
			if mission ~= nil then
				if mission.winCount > 0 then
					item:Find("Img_Locked").gameObject:SetActive(false);
					imageCheck.color = CS.UnityEngine.Color(40/255,41/255,42/255,1);
				elseif CheckMissionIdShow(missionid) then
					item:Find("Img_Locked").gameObject:SetActive(false);
					item:Find("Img_New").gameObject:SetActive(true);
					imageCheck.color = CS.UnityEngine.Color(230/255,54/255,99/255,1);
					--print("播放tween");					
					CS.CommonController.Invoke(function()
						tween:DoTween();	
						end,0.5,CS.OPSPanelController.Instance);
				else
					imageCheck.color = CS.UnityEngine.Color(167/255,168/255,171/255,1);
				end
			else
				imageCheck.color = CS.UnityEngine.Color(167/255,168/255,171/255,1);
			end
		end
	end
end

local SelectOPSMission = function(self,opsmission,item)
	self.checkPosMin = self.checkPosMax - self.num * self.distance;
	if not self.useOPSmissions:Contains(opsmission) then
		self.useOPSmissions:Add(opsmission);
	end
	self:SelectOPSMission(opsmission,item);
	if personStoryUI ~= nil then
		personStoryUI.transform:Find("Img_MissionBG").gameObject:SetActive(true);
	end
end
local CancelMission = function(self)
	if self.campaionId == -57 then
		if self.chooseSpot ~= nil then
			local canvas = self.chooseSpot.transform:Find("PanelLayout"):GetComponent(typeof(CS.UnityEngine.Canvas))
			canvas.sortingOrder = 0;
			local trans = self.chooseSpot.transform:Find("PanelLayout"):GetComponent(typeof(CS.UnityEngine.RectTransform));
			trans:DOAnchorPos(CS.UnityEngine.Vector2(222,135),0.5);
		end
		if personStoryUI ~= nil then
			personStoryUI.transform:Find("Img_MissionBG").gameObject:SetActive(false);
		end
	end
	--CS.OPSPanelBackGround.Instance.oldscale = 0;
	CS.OPSPanelProcessItem.canmapmove = true;
	local temp = self.currentContainer;
	self.currentContainer = nil;
	self:CancelMission();
	self.currentContainer = temp;
	self:RefreshMoudleBuildUI();
end
lastWinmissionid = 0;
missionidAvg = {};
function CheckForceAvg()--进入场景播放当前可能的剧情
	print("lastWinmissionid"..lastWinmissionid);
	if missionidAvg[lastWinmissionid] ~= nil then
		ShowAvg(missionidAvg[lastWinmissionid],lastWinmissionid);
	end
	--if CS.AVGController.inst ~= nil and not CS.AVGController.inst:isNull() then
	--	return;
	--end
	lastWinmissionid = 0;
	missionidAvg = {};
	for i=1,#avgshowinfo do
		local missionid = avgshowinfo[i][1];
		local day = avgshowinfo[i][4];
		local stage = avgshowinfo[i][5];
		local avg = avgshowinfo[i][2];
		local mission = CS.GameData.listMission:GetDataById(missionid);
		if mission ~= nil then
			if CheckMissionIdShow(missionid) then
				if currentSetDay == day then
					local canplay = false;
					if currentSetSatge > 2 then
						if stage>2 then
							canplay = true;
						end	
					else
						if stage<3 then
							canplay = true;;
						end	
					end
					if canplay then
						if missionavgs[missionid] == nil or not missionavgs[missionid]:Contains(avg) then
							print(missionid.."剧情满足条件强制播放day"..day.."stage"..stage)
							--ShowAvg(avg,missionid);
							missionidAvg[missionid] = avg;
						elseif CS.ConfigData.playReplay then
							print(missionid.."剧情满足条件重复播放day"..day.."stage"..stage)
							missionidAvg[missionid] = avg;
						end
					end
				end
			end
		end
	end
end
function CheckAvgNotRead(avgcode,missionid)
	if missionavgs[missionid] == nil then
		return true;
	end	
	if not missionavgs[missionid]:Contains(avgcode) then
		return true;		
	end	
	return false;
end
function ShowAvg(avgcode,missionid)
	--CS.UnityEngine.PlayerPrefs.SetInt(avgcode,1);
	--CS.UnityEngine.PlayerPrefs.Save();
	local txtAVG = CS.ResManager.GetObjectByPath("AVGTxt/"..avgcode,".txt");
	if txtAVG == nil then
		CS.NDebug.LogError("未找到avg剧本"..avgcode);
		return;
	end
	CS.AVGController.Instance.transform:SetParent(opsControl.transform,false);
	CS.AVGController.Instance:InitializeData(txtAVG);
	if missionid == 0 then
		return;
	end
	if missionavgs[missionid] == nil then
		missionavgs[missionid] = CS.System.Collections.Generic.List(CS.System.String)();
	end
	if not missionavgs[missionid]:Contains(avgcode) then
		missionavgs[missionid]:Add(avgcode);	
	end
	RequestSaveMissionAVG(missionid);
end
function RequestSaveMissionAVG(missionid)
	local sb = CS.System.Text.StringBuilder();
	local writer = CS.LitJson.JsonWriter(sb);
	writer:WriteObjectStart();
	writer:WritePropertyName("mission_id");
	writer:Write(missionid);
	writer:WritePropertyName("avg");
	local txt = "";
	for i=0,missionavgs[missionid].Count-1 do
		if i == missionavgs[missionid].Count-1 then
			txt=txt..missionavgs[missionid][i];
		else				
			txt=txt..missionavgs[missionid][i]..",";
		end
	end	
	writer:Write(txt);				
	writer:WriteObjectEnd();
	CS.ConnectionController.CreateConnection("Mission/avg","",sb,function(www)
					print("sucess");					
				end,nil,false);	
end
function OpenMission(missionid,spot)
	opsControl.Line.gameObject:SetActive(true);
	local point = spot.transform:Find("PanelLayout");
	if point ~= nil then
		opsControl.Line:ShowLine(point.transform, opsControl.MissionInfoController.transform:Find("LinePoint"));
	else
		opsControl.Line:ShowLine(spot.transform, opsControl.MissionInfoController.transform:Find("LinePoint"));
	end
	opsControl.MissionInfoController.gameObject:SetActive(true);
	opsControl.MissionInfoController:InitMission(missionid);
	if opsControl.chooseSpot ~= nil then
		local trans = opsControl.chooseSpot.transform:Find("PanelLayout"):GetComponent(typeof(CS.UnityEngine.RectTransform));
		trans:DOAnchorPos(CS.UnityEngine.Vector2(-550,140),0.5);
	end
	if personStoryUI ~= nil then
		personStoryUI.transform:Find("Img_MissionBG").gameObject:SetActive(true);
	end
end

local show = false;
function ClickPerson(child,order)--点击对应人物展示当前人物剧情	
	print("剧情"..order);
	if clickpersonChild ~= nil and not clickpersonChild:isNull() and clickpersonChild ~= child then
		local tweenGroup0 = clickpersonChild:GetComponent(typeof(CS.TweenPlayGroup));
		tweenGroup0:PlayTweensByOrder(2);
		show = false;
	end	
	if clickpersonChild == child then
		clickpersonChild = nil;
	else
		clickpersonChild = child;
	end
	orderlast = order;
	child:Find("MissionList").gameObject:SetActive(true);
	local tweenGroup1 = child:GetComponent(typeof(CS.TweenPlayGroup));
	if show then
		tweenGroup1:PlayTweensByOrder(2);
	else
		tweenGroup1:PlayTweensByOrder(1);
	end
	show = not show;
	for i=0,personinfo[order][2].Count-1 do
		local missionid = personinfo[order][2][i];
		local mission = CS.GameData.listMission:GetDataById(missionid);
		local item = child:Find("MissionList"):GetChild(i);
		local btn = item:GetComponent(typeof(CS.ExButton));
		local clockTrans = item:Find("Img_Locked");
		local newTrans = item:Find("Img_New");
		local completeTrans = item:Find("Img_Completed");
		newTrans.gameObject:SetActive(false);
		completeTrans.gameObject:SetActive(false);
		clockTrans.gameObject:SetActive(false);
		if mission ~= nil then
			if mission.winCount > 0 then
				completeTrans.gameObject:SetActive(true);
			elseif CheckMissionIdShow(missionid) then
				newTrans.gameObject:SetActive(true);
			else
				clockTrans.gameObject:SetActive(true);
			end
		else
			clockTrans.gameObject:SetActive(true);
		end
	end
end
function GetAvgInfo(missionid)
	for i=1,#avgshowinfo do
		if avgshowinfo[i][1] == missionid then
			local day = avgshowinfo[i][4];
			local stage = avgshowinfo[i][5];
			if currentSetDay == day then
				if currentSetSatge > 2 then
					if stage>2 then
						return avgshowinfo[i];
					end	
				else
					if stage<3 then
						return avgshowinfo[i];
					end	
				end
			end
		end
	end
	return nil;
end
function GetMissionKeyNum(missionkey)--获取missionkeynum
	local num = 0;
	if CS.GameData.missionKeyNum:ContainsKey(missionkey) then
		num = CS.GameData.missionKeyNum[missionkey];
	end
	return num;
end
function CurrentType()--(1-4)获取理论当前类型=4玩家进入自由选择阶段
	if GetMissionKeyNum(1126100) == 0 then
		return 1;
	end
	if GetMissionKeyNum(1126200) > 25 then
		if GetMissionKeyNum(1128301) >0 then
			return 4;
		else
			return 3;
		end
	end
	return 2;
end
function CurrentDay()--自由行动当前第几天(1-7)
	local keynum = 0;
	if CS.GameData.missionKeyNum:ContainsKey(checkMissionkeyId) then
		keynum = CS.GameData.missionKeyNum[checkMissionkeyId];
	end
	local day = CS.Mathf.FloorToInt(keynum/4)+1;
	if day>8 then
		day = 8;
	end
	return day;
end

function CurrentStage()--自由行动当前第几阶段(1-4)
	local keynum = 0;
	if CS.GameData.missionKeyNum:ContainsKey(checkMissionkeyId) then
		keynum = CS.GameData.missionKeyNum[checkMissionkeyId];
	end
	if keynum == 0 then
		return 1;
	end
	local stage = keynum%4;
	return stage+1;
end
local CapacityMap = nil;
function LoadCapacityMap()--载入5道具UI
	if CapacityMap == nil or CapacityMap:isNull() then
		CapacityMap = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/ZLSR_Ability"), opsControl.leftMain, false);
	end
	local text1 = CapacityMap.transform:Find("Frame/Ability1/Text_Num"):GetComponent(typeof(CS.ExText));
	local text2 = CapacityMap.transform:Find("Frame/Ability2/Text_Num"):GetComponent(typeof(CS.ExText));
	local text3 = CapacityMap.transform:Find("Frame/Ability3/Text_Num"):GetComponent(typeof(CS.ExText));
	local text4 = CapacityMap.transform:Find("Frame/Ability4/Text_Num"):GetComponent(typeof(CS.ExText));
	local text5 = CapacityMap.transform:Find("Frame/Ability5/Text_Num"):GetComponent(typeof(CS.ExText));
	local max1 = CapacityMap.transform:Find("Frame/Ability1/Img_Max");
	local max2 = CapacityMap.transform:Find("Frame/Ability2/Img_Max");
	local max3 = CapacityMap.transform:Find("Frame/Ability3/Img_Max");
	local max4 = CapacityMap.transform:Find("Frame/Ability4/Img_Max");
	local max5 = CapacityMap.transform:Find("Frame/Ability5/Img_Max");
	local textTitle1 = CapacityMap.transform:Find("Frame/Ability1/Text_Name"):GetComponent(typeof(CS.ExText));
	local textTitle2 = CapacityMap.transform:Find("Frame/Ability2/Text_Name"):GetComponent(typeof(CS.ExText));
	local textTitle3 = CapacityMap.transform:Find("Frame/Ability3/Text_Name"):GetComponent(typeof(CS.ExText));
	local textTitle4 = CapacityMap.transform:Find("Frame/Ability4/Text_Name"):GetComponent(typeof(CS.ExText));
	local textTitle5 = CapacityMap.transform:Find("Frame/Ability5/Text_Name"):GetComponent(typeof(CS.ExText));
	--local gradient1 = CapacityMap.transform:Find("Frame/Ability1/Text_Name"):GetComponent(typeof(CS.FontGradient));
	--local gradient2 = CapacityMap.transform:Find("Frame/Ability2/Text_Name"):GetComponent(typeof(CS.FontGradient));
	--local gradient3 = CapacityMap.transform:Find("Frame/Ability3/Text_Name"):GetComponent(typeof(CS.FontGradient));
	--local gradient4 = CapacityMap.transform:Find("Frame/Ability4/Text_Name"):GetComponent(typeof(CS.FontGradient));
	--local gradient5 = CapacityMap.transform:Find("Frame/Ability5/Text_Name"):GetComponent(typeof(CS.FontGradient));	
	local num1 = CS.GameData.GetItem(9021);
	local num2 = CS.GameData.GetItem(9022);
	local num3 = CS.GameData.GetItem(9023);
	local num4 = CS.GameData.GetItem(9024);
	local num5 = CS.GameData.GetItem(9025);
	local color0 = CS.UnityEngine.Color(57/255,57/255,57/255,1);
	local color1 = CS.UnityEngine.Color(254/255,37/255,93/255,1);
	if num1<100 then
		--textTitle1.color = color0;
		--gradient1.enabled = false;
		text1.color = color0;
		text1.gameObject:SetActive(true);
		max1.gameObject:SetActive(false);
	else
		--textTitle1.color = CS.UnityEngine.Color.white;
		--gradient1.enabled = true;
		--gradient1.angle = gradient1.angle - 0.01;
		text1.color = color1;
		text1.gameObject:SetActive(false);
		max1.gameObject:SetActive(true);
	end
	if num2<100 then
		--textTitle2.color = color0;
		--gradient2.enabled = false;
		text2.color = color0;
		text2.gameObject:SetActive(true);
		max2.gameObject:SetActive(false);
	else
		--textTitle2.color = CS.UnityEngine.Color.white;
		--gradient2.enabled = true;
		--gradient2.angle = gradient2.angle - 0.01;
		text2.color = color1;
		text2.gameObject:SetActive(false);
		max2.gameObject:SetActive(true);
	end	
	if num3<100 then
		--textTitle3.color = color0;
		--gradient3.enabled = false;
		text3.color = color0;
		text3.gameObject:SetActive(true);
		max3.gameObject:SetActive(false);
	else
		--textTitle3.color = CS.UnityEngine.Color.white;
		--gradient3.enabled = true;
		--gradient3.angle = gradient3.angle - 0.01;
		text3.color = color1;
		text3.gameObject:SetActive(false);
		max3.gameObject:SetActive(true);
	end	
	if num4<100 then
		--textTitle4.color = color0;
		--gradient4.enabled = false;
		text4.color = color0;
		text4.gameObject:SetActive(true);
		max4.gameObject:SetActive(false);
	else
		--textTitle4.color = CS.UnityEngine.Color.white;
		--gradient4.enabled = true;
		--gradient4.angle = gradient4.angle - 0.01;
		text4.color = color1;
		text4.gameObject:SetActive(false);
		max4.gameObject:SetActive(true);
	end
	if num5<100 then
		--textTitle5.color = color0;
		--gradient5.enabled = false;
		text5.color = color0;
		text5.gameObject:SetActive(true);
		max5.gameObject:SetActive(false);
	else
		--textTitle5.color = CS.UnityEngine.Color.white;
		--gradient5.enabled = true;
		--gradient5.angle = gradient5.angle - 0.01;
		text5.color = color1;
		text5.gameObject:SetActive(false);
		max5.gameObject:SetActive(true);
	end		
	text1.text = tostring(num1);
	text2.text = tostring(num2);
	text3.text = tostring(num3);
	text4.text = tostring(num4);
	text5.text = tostring(num5);
end
function CheckRestButton()--是否显示重置按钮
	local show = false;
	for i=0,startOPSmission.Count-1 do
		local opsmission = startOPSmission[i];
		if opsmission:ClearCount()>0 then
			show = true;
		end
	end
	if show then
		
	end
end
function OnClickReast()--点击重置按钮
	CS.CommonController.ConfirmBox(CS.Data.GetLang(60642) ,function()
			OnClickReastComfirm();
		end)
end
function OnClickReastComfirm()
	CS.CommonController.ConfirmBox(CS.Data.GetLang(60643) ,function()
			RequestReast();
		end)
end
function RequestReast()--重置请求
	local sb = CS.System.Text.StringBuilder();
	local writer = CS.LitJson.JsonWriter(sb);
	writer:WriteObjectStart();
	writer:WritePropertyName("campaign");
	writer:Write(opsControl.campaionId);
	writer:WriteObjectEnd();
	CS.ConnectionController.CreateConnection("Mission/weakResetCampaign","",sb,function(www)
			print("sucess");
			RequestReastHandle(www)
		end,function(www)
		end,false);	
end
function RequestReastHandle(www)--获取重置数据
	local jsonData = CS.ConnectionController.DecodeAndMapJson(www.text);
	local missionkeyData = jsonData:GetValue("user_all_mission_key");
	CS.NDebugJson.Log("user_all_mission_key", missionkeyData);
	CS.GameData.missionKeyNum:Clear();
	local keyids = CS.System.Collections.Generic.List(CS.System.String)(missionkeyData.Keys);
	for i=0,keyids.Count-1 do
		local missionkeyid = tonumber(keyids[i]);
		local num = missionkeyData:GetValue(keyids[i]).Int;
		if CS.GameData.missionKeyNum:ContainsKey(missionkeyid) then
			CS.GameData.missionKeyNum[missionkeyid] = num;
		else
			CS.GameData.missionKeyNum:Add(missionkeyid,num);
		end
	end
	local itemNumData = jsonData:GetValue("user_all_item");
	CS.NDebugJson.Log("user_all_item", itemNumData);
	local itemids = CS.System.Collections.Generic.List(CS.System.String)(itemNumData.Keys);
	for i=0,itemids.Count-1 do
		local tempData = itemNumData:GetValue(itemids[i]);
		local itemid = tempData:GetValue("item_id").Int;
		local num = tempData:GetValue("number").Int;
		CS.GameData.SetItem(itemid, num);
	end
	CS.GameData.SetItem(9021, 0);
	CS.GameData.SetItem(9022, 0);
	CS.GameData.SetItem(9023, 0);
	CS.GameData.SetItem(9024, 0);
	CS.GameData.SetItem(9025, 0);
	CheckAllTypeStage();
end	
function GetList(temp)
	local check = CS.System.Collections.Generic.List(CS.System.Int32)();
	if CS.System.String.IsNullOrEmpty(temp) then
		return check;
	end
	local txt = Split(temp,",");
	for j=1,#txt do
		local mtxt = txt[j];
		check:Add(tonumber(mtxt));
	end
	return  check;
end
--变相解析条件表达式
function GetMissionKeyListOr(temp)
	local listOr = {};
	if CS.System.String.IsNullOrEmpty(temp) then
		return listOr;
	end
	local txt = Split(temp,",");
	for j=1,#txt do
		local mtxt = txt[j];
		local listAnd = {};
		local mtxtAnd = Split(mtxt,"&");
		for m=1,#mtxtAnd do
			local itemnum = mtxtAnd[m];
			local itemVec3 = CS.UnityEngine.Vector3();
			if string.find(itemnum,">") then
				itemVec3.x = tonumber(Split(itemnum,">")[1]);
				itemVec3.y = tonumber(Split(itemnum,">")[2]);
				itemVec3.z = 1;
			elseif string.find(itemnum,"=") then
				itemVec3.x = tonumber(Split(itemnum,"=")[1]);
				itemVec3.y = tonumber(Split(itemnum,"=")[2]);
				itemVec3.z = 2;
			elseif string.find(itemnum,"<") then
				itemVec3.x = tonumber(Split(itemnum,"<")[1]);
				itemVec3.y = tonumber(Split(itemnum,"<")[2]);
				itemVec3.z = 3;			
			end	
			table.insert(listAnd,itemVec3);			
		end
		table.insert(listOr,listAnd);		
	end
	return  listOr;
end

--确定对应关卡各种状态是否显示
function CheckAllMissionIdSpotShow(missionid)--是否可以战斗
	if not endMissionIds:Contains(missionid) then
		return CheckMissionIdShow(missionid);
	end
	if CurrentType() == 3 or CurrentType() == 4 then --完全显示	
		local missionidShow = 0;
		if CheckMissionIdShow(11285) then
			missionidShow = 11285;
		elseif CheckMissionIdShow(11290) then
			missionidShow = 11290;
		elseif CheckMissionIdShow(11291) then
			missionidShow = 11291;
		elseif CheckMissionIdShow(11292) then
			missionidShow = 11292;
		elseif CheckMissionIdShow(11284) then
			missionidShow = 11284;	
		elseif CheckMissionIdShow(11288) then
			missionidShow = 11288;
		elseif CheckMissionIdShow(11289) then
			missionidShow = 11289;	
		elseif CheckMissionIdShow(11287) then
			missionidShow = 11287;
		elseif CheckMissionIdShow(11283) then
			missionidShow = 11283;
		elseif CheckMissionIdShow(11286) then
			missionidShow = 11286;
		elseif CheckMissionIdShow(11269) then
			missionidShow = 11269;	
		end	
		return missionidShow == missionid;
	end
	return false;
end
--检查对应关卡是否显示
function CheckMissionIdShow(missionid)
	local mission = CS.GameData.listMission:GetDataById(missionid);
	if mission == nil then
		return false;
	end
	if spotshowinfo[missionid] == nil then
		print("没配置数据"..missionid);
		return false;
	end
	local typeinfo = spotshowinfo[missionid][2];
	if typeinfo.Count>0 and not typeinfo:Contains(currentSetType) then
		--print("typeinfo不满足"..missionid);
		return false;
	end
	local dayinfo = spotshowinfo[missionid][3];
	if dayinfo.Count>0 and not dayinfo:Contains(currentSetDay) then
		--print("dayinfo不满足"..missionid);
		return false;
	end
	local stageinfo = spotshowinfo[missionid][4];
	if stageinfo.Count>0 then
		if currentSetSatge == 0 then
			if not stageinfo:Contains(1) and not stageinfo:Contains(2) then
				--print("Satge不满足"..missionid.."Satge"..currentSetSatge);
				return false;
			end
		elseif currentSetSatge == 5 then
			if not stageinfo:Contains(3) and not stageinfo:Contains(4) then
				--print("Satge不满足"..missionid.."Satge"..currentSetSatge);
				return false;
			end	
		else
			if not stageinfo:Contains(currentSetSatge) then
				--print("Satge不满足"..missionid.."Satge"..currentSetSatge);
				return false;
			end
		end
	end
	local missionkeyorinfo = spotshowinfo[missionid][5];
	if next(missionkeyorinfo) ~= nil then
		local missionkeyresult = false;
		for i=1,#missionkeyorinfo do
			local andInfo = missionkeyorinfo[i];
			local andResult = true;
			for j=1,#andInfo do
				andResult = andResult and CheckMissionKeyNumInfo(andInfo[j]);
			end
			missionkeyresult = missionkeyresult or andResult;
		end
		if missionkeyresult == false then
			--print("missionkey不满足"..missionid);
			return false;
		end
	end
	local itemorinfo = spotshowinfo[missionid][6];
	if next(itemorinfo) ~= nil then
		local itemresult = false;
		for i=1,#itemorinfo do
			local andInfo = itemorinfo[i];
			local andResult = true;
			for j=1,#andInfo do
				--print(andInfo[j]);
				andResult = andResult and CheckItemNumInfo(andInfo[j]);
			end
			itemresult = itemresult or andResult;
		end
		if itemresult == false then
			--print("iteminfo0不满足"..missionid);
			return false;
		end 
	end
	local itemorinfo1 = spotshowinfo[missionid][7];
	if next(itemorinfo1) ~= nil then
		local itemresult1 = false;
		for i=1,#itemorinfo1 do
			local andInfo = itemorinfo1[i];
			local andResult = true;
			for j=1,#andInfo do
				andResult = andResult and CheckItemNumInfo(andInfo[j]);
			end
			itemresult1 = itemresult1 or andResult;
		end
		if itemresult1 == false then
			--print("iteminfo1不满足"..missionid);
			return false;
		end
	end
	--print("显示"..missionid);
	return true;
end
function CheckMissionKeyNumInfo(infoVec3)
	local id = infoVec3.x;
	local num = infoVec3.y;
	if infoVec3.z == 1 then
		return GetMissionKeyNum(id) > num;
	elseif infoVec3.z == 2 then
		return GetMissionKeyNum(id) == num;
	elseif infoVec3.z == 3 then	
		return GetMissionKeyNum(id) < num;
	end
	return false;
end
function CheckItemNumInfo(infoVec3)
	local id = infoVec3.x;
	local num = infoVec3.y;
	if infoVec3.z == 1 then
		return CS.GameData.GetItem(id) > num;
	elseif infoVec3.z == 2 then
		return CS.GameData.GetItem(id) == num;
	elseif infoVec3.z == 3 then	
		return CS.GameData.GetItem(id) < num;
	end
	return false;
end
local InitCameraBackground = function(self)
	self:InitCameraBackground();
	if self.cameraBackground ~= nil then
		self.cameraBackground.transform:SetParent(self.transform.parent,false);
	end
end

local SelectMissionSpot = function(self,spot)
	if self.campaionId == -57 then
		if self.chooseSpot ~= nil then
			local canvas = self.chooseSpot.transform:Find("PanelLayout"):GetComponent(typeof(CS.UnityEngine.Canvas))
			canvas.sortingOrder = 0;
			local trans = self.chooseSpot.transform:Find("PanelLayout"):GetComponent(typeof(CS.UnityEngine.RectTransform));
			trans:DOAnchorPos(CS.UnityEngine.Vector2(222,135),0.5);
		end
		if CS.OPSPanelController.selectHolderOrder == -1 then
			CS.OPSPanelController.selectHolderOrder = spot.missionHolderOrder;
			self.chooseSpot = spot;
			local canvas = spot.transform:Find("PanelLayout"):GetComponent(typeof(CS.UnityEngine.Canvas))
			canvas.sortingOrder = 1;
			CS.OPSPanelBackGround.Instance:FocusSpotMove(spot.transform.localPosition);
			CS.OPSPanelProcessItem.canmapmove = false;		
		else
			--local canvas = spot.transform:Find("PanelLayout"):GetComponent(typeof(CS.UnityEngine.Canvas))
			--canvas.sortingOrder = 0;	
			--self.chooseSpot = nil;
			--CS.OPSPanelProcessItem.canmapmove = true;
			CS.OPSPanelController.selectHolderOrder = -1;
			self:CancelMission();
		end
		self:CheckSpecialAnim();
		return;
	end
	self:SelectMissionSpot(spot);
end

local onBattleSpot = nil;
local currentSpot = nil;
local CheckSpecialAnim = function(self)
	if self.campaionId == -57 then
		currentSpot = nil;
		onBattleSpot = nil;
		for i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
			local spot = CS.OPSPanelBackGround.Instance.all3dSpots:GetDataByIndex(i);
			spot:Show();
			local parent = spot.transform:Find("PanelLayout/MissionList");
			if CS.OPSPanelController.selectHolderOrder == spot.missionHolderOrder then
				self:Play3dSpotAnim(spot);
			else
				CheckSpotMission(spot);
				parent.gameObject:SetActive(false);
				spot.transform:Find("PanelLayout/MissionBG").gameObject:SetActive(false);
			end
		end
		if CurrentType() == 2 or CurrentType() == 3 then
			if currentSpot == nil then
				for i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
					local spot = CS.OPSPanelBackGround.Instance.all3dSpots:GetDataByIndex(i);
					if spot.gameObject.activeInHierarchy then
						currentSpot = spot;
					end
				end
			end
		elseif CurrentType() == 4 then
			currentSpot = nil;
		end
		if not findSpot then
			currentSpot = nil;
			onBattleSpot = nil;
		end
		if CS.OPSPanelController.selectHolderOrder == -1 then
			if onBattleSpot ~= nil then
				local pos = CS.UnityEngine.Vector2(onBattleSpot.transform.localPosition.x,onBattleSpot.transform.localPosition.y);
				CS.OPSPanelBackGround.Instance:Move(pos,true,0.5);			
				return;
			end
			if currentSpot ~= nil then
				print("移动到新关卡点");
				local pos = CS.UnityEngine.Vector2(currentSpot.transform.localPosition.x,currentSpot.transform.localPosition.y);
				CS.OPSPanelBackGround.Instance:Move(pos,true,0.5);
			end
		end
		findSpot = false;
		return;
	end
	self:CheckSpecialAnim();
end
function CheckSpotMission(spot)
	local missions = CS.System.Collections.Generic.List(CS.Mission)();
	if CS.OPSPanelController.Instance.currentPanelConfig.spotShowInfos:ContainsKey(spot.id) then
		local info = CS.OPSPanelController.Instance.currentPanelConfig.spotShowInfos[spot.id];
		for i=0,info.missionids.Count -1 do
			local missionid = info.missionids[i][CS.OPSPanelController.difficulty];
			if endMissionIds:Contains(missionid) and CurrentType() == 4 then
				if currentSetType == 4 or currentSetType == 3 then
					local mission = CS.GameData.listMission:GetDataById(missionid);
					if 	mission~= nil then				
						missions:Add(mission);
					end
				end
			elseif CheckAllMissionIdSpotShow(missionid) then
				local mission = CS.GameData.listMission:GetDataById(missionid);					
				missions:Add(mission);
			end
		end
	end
	local avatar = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar");
	local picParent = spot.transform:Find("PanelLayout/MissionList/Mission/AVG_Avatar");
	local onBattleTag = spot.transform:Find("PanelLayout/SpotPanel/Img_InProgress");
	local newTag = spot.transform:Find("PanelLayout/SpotPanel/Img_New");
	if onBattleTag.gameObject.activeInHierarchy then
		onBattleSpot = spot;
	end
	if newTag.gameObject.activeInHierarchy then
		currentSpot = spot;
	end
	local show = false;
	for i=0,missions.Count-1 do
		local avginfo = GetAvgInfo(missions[i].missionInfo.id);
		if avginfo ~= nil then
			--local avgread = CS.UnityEngine.PlayerPrefs.GetInt(avginfo[2],0);
			local spotpic0 = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar/Img_AvatarBG1");
			local spotpic1 = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar/Img_AvatarBG2");
			local spotpic2 = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar/Img_AvatarBG3");
			local spriteHolder = picParent:GetComponent(typeof(CS.UGUISpriteHolder));
			if avginfo[3][1] ~= nil then
				show = true;
				spotpic0.gameObject:SetActive(true);
				local spotimage = spotpic0:GetChild(0):GetComponent(typeof(CS.ExImage));
				spriteHolder:SetImageSprite(tonumber(avginfo[3][1]),spotimage);
			else
				spotpic0.gameObject:SetActive(false);
			end
			if avginfo[3][2] ~= nil then
				show = true;
				spotpic1.gameObject:SetActive(true);
				local spotimage = spotpic1:GetChild(0):GetComponent(typeof(CS.ExImage));
				spriteHolder:SetImageSprite(tonumber(avginfo[3][2]),spotimage);
			else
				spotpic1.gameObject:SetActive(false);
			end
			if avginfo[3][3] ~= nil then
				show = true;
				spotpic2.gameObject:SetActive(true);
				local spotimage = spotpic2:GetChild(0):GetComponent(typeof(CS.ExImage));
				spriteHolder:SetImageSprite(tonumber(avginfo[3][3]),spotimage);
			else
				spotpic2.gameObject:SetActive(false);
			end
		end
	end
	avatar.gameObject:SetActive(show);
end
local Play3dSpotAnim = function(self,spot)
	if self.campaionId == -57 then--显示列表
		local missions = CS.System.Collections.Generic.List(CS.Mission)();
		if CS.OPSPanelController.Instance.currentPanelConfig.spotShowInfos:ContainsKey(spot.id) then
			local info = CS.OPSPanelController.Instance.currentPanelConfig.spotShowInfos[spot.id];
			for i=0,info.missionids.Count -1 do
				local missionid = info.missionids[i][CS.OPSPanelController.difficulty];
				if endMissionIds:Contains(missionid) and CurrentType() == 4 then
					if currentSetType == 4 or currentSetType == 3 then
						print("showmissionid"..missionid);
						local mission = CS.GameData.listMission:GetDataById(missionid);
						if 	mission~= nil then				
							missions:Add(mission);
						end
					end
				elseif CheckAllMissionIdSpotShow(missionid) then
					local mission = CS.GameData.listMission:GetDataById(missionid);					
					missions:Add(mission);
				end
			end
		end
		local parent = spot.transform:Find("PanelLayout/MissionList");
		parent.gameObject:SetActive(true);
		local avatar = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar");
		avatar.gameObject:SetActive(false);
		spot.transform:Find("PanelLayout/MissionBG").gameObject:SetActive(true);
		while parent.childCount<missions.Count do
			local child = CS.UnityEngine.Object.Instantiate(parent:GetChild(0).gameObject);
			child.transform:SetParent(parent,false);
		end
		local show = false;
		for i=0,parent.childCount -1 do
			local child = parent:GetChild(i);
			if i<missions.Count then
				child.gameObject:SetActive(true);
				local mission = missions[i];
				local txt_name = child:Find("MissionName/Text_MissionName"):GetComponent(typeof(CS.ExText));
				txt_name.text = mission.missionInfo.name;
				if mission.missionInfo.specialType == CS.MapSpecialType.Story then
					txt_name.color = CS.UnityEngine.Color(1,1,1,1);
				else
					txt_name.color = CS.UnityEngine.Color(24/255,24/255,24/255,1);
				end
				local newTag = child:Find("Img_New");
				newTag.gameObject:SetActive(mission.winCount==0);
				local missionactionTag = child:Find("Img_InProgress");
				local onBattle = CS.GameData.missionAction ~= nil and CS.GameData.missionAction.mission == mission;
				missionactionTag.gameObject:SetActive(onBattle);
				local storyTag = child:Find("MissionType/Img_Story");
				storyTag.gameObject:SetActive(mission.missionInfo.specialType == CS.MapSpecialType.Story);
				local storyTagBg = child:Find("MissionBG/Img_StoryBG");
				storyTagBg.gameObject:SetActive(mission.missionInfo.specialType == CS.MapSpecialType.Story);
				local battleTag = child:Find("MissionType/Img_Battle");
				battleTag.gameObject:SetActive(mission.missionInfo.specialType ~= CS.MapSpecialType.Story);
				local battleTagBg = child:Find("MissionBG/Img_BattleBG");
				battleTagBg.gameObject:SetActive(mission.missionInfo.specialType ~= CS.MapSpecialType.Story);
				local btn = child:GetComponent(typeof(CS.ExButton));
				local lock = child:Find("Img_Locked");
				lock.gameObject:SetActive(false);
				local endtipText = "";
				local wincount = mission.winCount;
				if CurrentType() == 4 and endMissionIds:Contains(mission.missionInfo.id) then
					if not CheckAllMissionIdSpotShow(mission.missionInfo.id) and wincount == 0 then
						lock.gameObject:SetActive(true);
						if spotshowinfo[mission.missionInfo.id] ~= nil then
							local tipid = spotshowinfo[mission.missionInfo.id][8];
							if tipid ~= nil then
								endtipText = CS.Data.GetLang(tipid);
							end					
						end
					end
				end
				btn.onClick:RemoveAllListeners();
				btn:AddOnClick(function()
					if lock.gameObject.activeInHierarchy then
						if CanOpenAllEnd() then
							CS.CommonController.LightMessageTips(endtipText);
						else
							local timetext = CS.GameData.UnixToDateTime(CS.OPSConfig.startTime):ToString("G");
							local showtext = CS.System.String.Format(CS.Data.GetLang(60641), timetext);
							CS.CommonController.LightMessageTips(showtext);
						end
						return;
					end
					OpenMission(mission.missionInfo.id,spot);
				end)
				local avginfo = GetAvgInfo(mission.missionInfo.id);
				local btnStory = child:Find("Btn_PlayStory"):GetComponent(typeof(CS.ExButton)); 
				local picParent = child:Find("AVG_Avatar");
				btnStory.gameObject:SetActive(false);
				picParent.gameObject:SetActive(avginfo ~= nil);
				if avginfo ~= nil then
					btnStory.gameObject:SetActive(CurrentType() == 4);
					btnStory.onClick:RemoveAllListeners();
					btnStory:AddOnClick(function()
						ShowAvg(avginfo[2],mission.missionInfo.id);
						end)
					--local avgread = CS.UnityEngine.PlayerPrefs.GetInt(avginfo[2],0);
					btnStory.transform:Find("Img_New").gameObject:SetActive(CheckAvgNotRead(avginfo[2],mission.missionInfo.id));
					local pic0 = picParent:Find("Img_AvatarBG1");
					local pic1 = picParent:Find("Img_AvatarBG2");
					local pic2 = picParent:Find("Img_AvatarBG3");
					local spotpic0 = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar/Img_AvatarBG1");
					local spotpic1 = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar/Img_AvatarBG2");
					local spotpic2 = spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar/Img_AvatarBG3");
					local spriteHolder = picParent:GetComponent(typeof(CS.UGUISpriteHolder));
					if avginfo[3][1] ~= nil then
						--print("1picorder"..avginfo[3][1]);
						show = true;
						pic0.gameObject:SetActive(true);
						local image = pic0:GetChild(0):GetComponent(typeof(CS.ExImage));
						spriteHolder:SetImageSprite(tonumber(avginfo[3][1]),image);
						spotpic0.gameObject:SetActive(true);
						local spotimage = spotpic0:GetChild(0):GetComponent(typeof(CS.ExImage));
						spriteHolder:SetImageSprite(tonumber(avginfo[3][1]),spotimage);
					else
						pic0.gameObject:SetActive(false);
						spotpic0.gameObject:SetActive(false);
					end
					if avginfo[3][2] ~= nil then
						--print("2picorder"..avginfo[3][2]);
						show = true;
						pic1.gameObject:SetActive(true);
						local image = pic1:GetChild(0):GetComponent(typeof(CS.ExImage));
						spriteHolder:SetImageSprite(tonumber(avginfo[3][2]),image);
						spotpic1.gameObject:SetActive(true);
						local spotimage = spotpic1:GetChild(0):GetComponent(typeof(CS.ExImage));
						spriteHolder:SetImageSprite(tonumber(avginfo[3][2]),spotimage);
					else
						pic1.gameObject:SetActive(false);
						spotpic1.gameObject:SetActive(false);
					end
					if avginfo[3][3] ~= nil then
						--print("3picorder"..avginfo[3][3]);
						pic2.gameObject:SetActive(true);
						show = true;
						local image = pic2:GetChild(0):GetComponent(typeof(CS.ExImage));
						spriteHolder:SetImageSprite(tonumber(avginfo[3][3]),image);
						spotpic2.gameObject:SetActive(true);
						local spotimage = spotpic2:GetChild(0):GetComponent(typeof(CS.ExImage));
						spriteHolder:SetImageSprite(tonumber(avginfo[3][3]),spotimage);
					else
						pic2.gameObject:SetActive(false);
						spotpic2.gameObject:SetActive(false);
					end
				end
			else
				child.gameObject:SetActive(false);
			end
		end
		--spot.transform:Find("PanelLayout/SpotPanel/AVG_Avatar").gameObject:SetActive(show);
		return;
	end
	self:Play3dSpotAnim(spot);
end
function CanOpenAllEnd()
	local time = CS.GameData.GetCurrentTimeStamp();
	if CS.OPSConfig.startTime<time then
		return true;
	else
		return false;
	end
end
local CheckMissionProcessData = function(self,spot)
	if self.campaionId == -57 then
		return;
	end
	self:CheckMissionProcessData(spot);
end
local RefreshUI = function(self,onlyrefreshLabel)
	print("检查"..currentSetSatge);
	if self.campaionId == -57 then
		CheckAllTypeStage();
	end
	self:RefreshUI(onlyrefreshLabel);
end

function RequestRankData()--获取排行数据
	local sb = CS.System.Text.StringBuilder();
	local writer = CS.LitJson.JsonWriter(sb);
	writer:WriteObjectStart();
	writer:WritePropertyName("type");
	writer:Write(1001);
	writer:WritePropertyName("sub_type");
	writer:Write(0);
	writer:WritePropertyName("index");
	writer:Write(0);
	writer:WritePropertyName("length");
	writer:Write(10);
	writer:WriteObjectEnd();
	CS.ConnectionController.CreateConnection("Index/rank","",sb,function(www)
			print("sucess");
			RequestRankDataHandle(www)
		end,nil,false);	
end
local rankUI = nil;

function RequestRankDataHandle(www)
	local jsonData = CS.ConnectionController.DecodeAndMapJson(www.text);
	print(jsonData:ToJson());
	if rankUI == nil or rankUI:isNull() then
		rankUI = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/ZLSR_Ranking"), opsControl.leftMain, false);
		local btnreturn = rankUI.transform:Find("Btn_Return"):GetComponent(typeof(CS.ExButton));
		btnreturn:AddOnClick(function()
			rankUI:SetActive(false);
		end)
		local btnreward = rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/Btn_ScoreReward"):GetComponent(typeof(CS.ExButton));
		btnreward:AddOnClick(function()
			OpenRankingReward();
		end)
	end
	rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/Btn_ScoreReward/Img_New").gameObject:SetActive(checkCanGetPrize());
	RefreshRankUI(jsonData);
	rankUI:SetActive(true);
end
--刷新排行界面
function RefreshRankUI(jsonData)
	local datas = {};
	local rankJson = jsonData:GetValue("rank_list");
	for i=0,rankJson.Count-1 do
		local data = {};
		data[1] = rankJson[i]:GetValue("id").Int;
		data[2] = rankJson[i]:GetValue("user_id").Int;
		data[3] = rankJson[i]:GetValue("user_name").String;
		data[4] = rankJson[i]:GetValue("user_level").Int;
		data[5] = rankJson[i]:GetValue("score").Int;
		data[6] = rankJson[i]:GetValue("rank").Int;
		data[7] = rankJson[i]:GetValue("headpic_id").Int;
		data[8] = rankJson[i]:GetValue("frame_id").Int;
		data[9] = rankJson[i]:GetValue("commander_info").String;
		data[10] = rankJson[i]:GetValue("server_name").String;
		table.insert(datas,data);
	end
	local config = CS.Data.GetString("zls_support_progress");
	local temp = Split(config,";");
	local stage0 = tonumber(Split(temp[1],":")[1]);
	local stage1 = tonumber(Split(temp[2],":")[1]);
	local stage2 = tonumber(Split(temp[3],":")[1]);
	local prizeId0 = tonumber(Split(temp[1],":")[2]);
	local prizeId1 = tonumber(Split(temp[2],":")[2]);
	local prizeId2 = tonumber(Split(temp[3],":")[2]);
	local prize0 = CS.GameData.listPrize:GetDataById(prizeId0);
	local prize1 = CS.GameData.listPrize:GetDataById(prizeId1);
	local prize2 = CS.GameData.listPrize:GetDataById(prizeId2);
	if prize0 ~= nil then
		local parent = rankUI.transform:Find("Top/ProgressBar/Prize1");
		if parent.childCount == 0 then
			local txt = prize0:ToString(true,true);
			local rewardicon = prize0:GetIconBuilder():SetIntroduction(txt):SetTipOrder(5):Build():GetComponent(typeof(CS.CommonIconController));
			rewardicon.transform:SetParent(parent,false);
			rewardicon.transform:Find("RarityBG").gameObject:SetActive(false);
			rewardicon.transform:Find("IconMask").gameObject:SetActive(false);
		end
	end
	if prize1 ~= nil then
		local parent = rankUI.transform:Find("Top/ProgressBar/Prize2");
		if parent.childCount == 0 then
			local txt = prize1:ToString(true,true);
			local rewardicon = prize1:GetIconBuilder():SetIntroduction(txt):SetTipOrder(5):Build():GetComponent(typeof(CS.CommonIconController));
			rewardicon.transform:SetParent(parent,false);
			rewardicon.transform:Find("RarityBG").gameObject:SetActive(false);
			rewardicon.transform:Find("IconMask").gameObject:SetActive(false);
		end
	end
	if prize2 ~= nil then
		local parent = rankUI.transform:Find("Top/ProgressBar/Prize3");
		if parent.childCount == 0 then
			local txt = prize2:ToString(true,true);
			local rewardicon = prize2:GetIconBuilder():SetIntroduction(txt):SetTipOrder(5):Build():GetComponent(typeof(CS.CommonIconController));
			rewardicon.transform:SetParent(parent,false);
			rewardicon.transform:Find("RarityBG").gameObject:SetActive(false);
			rewardicon.transform:Find("IconMask").gameObject:SetActive(false);
		end
	end
	local allNum = jsonData:GetValue("zls_support_total").Int;
	local maxnum = CS.Data.GetInt("zls_support_max",1000);
	local percent = allNum/maxnum*100;
	print(config.."maxnum"..maxnum.."percent"..percent);
	local bar1 = rankUI.transform:Find("Top/ProgressBar/ProgressBar1"):GetComponent(typeof(CS.UnityEngine.UI.Slider));
	local bar2 = rankUI.transform:Find("Top/ProgressBar/ProgressBar2"):GetComponent(typeof(CS.UnityEngine.UI.Slider));
	local bar3 = rankUI.transform:Find("Top/ProgressBar/ProgressBar3"):GetComponent(typeof(CS.UnityEngine.UI.Slider));
	local reach1 = rankUI.transform:Find("Top/ProgressBar/Img_Reward1");
	local reach2 = rankUI.transform:Find("Top/ProgressBar/Img_Reward2");
	local reach3 = rankUI.transform:Find("Top/ProgressBar/Img_Reward3");
	local level1 = rankUI.transform:Find("Stage/Level1");
	local level2 = rankUI.transform:Find("Stage/Level2");
	local level3 = rankUI.transform:Find("Stage/Level3");
	local level4 = rankUI.transform:Find("Stage/Level4");
	if percent >= stage2 then
		level4.gameObject:SetActive(true);
	elseif percent >= stage1 then
		level3.gameObject:SetActive(true);
	elseif percent >= stage0 then
		level2.gameObject:SetActive(true);
	else
		level1.gameObject:SetActive(true);
	end
	bar1.gameObject:SetActive(true);
	bar2.gameObject:SetActive(true);
	bar3.gameObject:SetActive(true);
	if percent < stage0 then
		bar1.value = CS.Mathf.InverseLerp(0,stage0,percent);
		reach1.gameObject:SetActive(false);
		level1.gameObject:SetActive(true);
	else
		bar1.value = 1;
		reach1.gameObject:SetActive(true);
	end
	if percent < stage1 then
		bar2.value = CS.Mathf.InverseLerp(stage0,stage1,percent);
		reach2.gameObject:SetActive(false);
	
	else
		bar2.value = 1;
		reach2.gameObject:SetActive(true);
	end
	if percent < stage2 then
		bar3.value = CS.Mathf.InverseLerp(stage1,stage2,percent);
		reach3.gameObject:SetActive(false);
	else
		bar3.value = 1;
		reach3.gameObject:SetActive(true);
	end
	local txtTotal = rankUI.transform:Find("Top/TotalScore/Text_TotalScore"):GetComponent(typeof(CS.ExText));
	local percentnum = CS.Mathf.CeilToInt(percent*100)/100;
	if percentnum>100 then
		percentnum = 100;
	end
	txtTotal.text = percentnum.."%";
	local itemParent = rankUI.transform:Find("RankingInfo/Main/Items");
	local bottom = rankUI.transform:Find("RankingInfo/Main/Bottom");
	for i=1,#datas do
		if itemParent.childCount<i+1 then
			local item = CS.UnityEngine.Object.Instantiate(itemParent:GetChild(0).gameObject, itemParent, false);
			item.transform:SetAsFirstSibling();
		end
	end
	for i=0,itemParent.childCount-2 do
		local item = itemParent:GetChild(i);
		local index = i+1;
		if datas[index] ~= nil then
			item.gameObject:SetActive(true);
			item:Find("Other/FirstBg").gameObject:SetActive(datas[index][6] == 1);
			item:Find("Other/SecondBg").gameObject:SetActive(datas[index][6] == 2);
			item:Find("Other/ThirdBg").gameObject:SetActive(datas[index][6] == 3);
			item:Find("Other/NormalBg").gameObject:SetActive(datas[index][6] > 3);
			local rank = item:Find("Other/Rank"):GetComponent(typeof(CS.ExText));
			rank.gameObject:SetActive(datas[index][6] > 3);
			if 	datas[index][6] < 10 then
				rank.text = "0"..tostring(datas[index][6])..".";
			else
				rank.text = tostring(datas[index][6])..".";
			end
			local txtName = item:Find("Other/Name/Name"):GetComponent(typeof(CS.ExText));
			txtName.text = datas[index][3];
			local serverName = item:Find("Other/Name/Server"):GetComponent(typeof(CS.ExText));
			serverName.text = datas[index][10];
			local txtLevel = item:Find("Other/Level"):GetComponent(typeof(CS.ExText));
			txtLevel.text = CS.System.String.Format(CS.Data.GetLang(39033), tostring(datas[index][4]));
			local txtScore = item:Find("Other/Tex_Score"):GetComponent(typeof(CS.ExText));
			txtScore.text = tostring(datas[index][5]);
			local imageHead = item:Find("Other/HeadImage"):GetComponent(typeof(CS.ExImage));
			CS.CommonController.LoadImageAvatarWithSequenceFrame(imageHead, datas[index][7]);
			CS.CommonController.LoadImageHeadFrameWithSequenceFrame(imageHead, datas[index][8]);
		else
			item.gameObject:SetActive(false);
		end
	end
	local userData = jsonData:GetValue("user_info");
	local rankcount = jsonData:GetValue("rank_count").Int;
	local userrank = userData:GetValue("rank").Int;
	local txtPlayerName = rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/Name/Name"):GetComponent(typeof(CS.ExText));
	txtPlayerName.text = CS.GameData.userInfo.name;
	local txtServerName = rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/Name/Server"):GetComponent(typeof(CS.ExText));
	txtServerName.text = CS.ConnectionController.currentServer.name;
	local txtPlayerLevel = rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/Level"):GetComponent(typeof(CS.ExText));
	txtPlayerLevel.text = CS.System.String.Format(CS.Data.GetLang(39033), tostring(CS.Data.GetUserInfo().level));
	local txtRankPercent = rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/Tex_RankPercent"):GetComponent(typeof(CS.ExText));
	if userrank> 0 then
		if userrank < 10 then
			txtRankPercent.text = "0"..tostring(userrank)..".";
		elseif userrank == 10 then
			txtRankPercent.text = tostring(userrank)..".";
		else
			local percent = (userrank/rankcount)*100;
		    CS.NDebug.Log("percent",percent,"userrank",userrank,"rankcount",rankcount);
			percent = CS.Mathf.CeilToInt(percent);
			txtRankPercent.text = percent.."%";
		end
	else
		txtRankPercent.text = CS.Data.GetLang(39032);
	end
	local txtPlayerCount = rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/Tex_Score"):GetComponent(typeof(CS.ExText));
	txtPlayerCount.text = tostring(CS.GameData.GetItem(9020));
	local spineholder = rankUI.transform:Find("Stage/SpineHolder");
	for i=0,spineholder.childCount-1 do
		local spine = spineholder:GetChild(i):GetComponent(typeof(CS.SkeletonAnimation));
		for j=0,spine.skeleton.Data.Animations.Count-1 do
			local anim = spine.skeleton.Data.Animations[j];
			if anim.Name == "sing" then
				spine.state:SetAnimation(0, "sing", true);
			elseif anim.Name == "s2" then
				spine.state:SetAnimation(0, "s2", true);
			end
		end
	end
	local effect = rankUI.transform:Find("RankingInfo/Main/PlayerRankItem/YY_feipiao"); 
	local ratio = CS.UnityEngine.Screen.height/CS.UnityEngine.Screen.width;
	print("ratio"..ratio);
	effect.localScale = CS.UnityEngine.Vector3(100,ratio*100/0.562,100);
	local itemnumOld = CS.UnityEngine.PlayerPrefs.GetInt("opsitem",0);
	local itemnumNew = CS.GameData.GetItem(9020);
	if itemnumOld ~= itemnumNew then
		effect.gameObject:SetActive(true);
		CS.UnityEngine.PlayerPrefs.SetInt("opsitem",itemnumNew);
		CS.UnityEngine.PlayerPrefs.Save();
	else
		effect.gameObject:SetActive(false);
	end
end

local ShowAllMission = function(self)
	if self.campaionId == -57 then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(60696));
		return;
	end
	self:ShowAllMission();
end
local checkRequestDrawEvent = false;

local RequestDrawEvent = function(self)
	if checkRequestDrawEvent then
		self:RequestDrawEvent();
	end
end
local Start = function(self)
	self:Start();
	checkRequestDrawEvent = true;
	CS.CommonController.Invoke(function()
		CS.OPSPanelController.Instance:RequestDrawEvent();
	end,0.2,CS.OPSPanelController.Instance);
	findSpot = true;
	local requestPrize = CS.RequestActivityEventPrize();
	requestPrize:Request();
end

local ShowCommonBattleSettlement = function(self)
	if CS.GameData.missionResult.rank ~= CS.Rank.C and CS.GameData.missionResult.rank ~= CS.Rank.D then
		lastWinmissionid = CS.GameData.currentSelectedMissionInfo.id;
	end
	self:ShowCommonBattleSettlement();
end
--打开奖励列表
function OpenRankingReward()
	CS.OPSEventPrizeController.OpenInOPS();
end

local RequestActivityEventPrizeHandle = function(self)
	self:RequestActivityEventPrizeHandle();
	if CS.OPSEventPrizeController.eventType == 1 then
		self.left:SetActive(false);
		self.adapterLayout.localPosition = CS.UnityEngine.Vector3.zero;
	end
end

function checkCanGetPrize()
	if CS.GameData.eventPrizeData.Count == 0 then
		return false;
	end
	--print("checkeventPrize");
	local prizeData = CS.GameData.eventPrizeData[0];
	local nums = CS.System.Collections.Generic.List(CS.System.Int32)(prizeData.prizeLevelInfo.num_prizeId.Keys);
	if prizeData.hasGet.Count >= nums.Count then
		return false;
	end
	for i=0,nums.Count-1 do
		local point = nums[i];
		local hasGet = prizeData.hasGet:Contains(i);
		local reach = prizeData.Num >= point;
		--print(point);
		if not hasGet and reach then
			return true;
		end
	end
	return false;
end

local ReadRecord = function(self)
	if currentSpot ~= nil then
		return true;
	end
	if onBattleSpot ~= nil then
		return true;
	end
	return self:ReadRecord();
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
local Awake = function(self)
	util.hotfix_ex(CS.OPSPanelController,'RefreshUI',RefreshUI)
	util.hotfix_ex(CS.OPSPanelController,'CancelMission',CancelMission)
	CS.OPSPanelController.diffclutyRecord = CS.Mathf.Max(0,CS.OPSPanelController.diffclutyRecord);
	checkRequestDrawEvent = false;
	self:Awake();
	checkRequestDrawEvent = true;
end
util.hotfix_ex(CS.OPSPanelController,'FindPanelMission',FindPanelMission)
util.hotfix_ex(CS.OPSPanelController,'SelectContainer',SelectContainer)
util.hotfix_ex(CS.OPSPanelController,'SelectModuleSpine',SelectModuleSpine)
util.hotfix_ex(CS.OPSPanelController,'ShowOPSSpineMissionUI',ShowOPSSpineMissionUI)
util.hotfix_ex(CS.OPSPanelController,'HideOPSSpineMissionUI',HideOPSSpineMissionUI)
util.hotfix_ex(CS.OPSPanelController,'CanGetPoint',CanGetPoint)
util.hotfix_ex(CS.OPSPanelController,'LoadReturn',myLoadReturn)
util.hotfix_ex(CS.OPSPanelController,'CheckEndlessPoint',CheckEndlessPoint)
util.hotfix_ex(CS.OPSPanelController,'CancelSelectMoudleSpine',CancelSelectMoudleSpine)
util.hotfix_ex(CS.OPSPanelController,'CheckMoudleUiTween',CheckMoudleUiTween)
util.hotfix_ex(CS.OPSPanelController,'RefreshMoudleBuildUI',RefreshMoudleBuildUI)
util.hotfix_ex(CS.OPSPanelController,'CheckMoudleUi',CheckMoudleUi)
util.hotfix_ex(CS.OPSPanelController,'CheckMoudleMissionTip',CheckMoudleMissionTip)
util.hotfix_ex(CS.OPSPanelController,'PlayMoudleBackgroundRailMove',PlayMoudleBackgroundRailMove)
util.hotfix_ex(CS.OPSPanelController,'RefreshCurrentDiffcluty',RefreshCurrentDiffcluty)
util.hotfix_ex(CS.OPSPanelController,'PlayMoudleBackgroundMove',PlayMoudleBackgroundMove)
util.hotfix_ex(CS.OPSPanelController,'CheckModuleSpine',CheckModuleSpine)
util.hotfix_ex(CS.OPSPanelController,'Load',Load)
util.hotfix_ex(CS.OPSPanelController,'RefreshMoudleUI',RefreshMoudleUI)
util.hotfix_ex(CS.OPSPanelController,'SelectOPSMission',SelectOPSMission)
util.hotfix_ex(CS.OPSPanelController,'OpenRuler',OpenRuler)
--util.hotfix_ex(CS.OPSPanelController,'LoadTitle',LoadTitle)
--util.hotfix_ex(CS.OPSPanelController,'RequestSetCampaigns',RequestSetCampaigns)
util.hotfix_ex(CS.OPSPanelController,'RequestSetDrawEvent',RequestSetDrawEvent)
util.hotfix_ex(CS.OPSPanelController,'GetAllGroupTotalHighScore',GetAllGroupTotalHighScore)
util.hotfix_ex(CS.OPSPanelController,'InitCameraBackground',InitCameraBackground)
util.hotfix_ex(CS.OPSPanelController,'SelectMissionSpot',SelectMissionSpot)
util.hotfix_ex(CS.OPSPanelController,'CheckSpecialAnim',CheckSpecialAnim)
util.hotfix_ex(CS.OPSPanelController,'Play3dSpotAnim',Play3dSpotAnim)
util.hotfix_ex(CS.OPSPanelController,'CheckMissionProcessData',CheckMissionProcessData)
util.hotfix_ex(CS.OPSPanelController,'ShowAllMission',ShowAllMission)
util.hotfix_ex(CS.OPSPanelController,'Awake',Awake)
util.hotfix_ex(CS.OPSPanelController,'Start',Start)
util.hotfix_ex(CS.OPSPanelController,'RequestDrawEvent',RequestDrawEvent)
util.hotfix_ex(CS.RequestDrawEvent,'SuccessJsonHandleData',SuccessJsonHandleData)
util.hotfix_ex(CS.DeploymentController,'ShowCommonBattleSettlement',ShowCommonBattleSettlement)
util.hotfix_ex(CS.OPSEventPrizeController,'RequestActivityEventPrizeHandle',RequestActivityEventPrizeHandle)
util.hotfix_ex(CS.OPSPanelBackGround,'ReadRecord',ReadRecord)
util.hotfix_ex(CS.HomeController,'InitUIElements',InitUIElements)