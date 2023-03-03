local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterMissiontSettlementController)

local InitData = function(self,result)
	self:InitData(result);
	self.scoreText.gameObject:SetActive(true);
end


util.hotfix_ex(CS.TheaterMissiontSettlementController,'InitData',InitData)