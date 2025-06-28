local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.Data)

local CheckCarnivalAndBingoBadge = function(self)
	local exitcurrentBingo = CS.Data.GetCurrentBingo() ~= nil;
	if exitcurrentBingo then
		local bingoMail = CS.Data.CheckMailTypeExists(CS.MailType.bingo);
		local bingoTaskMail = CS.Data.ExistsNewBingoTaskRewards();
		if bingoMail or bingoTaskMail then
			return true;
		end
	end
	local exitcurrentCarnival = CS.Data.GetCurrentCarnival() ~= nil;
	if exitcurrentCarnival then
		local carnivalPrizeMail = CS.Data.ExistsNewCarnivalPrizeRewards();
		local carnivalTaskMail = CS.Data.ExistsNewCarnivalTaskRewards();
		if carnivalPrizeMail or carnivalTaskMail then
			return true;
		end
	end
	return false;
end

local Start = function(self)
	self:Start();
	self.transform:Find("BonuseEffectSingle").localScale = CS.UnityEngine.Vector3.one;
	self.transform:Find("BonuseEffectTen").localScale = CS.UnityEngine.Vector3.one;
end
util.hotfix_ex(CS.HomeController,'CheckCarnivalAndBingoBadge',CheckCarnivalAndBingoBadge)
util.hotfix_ex(CS.FlightChessLobbyGashaBonusAnimController,'Start',Start)
