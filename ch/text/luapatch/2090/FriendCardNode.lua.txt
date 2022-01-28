local util = require 'xlua.util'
xlua.private_accessible(CS.FriendCardNode)
xlua.private_accessible(CS.FairyInfo)


local _InitGender = function(self)
	self:InitGender();
	if self.userCard ~=nil then
		local show= self.userCard.uid == CS.GameData.userInfo.userId;
		self.storyCollectionText.transform.parent.gameObject:SetActive(show);
		self.gunCollectionText.transform.parent.gameObject:SetActive(show);
		self.furnitureCollectionText.transform.parent.gameObject:SetActive(show);
		self.fairyCollectionText.transform.parent.gameObject:SetActive(show);
	end
 
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


util.hotfix_ex(CS.FriendCardNode,'InitGender',_InitGender)