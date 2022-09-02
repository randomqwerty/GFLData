local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionOperationBarController)


local RequestFinishOperationHandle = function(self)
	self:RequestFinishOperationHandle();
	self.parentController.teamInfo:Show(self.operationInfo);
end
util.hotfix_ex(CS.MissionSelectionOperationBarController,'RequestFinishOperationHandle',RequestFinishOperationHandle)