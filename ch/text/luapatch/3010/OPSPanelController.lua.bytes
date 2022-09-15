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

local CancelMission = function(self)
	self:CancelMission();
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
local Load = function(self,campaion)
	self:Load(campaion);
	if campaion == -54 then
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

local SelectOPSMission = function(self,opsmission,item)
	self.checkPosMin = self.checkPosMax - self.num * self.distance;
	if not self.useOPSmissions:Contains(opsmission) then
		self.useOPSmissions:Add(opsmission);
	end
	self:SelectOPSMission(opsmission,item);
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
local RequestSetCampaigns = function(self,data)
	self:RefreshUI();
end
local LoadTitle = function(self)
	self:LoadTitle();
	self:CheckConfigTip();
end
local RequestSetDrawEvent = function(self,data)
	self:RefreshUI(true);
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
util.hotfix_ex(CS.OPSPanelController,'SelectModuleSpine',SelectModuleSpine)
util.hotfix_ex(CS.OPSPanelController,'ShowOPSSpineMissionUI',ShowOPSSpineMissionUI)
util.hotfix_ex(CS.OPSPanelController,'HideOPSSpineMissionUI',HideOPSSpineMissionUI)
util.hotfix_ex(CS.OPSPanelController,'CanGetPoint',CanGetPoint)
util.hotfix_ex(CS.OPSPanelController,'LoadReturn',myLoadReturn)
util.hotfix_ex(CS.OPSPanelController,'CheckEndlessPoint',CheckEndlessPoint)
util.hotfix_ex(CS.OPSPanelController,'CancelSelectMoudleSpine',CancelSelectMoudleSpine)
util.hotfix_ex(CS.OPSPanelController,'CheckMoudleUiTween',CheckMoudleUiTween)
util.hotfix_ex(CS.OPSPanelController,'RefreshMoudleBuildUI',RefreshMoudleBuildUI)
util.hotfix_ex(CS.OPSPanelController,'CancelMission',CancelMission)
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
util.hotfix_ex(CS.OPSPanelController,'LoadTitle',LoadTitle)
util.hotfix_ex(CS.OPSPanelController,'RequestSetCampaigns',RequestSetCampaigns)
util.hotfix_ex(CS.OPSPanelController,'RequestSetDrawEvent',RequestSetDrawEvent)
util.hotfix_ex(CS.OPSPanelController,'GetAllGroupTotalHighScore',GetAllGroupTotalHighScore)