local util = require 'xlua.util'
xlua.private_accessible(CS.ObtainController)


local mShowMissionDetail = function(self)
	if self.obtain ~= nil and self.obtain.obtainInfo.id ==3 and self.obtain.listMission ~= nil and  self.obtain.listMission.Count == 0 then
		CS.CommonObtainMessageBoxController.Instance:Init(self.obtain);
	else
		self:ShowMissionDetail()
	end
end
util.hotfix_ex(CS.ObtainController,'ShowMissionDetail',mShowMissionDetail)