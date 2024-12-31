local util = require 'xlua.util'
xlua.private_accessible(CS.CharacterVoiceController)
xlua.private_accessible(CS.CommonLive2DController)

local ShowDialog = function(self,message,name,isFetter)
	self:ShowDialog(message,name,isFetter);
	local newStr, count = string.gsub(message, "<.->", "")
	self.exDialogContent.text = newStr;
end

local TryGetText = function(self,live2DMotionData,no)
	local txt = self:TryGetText(live2DMotionData,no);
	local newStr, count = string.gsub(txt, "<.->", "")
	return newStr;
end
util.hotfix_ex(CS.CharacterVoiceController,'ShowDialog',ShowDialog)
util.hotfix_ex(CS.CommonLive2DController,'TryGetText',TryGetText)

