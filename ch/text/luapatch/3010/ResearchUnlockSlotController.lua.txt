local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchUnlockSlotController)

local SpineSpecilEffect = function(self, spine,gun)
	self:SpineSpecilEffect(spine,gun)

    if self.mSpineMemberControl ~= nil then
		self.mSpineMemberControl.isInCanvas = true
	end
end
local AddSangvisMuzzleBlackList = function(self)
	self:AddSangvisMuzzleBlackList()
	self.muzzleBlackList:Add("Scarecrow_SpringFes")
end
local AddSangvisMuzzle2BlackList = function(self)
	self:AddSangvisMuzzle2BlackList()
	self.muzzle2BlackList:Add("Scarecrow_SpringFes")
end

util.hotfix_ex(CS.ResearchUnlockSlotController,'SpineSpecilEffect',SpineSpecilEffect)
util.hotfix_ex(CS.ResearchUnlockSlotController,'AddSangvisMuzzleBlackList',AddSangvisMuzzleBlackList)
util.hotfix_ex(CS.ResearchUnlockSlotController,'AddSangvisMuzzle2BlackList',AddSangvisMuzzle2BlackList)