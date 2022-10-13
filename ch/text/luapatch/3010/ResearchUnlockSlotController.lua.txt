local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchUnlockSlotController)

local SpineSpecilEffect = function(self, spine,gun)
	self:SpineSpecilEffect(spine,gun)

    if self.mSpineMemberControl ~= nil then
		self.mSpineMemberControl.isInCanvas = true
	end
end

util.hotfix_ex(CS.ResearchUnlockSlotController,'SpineSpecilEffect',SpineSpecilEffect)