local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterMissiontSettlementController)
local myInitData = function(self,result)
	self.scoreText.isOrnamental = false;
    self:InitData(result);
end
util.hotfix_ex(CS.TheaterMissiontSettlementController,'InitData',myInitData)