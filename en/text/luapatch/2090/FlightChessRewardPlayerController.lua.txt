local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessRewardPlayerController)

local _ShowUserCard = function(self)
	if self.isAI == false and self.cansShowCard == true then
		self:ShowUserCard();
	else 
		CS.CommonController.LightMessageTips(CS.Data.GetLang(280426));
	end
end

util.hotfix_ex(CS.GF.FlightChess.FlightChessRewardPlayerController,'ShowUserCard',_ShowUserCard)