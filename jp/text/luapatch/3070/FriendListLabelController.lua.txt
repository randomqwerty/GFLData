local util = require 'xlua.util'

local get_textServerName = function(self)
	return self.uiHolder:GetUIElement("FriendInfoItem/UI_Layout/LayoutServer/UI_Text_Server",typeof(CS.UnityEngine.UI.Text))
end
local Init = function(self)
	self:Init()
	local parent = self.uiHolder:GetUIElement("FriendInfoItem/UI_Layout/LayoutServer",typeof(CS.UnityEngine.GameObject))
	if parent ~= nil then
		parent:SetActive(CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal)
	end
end
xlua.hotfix(CS.FriendListLabelController,'get_textServerName',get_textServerName)
util.hotfix_ex(CS.FriendListLabelController,'Init',Init)