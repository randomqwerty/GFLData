local util = require 'xlua.util'

Awake = function()
end

Start = function()
	local bgmName = "BGM_Empty"
	if bgmNameObj ~= nil then
		bgmName = bgmNameObj.name
	end
	CS.CommonAudioController.PlayBGM(bgmName)
end