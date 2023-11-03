local util = require 'xlua.util'
xlua.private_accessible(CS.FriendChatBoxController)
xlua.private_accessible(CS.RequestSendMessage)

 

local mOnSendSuccess = function(self,result)

	if result.selfMessage~=nil and result.selfMessage.fromMe==true then
		local msg = result.selfMessage.message;
		--print(msg)
		result.selfMessage.message = CS.Data.CheckForbidWord(msg);
		--print(result.selfMessage.message)
	end
	self:OnSendSuccess(result);
end

util.hotfix_ex(CS.FriendChatBoxController,'OnSendSuccess',mOnSendSuccess)