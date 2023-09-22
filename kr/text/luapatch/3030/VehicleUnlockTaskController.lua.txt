local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleUnlockTaskController)

local _Jump = function(self)
	self:Jump();
	
	if self.taskInfo.isFunctionOpen == true then
		if CS.ResCenter.instance.currentSceneName == "Dorm" then
			if CS.DormController.currentRoom == CS.EstablishRoom.VehicleRoom then
				CS.CommonSceneManagerController.instance:Clear();
			end
		end
	end
end


util.hotfix_ex(CS.VehicleUnlockTaskController,'Jump',_Jump)