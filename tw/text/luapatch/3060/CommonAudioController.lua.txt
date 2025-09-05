local util = require 'xlua.util'
xlua.private_accessible(CS.CommonAudioController)

local PlayCharacterVoiceHandle = function(self, characterName, ...)
	if characterName ~= nil then
		characterName = string.gsub(characterName, "ModMod", "Mod")
	end
	return self:PlayCharacterVoiceHandle(characterName, ...)
end

util.hotfix_ex(CS.CommonAudioController,'PlayCharacterVoiceHandle',PlayCharacterVoiceHandle)


