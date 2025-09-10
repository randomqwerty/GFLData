local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessUserCardController)
local Init = function(self)
	self:Init()
	if not CS.Data.unlockApplyFriend then
		self.btnAddFriend.gameObject:SetActive(false)
	end
end
util.hotfix_ex(CS.GF.FlightChess.FlightChessUserCardController,'Init',Init)