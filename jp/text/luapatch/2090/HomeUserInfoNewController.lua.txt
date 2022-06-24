local util = require 'xlua.util'
xlua.private_accessible(CS.HomeUserInfoNewController)

local _InitEmoji = function(self)
	self:InitEmoji();
	
	if self.fairyCollectionObj.activeSelf then
		local acquired = CS.GameData.userInfo.listFairyCollect.Count;
        local amount = CS.GameData.listFairyInfo.Count;
        local length = CS.GameData.listFairyInfo.Count-1;
         local fairy;
		for i=0,length do
			fairy=CS.GameData.listFairyInfo:GetDataByIndex(i);
			if fairy.type ==CS.FairyType.Fake or fairy.isAdditional or fairy.id == 90004 or fairy.id == 90003 then
				amount=amount-1;
			end	
		end 
		local id;
		length=CS.GameData.userInfo.listFairyCollect.Count-1;
		for i=0,length do
			id=CS.GameData.userInfo.listFairyCollect[i];
			fairy=CS.GameData.listFairyInfo:GetDataById(id);
			if fairy.isAdditional then
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
local _Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
		
		local timeTextObj =  CS.UnityEngine.Object.Instantiate(self.textUserID.gameObject); 

		timeTextObj.transform:SetParent(self.textUserID.transform.parent, false);
		timeTextObj.transform.localPosition= CS.UnityEngine.Vector3(timeTextObj.transform.localPosition.x+200,timeTextObj.transform.localPosition.y,0);
	
		local curStamp = CS.GameData.GetCurrentTimeStamp();
        local curDateTime = CS.Data.ConvertDataTime(curStamp);
		local timeText=timeTextObj:GetComponent(typeof(CS.ExText));

        timeText.text = CS.System.String.Format(CS.Data.GetLang(20069), curDateTime);
	end 
end
util.hotfix_ex(CS.HomeUserInfoNewController,'Awake',_Awake) 
util.hotfix_ex(CS.HomeUserInfoNewController,'InitEmoji',_InitEmoji) 



