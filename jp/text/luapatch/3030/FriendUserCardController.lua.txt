local util = require 'xlua.util'
xlua.private_accessible(CS.FriendUserCardController)

local Init_New = function(self)
    local checkNode = self.uiHolder:GetUIElement("CheckNode",typeof(CS.UnityEngine.GameObject));
    checkNode:SetActive(true)
    self:Init()
end

local SwitchDormHandle_New = function(self,...)
    if CS.CommonSceneManagerController.instance.currentSceneName == "Dorm" and CS.DormUIController.Instance ~= nil then
    	CS.DormUIController.Instance:SwitchDormRoom(0)
    	self:Close()
    else
    	CS.CommonController.GotoScene("Dorm")
    end
end

local SwitchVehicleRoomHandle_New = function(self,...)
    if CS.CommonSceneManagerController.instance.currentSceneName == "Dorm" and CS.DormUIController.Instance ~= nil then
    	CS.DormUIController.Instance:SwitchFriendVehicleRoom()
    	self:Close()
    else
    	CS.CommonController.GotoScene("Dorm")
    end
end


util.hotfix_ex(CS.FriendUserCardController,'Init',Init_New)
util.hotfix_ex(CS.FriendUserCardController,'SwitchDormHandle',SwitchDormHandle_New)
util.hotfix_ex(CS.FriendUserCardController,'SwitchVehicleRoomHandle',SwitchVehicleRoomHandle_New)


