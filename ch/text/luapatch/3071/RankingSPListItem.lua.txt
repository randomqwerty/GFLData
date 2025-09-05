local util = require 'xlua.util'
xlua.private_accessible(CS.RankingSPListItem)

local ShowFlightChessUserCardInfo = function(self)
	if self.chessRankData == nil then
		return;
	end
	if CS.ApplicationConfigData.IsCrossServer() then
		CS.CommonAudioController.PlayUI(CS.AudioUI.UI_selete);
		CS.GF.FlightChess.FlightChessTopRankingListController.Instance:ShowUserCard(self.chessRankData.user_id,self.chessRankData.server_id);
	else
		self:ShowFlightChessUserCardInfo();
	end
end
util.hotfix_ex(CS.RankingSPListItem,'ShowFlightChessUserCardInfo',ShowFlightChessUserCardInfo)