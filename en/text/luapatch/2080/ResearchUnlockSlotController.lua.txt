local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchUnlockSlotController)

local AddSangvisMuzzle2BlackList = function(self)
	self:AddSangvisMuzzle2BlackList()
	self.muzzle2BlackList:Add("Intruder_Halloween")
end

util.hotfix_ex(CS.ResearchUnlockSlotController,'AddSangvisMuzzle2BlackList',AddSangvisMuzzle2BlackList)

