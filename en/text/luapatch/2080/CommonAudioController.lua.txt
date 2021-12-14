local util = require 'xlua.util'
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.AVGController)

local StopBattleAudio = function(self, type)
	if type == CS.AudioSourceType.SoundSource and CS.AVGController.inst ~= nil and not CS.AVGController.inst:isNull() then
		if CS.AVGController.inst.isTypeWriterPlaying then
			return;
		end
	end
	self:StopBattleAudio(type);
end

util.hotfix_ex(CS.CommonAudioController,'StopBattleAudio',StopBattleAudio)


