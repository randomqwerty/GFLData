local util = require 'xlua.util'
xlua.private_accessible(CS.CreationVisionEffect)

local animDuration = 4
local animDelay = 2.25
local animStartFrame = 0
local TargetBuffID = 4558
local castskillflag = false
local GetPercent = function(self)
	local value = self:GetPercent()
	if self.target ~= nil then
		local chargeBuffTier = self.target:GetComponent(typeof(CS.GF.Battle.BattleCharacterController)).conditionListSelf:GetTierByID(TargetBuffID)
		if castskillflag and chargeBuffTier <= 0 then
			castskillflag = false
			animStartFrame = CS.BattleFrameManager.Instance:GetCurFrame()
		end
		if not castskillflag and chargeBuffTier > 0 then
			castskillflag = true
			animStartFrame = CS.BattleFrameManager.Instance:GetCurFrame()
		end
		if castskillflag then
			local curframe = CS.BattleFrameManager.Instance:GetCurFrame()
			local timer = ((curframe - animStartFrame) / 30) - animDelay
			if timer > animDuration then
				timer = animDuration
			end
			local lightRange = ((animDuration - timer) / animDuration)
			if lightRange > 1 then
				lightRange = 1
			end
			print (lightRange..' '..timer..' '..value)
			if value > 1-lightRange then
				return 1-lightRange
			else
				return value
			end
		else
			return value
		end
	end
	return value
	
end

util.hotfix_ex(CS.CreationVisionEffect,'GetPercent',GetPercent)