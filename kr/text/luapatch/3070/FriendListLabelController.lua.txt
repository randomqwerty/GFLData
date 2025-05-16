local util = require 'xlua.util'

local get_textServerName = function(self)
	return self.uiHolder:GetUIElement("FriendInfoItem/UI_Layout/LayoutServer/UI_Text_Server",typeof(CS.UnityEngine.UI.Text))
end
xlua.hotfix(CS.FriendListLabelController,'get_textServerName',get_textServerName)
