local util = require 'xlua.util'
xlua.private_accessible(CS.FriendFriendMallController)

--暂时关闭头像框标签
local InitUIElements = function(self)
	self:InitUIElements();
	self.toggleHeadFrame.gameObject:SetActive(false);
	self.toggleHomeBg.transform.localPosition = CS.UnityEngine.Vector3(570,-10,0);
end

util.hotfix_ex(CS.FriendFriendMallController,'InitUIElements',InitUIElements)