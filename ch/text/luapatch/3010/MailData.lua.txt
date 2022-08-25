local util = require 'xlua.util'
xlua.private_accessible(CS.Mail)

function Check()
	CS.UIManager.Instance:DequeuePerformance();
end

local RequestMailResourceHandle = function(self,www)
	self:RequestMailResourceHandle(www);
	CS.CommonController.Invoke(Check,0.1,CS.UIManager.Instance);
end

util.hotfix_ex(CS.Mail,'RequestMailResourceHandle',RequestMailResourceHandle)



