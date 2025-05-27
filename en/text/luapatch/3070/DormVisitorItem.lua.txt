local util = require 'xlua.util'
xlua.private_accessible(CS.DormVisitorItem)

local get_textServerName = function(self)
	return self.uiHolder:GetUIElement("UI_Layout/LayoutServer/UI_Text_Server",typeof(CS.UnityEngine.UI.Text))
end
local Init = function(self,data)
	self:Init(data)
	local parent = self.uiHolder:GetUIElement("UI_Layout/LayoutServer",typeof(CS.UnityEngine.GameObject))
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local target = self.uiHolder:GetUIElement("UI_Layout/LayoutServer/UI_Text_Server",typeof(CS.UnityEngine.UI.Text))
		if target ~= nil then
			target.text = self.friend.serverName
		end
		if parent ~= nil then
			parent:SetActive(true)
		end
	else
		if parent ~= nil then
			parent:SetActive(false)
		end
	end
end

xlua.hotfix(CS.DormVisitorItem,'get_textServerName',get_textServerName)
util.hotfix_ex(CS.DormVisitorItem,'Init',Init)



