local util = require 'xlua.util'
xlua.private_accessible(CS.FetterStoryController)

local OnBackBtnClicked_New = function(self)
	self:OnBackBtnClicked()

	if CS.ResCenter.instance.currentSceneName == "Dorm" then
		if CS.DormController.instance.currentMode ~= CS.DormMode.Establish or CS.DormController.currentRoom ~= CS.EstablishRoom.DataRoom then
			CS.DormUIController.Instance:SwitchEstablishRoom(CS.EstablishRoom.DataRoom)
		end
	end
end


util.hotfix_ex(CS.FetterStoryController,'OnBackBtnClicked',OnBackBtnClicked_New)
