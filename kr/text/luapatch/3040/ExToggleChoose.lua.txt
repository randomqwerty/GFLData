local util = require 'xlua.util'
xlua.private_accessible(CS.ExToggleChoose)
xlua.private_accessible(CS.ExToggle)

local ExToggleChooseAwake = function(self)
	self:Awake();
	if self.openAudioEventId ~= 0 then
		self.openAudioEventClass = CS.Data.GetAudioEventClass(self.openAudioEventId);
	end
	if self.closeAudioEventId ~= 0 then
		self.closeAudioEventClass = CS.Data.GetAudioEventClass(self.closeAudioEventId);
	end
	if self.groupAudioEventId ~= 0 then
		self.groupAudioEventClass = CS.Data.GetAudioEventClass(self.groupAudioEventId);
	end
end
local ExToggleAwake = function(self)
	self:Awake();
	if self.openAudioEventId ~= 0 then
		self.openAudioEventClass = CS.Data.GetAudioEventClass(self.openAudioEventId);
	end
	if self.closeAudioEventId ~= 0 then
		self.closeAudioEventClass = CS.Data.GetAudioEventClass(self.closeAudioEventId);
	end
	if self.groupAudioEventId ~= 0 then
		self.groupAudioEventClass = CS.Data.GetAudioEventClass(self.groupAudioEventId);
	end
end
util.hotfix_ex(CS.ExToggleChoose,'Awake',ExToggleChooseAwake)
util.hotfix_ex(CS.ExToggle,'Awake',ExToggleAwake)
