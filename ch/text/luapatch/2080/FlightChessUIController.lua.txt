local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessUIController)
local gameEndFlag = false
local Init = function(self)
	gameEndFlag = false
	self:Init()
end
local CloseForGameEnd = function(self)
	gameEndFlag = true
	local trans = self.gameObject.transform
	for i=0,trans.childCount -1 do
		trans:GetChild(i).gameObject:SetActive(false)		
	end
	CS.FlightChessCountdownController.Instance.gameObject:SetActive(false)
	if CS.GF.FlightChess.FlightChessGameLeavingScreenController.Instance ~= nil then
		CS.GF.FlightChess.FlightChessGameLeavingScreenController.Instance:Close()
	end
end
local HideBattleUI = function(self)
	if self.BattleUI ~= nil then
		if gameEndFlag then
			self.BattleUI.gameObject:SetActive(false)
		else
			self:HideBattleUI()
		end
	end
end
util.hotfix_ex(CS.GF.FlightChess.FlightChessUIController,'Init',Init)
util.hotfix_ex(CS.GF.FlightChess.FlightChessUIController,'CloseForGameEnd',CloseForGameEnd)
util.hotfix_ex(CS.GF.FlightChess.FlightChessUIController,'HideBattleUI',HideBattleUI)

