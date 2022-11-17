local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessGameController)
xlua.private_accessible(CS.GF.FlightChess.ChessCollectChipViewController)
local myOnPreBattleMainPhase = function(self)
    self:OnPreBattleMainPhase()
	if CS.GF.FlightChess.ChessCollectChipViewController.Instance ~= nil and not CS.GF.FlightChess.ChessCollectChipViewController.Instance:isNull() then
		CS.GF.FlightChess.ChessCollectChipViewController.Instance:Close();	
	end
end
util.hotfix_ex(CS.GF.FlightChess.FlightChessGameController,'OnPreBattleMainPhase',myOnPreBattleMainPhase)