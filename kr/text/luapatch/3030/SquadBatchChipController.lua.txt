local util = require 'xlua.util'
xlua.private_accessible(CS.SquadBatchChipController)

local _Init = function(self,newChip,info,controller)
	self:Init(newChip,info,controller)
	self.textPoint.text = tostring(info.unlock_chip_point)
end


util.hotfix_ex(CS.SquadBatchChipController,'Init',_Init)