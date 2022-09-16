local util = require 'xlua.util'
xlua.private_accessible(CS.Mail)

function Check()
	CS.UIManager.Instance:DequeuePerformance();
end

local RequestMailResourceHandle = function(self,www)
	self:RequestMailResourceHandle(www);
	if self.type==CS.MailType.medal then
		local mail_id =  self.id;
		CS.GameData.listMail:Remove(mail_id);
	end
	CS.CommonController.Invoke(Check,0.1,CS.UIManager.Instance);
end

util.hotfix_ex(CS.Mail,'RequestMailResourceHandle',RequestMailResourceHandle)



