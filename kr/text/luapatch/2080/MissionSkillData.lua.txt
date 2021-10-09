local util = require 'xlua.util'

local DeathEffect = function(self)
	if self.lastEffect ~= nil and not self.lastEffect:isNull() then
		if self.lastEffect.name == "Viscosity_Bomb(Clone)" then
			CS.CommonAudioController.PlayBattle("Stop_Battle_loop");
		end
	end
	self:DeathEffect();
end

util.hotfix_ex(CS.SpecialSpotAction,'DeathEffect',DeathEffect)