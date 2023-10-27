local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialMissionInfoController)


local UpdateAutoMissionTimer = function(self)
	if self.mission == nil then
		self.nodeDownBtn:SetActive(true);
		self.nodeAutoActivity:SetActive(false);
		return;
	end
	self:UpdateAutoMissionTimer();
end

util.hotfix_ex(CS.SpecialMissionInfoController,'UpdateAutoMissionTimer',UpdateAutoMissionTimer)
