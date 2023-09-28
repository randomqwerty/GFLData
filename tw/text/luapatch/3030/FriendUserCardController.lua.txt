local util = require 'xlua.util'
xlua.private_accessible(CS.FriendUserCardController)

local Init_New = function(self)
    local checkNode = self.uiHolder:GetUIElement("CheckNode",typeof(CS.UnityEngine.GameObject));
    checkNode:SetActive(true)
    self:Init()
end


util.hotfix_ex(CS.FriendUserCardController,'Init',Init_New)

