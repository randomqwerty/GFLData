local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.ResCenter)
xlua.private_accessible(CS.PassOrderController)
--修正home界面下载对话框显示
local SevenLoginHandler = function(self)
	self:SevenLoginHandler(); 
	CS.ResCenter.instance.currentNeedUnCompress = nil;
	if CS.ResCenter.instance.currentDownloadState ~= CS.ResCenter.DownloadAddState.DownloadAddInHome and 
		CS.ResCenter.instance.currentDownloadVoiceState ~= CS.ResCenter.DownloadVoiceState.DownloadInHome then
		return;
	end
	if CS.ResCenter.instance.resDownload ~= nil and not CS.ResCenter.instance.resDownload:isNull() then
		CS.ResCenter.instance.resDownload:Hide();
	end
end

local myOnApplicationFocus = function(self, isFocus)
	if isFocus == true then
		if((CS.PassOrderController.Instance ~= nil and CS.PassOrderController.Instance.gameObject.activeInHierarchy)) then
			
		else
			self:OnApplicationFocus(isFocus); 
		end
	end
end
local myCheckPassOrderScaleUI = function(self, isScale)
	if(isScale == false) then
		if (CS.PassOrderConfig.Instance.passEnter == true and CS.PassOrderUserData.Instance:HasActivePassOrder() ~= nil) then
			self.btnPassObj:SetActive(true);
		end
		else
	self:CheckPassOrderScaleUI(isScale)
	end
end

local ShowUI = function(self)
	self:ShowUI();
	if CS.GameData.missionAction ~= nil then
		local campaionid = CS.GameData.missionAction.missionInfo.campaign;
		if campaionid == -54 then
			local ids = CS.System.Collections.Generic.List(CS.System.Int32)();
			ids:Add(campaionid);
			local Request = CS.RequestDrawEvent(ids);
			Request:Request();	
		end
	end
end
local InitEmoji = function(self)
	self:InitEmoji();
	if self.fairyCollectionObj.activeSelf then
		local acquired = CS.GameData.userInfo.listFairyCollect.Count;
        local amount = CS.GameData.listFairyInfo.Count;
        local length = CS.GameData.listFairyInfo.Count-1;
         local fairy;
		for i=0,length do
			fairy=CS.GameData.listFairyInfo:GetDataByIndex(i);
			if fairy.type ==CS.FairyType.Fake or fairy.isAdditional or fairy.id == 90004 or fairy.id == 90003 or fairy.id == 90002 or fairy.id == 90001 then
				amount=amount-1;
			end	
		end 
		local id;
		length=CS.GameData.userInfo.listFairyCollect.Count-1;
		for i=0,length do
			id=CS.GameData.userInfo.listFairyCollect[i];
			fairy=CS.GameData.listFairyInfo:GetDataById(id);
			if fairy.isAdditional or fairy.id == 90004 or fairy.id == 90003 or fairy.id == 90002 or fairy.id == 90001 then
				acquired=acquired-1;
			end	
		end
		--print("clolect:"..acquired);
		--print("all:"..amount);
		local rate=100.0 * acquired / amount;
		local s=tostring(rate);
		if acquired == amount then
			self.fairyCollectionText.text = "100%";
		else
			if rate > 10.0 then
				self.fairyCollectionText.text = string.sub(s, 0 , 2).."%";
			else
				self.fairyCollectionText.text = string.sub(s, 0 , 1).."%";
			end
		end
	end
end
util.hotfix_ex(CS.HomeController,'SevenLoginHandler',SevenLoginHandler)
--util.hotfix_ex(CS.HomeController,'OnApplicationFocus',myOnApplicationFocus)
util.hotfix_ex(CS.HomeController,'CheckPassOrderScaleUI',myCheckPassOrderScaleUI)
util.hotfix_ex(CS.HomeController,'ShowUI',ShowUI)
util.hotfix_ex(CS.HomeUserInfoNewController,'InitEmoji',InitEmoji)


