local util = require 'xlua.util'
xlua.private_accessible(CS.FlightChessLobbyGashaRewardPoolController)

local UpdateView = function(self,itemObj,father)
	self:UpdateView(itemObj,father);
	if father.gashaponRewardObjectType ~= CS.FlightChessGashaponRewardObjectType.TitleBar then
		if father.rewardInfo.rewardType == CS.GF.FlightChess.ChessGashaRewardInfo.RewardType.Prize then
			local iconHolder = itemObj.transform:Find("IconHolder");
			iconHolder:DestroyChildren();
			local package = CS.GameData.listPrize:GetDataById(father.rewardInfo.prizeId);
			package:GetIconBuilder(true):SetHideBG(true):SetHideStars(true):Build().transform:SetParent(iconHolder, false);
			
		end
	end
end

util.hotfix_ex(CS.FlightChessLobbyGashaRewardPoolController,'UpdateView',UpdateView)