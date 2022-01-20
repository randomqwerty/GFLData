local util = require 'xlua.util'
xlua.private_accessible(CS.FriendCardNode)


local _InitGender = function(self)
	self:InitGender();
	if self.userCard ~=nil then
		local show= self.userCard.uid == CS.GameData.userInfo.userId;
		self.storyCollectionText.transform.parent.gameObject:SetActive(show);
		self.gunCollectionText.transform.parent.gameObject:SetActive(show);
		self.furnitureCollectionText.transform.parent.gameObject:SetActive(show);
		self.fairyCollectionText.transform.parent.gameObject:SetActive(show);
	end
end


util.hotfix_ex(CS.FriendCardNode,'InitGender',_InitGender)