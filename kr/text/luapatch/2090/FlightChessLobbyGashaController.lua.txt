local util = require 'xlua.util'
xlua.private_accessible(CS.FlightChessLobbyGashaController)
xlua.private_accessible(CS.GF.FlightChess.FlightChessLobbyMainController)

local ShowGashaEffect_New = function(self, gold)
	self:ShowGashaEffect(gold)
	CS.GF.FlightChess.FlightChessLobbyMainController.Instance:RefreshUI()
end

util.hotfix_ex(CS.FlightChessLobbyGashaController,'ShowGashaEffect',ShowGashaEffect_New)
