local util = require 'xlua.util'
xlua.private_accessible(CS.BattleInteractionController)
--xlua.private_accessible(CS.GF.Tarkov.TarkovDragItem)

local Init = function(self)
	self:Init()	
	local aspectFixed = 1.778
	self.cameraController.battleMainCamera.orthographicSize = 8 / CS.UnityEngine.Screen.width * CS.UnityEngine.Screen.height * aspectFixed
end

--local GetScreenWidth = function(self)
--	local aspect = 1.778
--	local worldHeight = self.cameraController.battleMainCamera.orthographicSize * 2
--	return worldHeight * aspect
--	
--end

util.hotfix_ex(CS.BattleInteractionController,'Init',Init)


