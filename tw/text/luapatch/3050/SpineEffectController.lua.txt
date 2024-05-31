local util = require 'xlua.util'
xlua.private_accessible(CS.SpineEffectFilter)

local _SpineEffectFilter = function(self,filterMode,anims)
	self.listAnim:Add("r_wait");
	self.listAnim:Add("r_move");
end

util.hotfix_ex(CS.SpineEffectFilter,'.ctor',_SpineEffectFilter)

