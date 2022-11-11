local util = require 'xlua.util'
xlua.private_accessible(CS.FlightChessGameController)
xlua.private_accessible(CS.ChessCollectChipViewController)
local myOnPreBattleMainPhase = function(self)
    self:OnPreBattleMainPhase()
	if CS.ChessCollectChipViewController.Instance ~= nil and not CS.ChessCollectChipViewController.Instance:isNull() then
		CS.ChessCollectChipViewController.Instance:Close();	
	end
end
util.hotfix_ex(CS.FlightChessGameController,'OnPreBattleMainPhase',myOnPreBattleMainPhase)