local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionMissionDetailController)

local mOnClickCancel = function(self)
	self.raidNormalStartCallBack=nil
	self.raidStartCallBack=nil
	self:OnClickCancel()
end


util.hotfix_ex(CS.MissionSelectionMissionDetailController,'OnClickCancel',mOnClickCancel)