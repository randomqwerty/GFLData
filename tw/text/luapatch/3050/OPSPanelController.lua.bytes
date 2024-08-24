local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.OPSPanelBackGround)
xlua.private_accessible(CS.OPSPanelSpot)
xlua.private_accessible(CS.OPSLetterWriteController)
xlua.private_accessible(CS.RequsetGetAllLetterData)
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
local MoveMissionHolder = function(self)
	self:MoveMissionHolder();
	if CS.OPSPanelBackGround.Instance.spotMissionHolders.Count == 0 then
		local movespot = nil;
		for i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
			local spot = CS.OPSPanelBackGround.Instance.all3dSpots[i];
			if movespot == nil then
				if spot.CanShow and spot.mission ~= nil and spot.mission.showNewTag then
					movespot = spot;
				end
			end
		end
		if movespot ~= nil then
			local pos = CS.UnityEngine.Vector2(movespot.transform.localPosition.x,movespot.transform.localPosition.y);
			CS.OPSPanelBackGround.Instance:Move(pos,true, 0.7);
		end
	end
end
local CancelMission = function(self)
	if self.chooseSpot ~= nil then
		local select = self.chooseSpot.transform:Find("Img_Selected");
		if select~= nil then
			select.gameObject:SetActive(false);
		end
		self.chooseSpot:ShowNewTag();
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
	local combat = self.transform:Find("InCombat");
	if combat ~= nil then 
		if self.mission ~= nil then
			local inbattle = self.opsMission:isInCombat();
			combat.gameObject:SetActive(inbattle);
		else
			combat.gameObject:SetActive(false);
		end
	end
end
local CheckIsolateSpots = function(self)
	self:CheckIsolateSpots();
	for i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
		local spot = CS.OPSPanelBackGround.Instance.all3dSpots:GetDataByIndex(i);
		if spot.holder == nil then
			if not self.playSpots:Contains(spot) then
				if spot.mission ~= nil and not CS.SpecialActivityController.missionid_State:ContainsKey(spot.mission.missionInfo.id) then
					self.playSpots:Add(spot);
				end
			end
			spot:Show();
		end
	end
end
local RequestSetDrawEvent = function(self,data)
	self:RequestSetDrawEvent(data);
	self:LoadLetterUI();
end
local LoadLetterUI = function(self)
	self:LoadLetterUI();
	if self.letterUI ~= nil and not self.letterUI:isNull() then
		local read = CS.UnityEngine.PlayerPrefs.GetInt("isLetterInlet",0);
		if read == 0 then
			self:ShowLetterEvent();	
			CS.UnityEngine.PlayerPrefs.SetInt("isLetterInlet",1);
			CS.UnityEngine.PlayerPrefs.Save();	
		end
	end
end
local ShowLetterList = function(self)
	self:ShowLetterList();
	local read = CS.UnityEngine.PlayerPrefs.GetInt("isFirstLetterTip",0);
	if read == 0 then
		PlayGuide("isFirstLetterTip");
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
local InitUIElements = function(self)
	self:InitUIElements();
	self.btnGunSure:AddOnClick(function()
		self.goGunFliter:SetActive(false);
	end)
	local btn = self.transform:Find("Btn_Tutorials"):GetComponent(typeof(CS.ExButton));
	btn:AddOnClick(function()
		PlayGuide("isLetterPerTip");
	end)	
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
local CheckLetterText = function(self,txt)
	self:CheckLetterText(txt);
	local length = utf8len(self.lastText);
	self.txtLimit.text = tostring(length).."/"..tostring(CS.OPSLetterListController.Instance.LetterContentLengthLimit-1);
end
local EditLetter = function(self)
	if CS.ResCenter.CONGIGNAME == "IosResConfigData2018.txt" then
		if self.letterEdit == nil or self.letterEdit:isNull() then
			self.letterEdit = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath(self.EditLetterPath), CS.OPSPanelController.Instance.transform);
			self.inputField = self.letterEdit.transform:Find("Img_Background/Main"):GetComponent(typeof(CS.UnityEngine.UI.InputField));
			self.inputField.onEndEdit:AddListener(function(txt)
				self:EndInput(txt);
			end);
			self.scrollrect = self.letterEdit.transform:Find("Img_Background/Main"):GetComponent(typeof(CS.UnityEngine.UI.ScrollRect));
			self.layout = self.letterEdit.transform:Find("Img_Background/Main/Layout"):GetComponent(typeof(CS.UnityEngine.RectTransform));
			self.txtCheck = self.letterEdit.transform:Find("Img_Background/Main/Layout/Text_Check"):GetComponent(typeof(CS.ExText));
			self.txtLimit = self.letterEdit.transform:Find("Img_Background/Text_WordsNum"):GetComponent(typeof(CS.ExText));
			self.txtCheck.gameObject:SetActive(true);
			self.txtCheck.color = CS.UnityEngine.Color(0, 0, 0, 0);
			self.inputField.onValueChanged:AddListener(function(txt)
				self:CheckLetterText(txt);
			end);
			local btnBack = self.letterEdit.transform:Find("Img_Background/Btn_Back"):GetComponent(typeof(CS.ExButton));
			btnBack:AddOnClick(function()
				self:LeaveEditLetter();
			end);
		end
		self.inputField.text = self.letterData.content;
		self.letterEdit.gameObject:SetActive(true);
	else
		self:EditLetter();
	end
	local length = utf8len(self.letterData.content);
	self.txtLimit.text = tostring(length).."/"..tostring(CS.OPSLetterListController.Instance.LetterContentLengthLimit-1);
end
local LeaveEditLetter = function(self)
	if CS.ResCenter.CONGIGNAME == "IosResConfigData2018.txt" then
		if self.CheckForbidWord and CS.Data.IsContainForbidWord(self.inputField.text) then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(110019));
			return;
		end
		self.letterData.content = self.inputField.text;
		self.letterEdit.gameObject:SetActive(false);
		self.txtConcent.text = self.letterData.content;
	else
		self:LeaveEditLetter();
	end
end
local RefreshSangvisUI = function(self)
	self:RefreshSangvisUI();
	local typeTrans = self.transform:Find("SangvisFrame/Top/Type");
	local holder = typeTrans:GetComponent(typeof(CS.UGUISpriteHolder));
	local type = 0;
	if self.letterInfo.sangvisGunInfo.forces == CS.SangvisForceType.sangvis then
		type = 1;
	elseif self.letterInfo.sangvisGunInfo.forces == CS.SangvisForceType.KCCO then
		type = 2;
	elseif self.letterInfo.sangvisGunInfo.forces == CS.SangvisForceType.paradeus then
		type = 3;
	end
	typeTrans:GetComponent(typeof(CS.ExImage)).sprite = holder.listSprite[type];
end
local CheckRenderTexture = function(self)
	if self.rendTexture ~= nil then
		CS.UnityEngine.Object.DestroyImmediate(self.rendTexture);
	end
	local x = CS.Mathf.CeilToInt(self.rectTrans.sizeDelta.x);
	local y = CS.Mathf.CeilToInt(self.rectTrans.sizeDelta.y);
	self.rendTexture = CS.UnityEngine.RenderTexture(x,y,0,CS.UnityEngine.RenderTextureFormat.ARGB32);
	self.captureCamera.targetTexture = self.rendTexture;
end
function utf8len(input)
	local len  = string.len(input)
	local left = len
	local cnt  = 0
	local arr  = {0, 0xc0, 0xe0, 0xf0, 0xf8, 0xfc}
	while left ~= 0 do
		local tmp = string.byte(input, -left)
		local i   = #arr
		while arr[i] do
			if tmp >= arr[i] then
				left = left - i
				break
			end
			i = i - 1
		end
		cnt = cnt + 1
	end
	return cnt
end
local SuccessJsonHandleData = function(self,jsonData)
	CS.GameData.listLetterData:Clear();
	self:SuccessJsonHandleData(jsonData);
end
util.hotfix_ex(CS.OPSPanelController,'ReturnContainerPos',ReturnContainerPos)
util.hotfix_ex(CS.OPSPanelController,'CanChooseDrag',CanChooseDrag)
util.hotfix_ex(CS.OPSPanelController,'ShowProcessAllMission',ShowProcessAllMission)
util.hotfix_ex(CS.OPSPanelController,'MoveSelectDiskMission',MoveSelectDiskMission)
util.hotfix_ex(CS.OPSPanelController,'MoveSpine',MoveSpine)
util.hotfix_ex(CS.OPSPanelController,'MoveMissionHolder',MoveMissionHolder)
util.hotfix_ex(CS.OPSPanelController,'CancelMission',CancelMission)
util.hotfix_ex(CS.OPSPanelController,'CheckIsolateSpots',CheckIsolateSpots)
util.hotfix_ex(CS.OPSPanelController,'RequestSetDrawEvent',RequestSetDrawEvent)
util.hotfix_ex(CS.OPSPanelController,'LoadLetterUI',LoadLetterUI)
util.hotfix_ex(CS.OPSPanelController,'ShowLetterList',ShowLetterList)
util.hotfix_ex(CS.OPSPanelBackGround,'CheckNewsPos',CheckNewsPos)
util.hotfix_ex(CS.OPSPanelSpot,'ShowNewTag',ShowNewTag)
util.hotfix_ex(CS.OPSPanelSpot,'Init',Init)
util.hotfix_ex(CS.OPSPanelSpot,'Show',Show)
util.hotfix_ex(CS.OPSLetterListController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.OPSLetterWriteController,'CheckLetterText',CheckLetterText)
util.hotfix_ex(CS.OPSLetterWriteController,'EditLetter',EditLetter)
util.hotfix_ex(CS.OPSLetterWriteController,'LeaveEditLetter',LeaveEditLetter)
util.hotfix_ex(CS.OPSLetterWriteController,'CheckRenderTexture',CheckRenderTexture)
util.hotfix_ex(CS.OPSLetterLabel,'RefreshSangvisUI',RefreshSangvisUI)
util.hotfix_ex(CS.RequsetGetAllLetterData,'SuccessJsonHandleData',SuccessJsonHandleData)
