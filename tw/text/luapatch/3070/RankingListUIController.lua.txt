local util = require 'xlua.util'
xlua.private_accessible(CS.RankingListUIController)

local OpenRankingReward = function(self)
	self:OpenRankingReward();
	self.WebWindow.transform:Find("ImageBlock"):SetAsFirstSibling();
	self.WebWindow.transform:Find("Background"):SetAsFirstSibling();
end

util.hotfix_ex(CS.RankingListUIController,'OpenRankingReward',OpenRankingReward)
