local util = require 'xlua.util'
xlua.private_accessible(CS.BattleInteractionController)
local BattleController = CS.GF.Battle.BattleController
local LerpCameraPosition = function(self,targetpos)

	self.switchedCharacter = false
	self:LerpCameraPosition(targetpos)
end
local SLGClampCameraPosition = function(self)

	if BattleController.Instance.EntranceType == CS.BattleEntranceType.SLGMiniGame then
		local x = CS.BattleInteractionController.dragOffset.x - 2
		if x < -2 then 
			x = -2 
		end
		if x > -2+CS.GF.Battle.BattleSLGModeController.gridLength then
			x = -2 + CS.GF.Battle.BattleSLGModeController.gridLength
		end
	
		if CS.BattleInteractionController.scale < 1 then
			CS.BattleInteractionController.scale = 1
		end
		if CS.BattleInteractionController.scale > 5 then
			CS.BattleInteractionController.scale = 5
		end
		local scale = CS.BattleInteractionController.scale
		self.transformCameraPosition.localPosition = CS.UnityEngine.Vector3(x,-0.4444444 * scale,scale)
	end
	--print('SLGClampCameraPosition '..self.transformCameraPosition.localPosition)
end
local SLGUpdateDragOffset = function(self)
	local maxwid = CS.GF.Battle.BattleSLGModeController.Instance:GetFrontlineWidth()
	if CS.BattleInteractionController.dragOffset.x > maxwid then
		CS.BattleInteractionController.dragOffset = CS.UnityEngine.Vector2(maxwid,CS.BattleInteractionController.dragOffset.y) 
	end
end

local UpdateScalePos = function(self)
	if BattleController.Instance.EntranceType == CS.BattleEntranceType.SLGMiniGame then
		self:SLGUpdateDragOffset()
	else
		self:UpdateScalePos()
	end
end
util.hotfix_ex(CS.BattleInteractionController,'LerpCameraPosition',LerpCameraPosition)
util.hotfix_ex(CS.BattleInteractionController,'SLGClampCameraPosition',SLGClampCameraPosition)
util.hotfix_ex(CS.BattleInteractionController,'SLGUpdateDragOffset',SLGUpdateDragOffset)
util.hotfix_ex(CS.BattleInteractionController,'UpdateScalePos',UpdateScalePos)
