local util = require 'xlua.util'
xlua.private_accessible(CS.DailyGameAutoPlanController)

local CheckAutoPlanInDailyGame = function()
	CS.DailyGameAutoPlanController.CheckAutoPlanInDailyGame();
	CS.RewardBoxController.boxes:Clear();
end

local MissionState = function(finishHexCount)
	local count = finishHexCount -1;
	return CS.DailyGameAutoPlanController.MissionState(count);
end

local GoToDeployment = function(hexData)
	if not hexData:isMeetSelect() then
		CS.DailyGameAutoPlanController.RequestPlanFinish();
		return;
	end
	CS.DailyGameAutoPlanController.GoToDeployment(hexData);
end

local CheckShowSelectAllHex = function()
	CS.DailyGameAutoPlanController.AutoSelectAllHex();
	if CS.DailyGameAutoPlanController.onlyuseticket then
		local canSelectCount = 0;
		for i=0,CS.DailyExploreGameManager.Instance.mapController.listHex.Count-1 do
			local hex = CS.DailyExploreGameManager.Instance.mapController.listHex[i];
			if hex.hexData:isMeetSelect() then
				canSelectCount = canSelectCount + 1;
			end
		end
		if canSelectCount > CS.DailyGameAutoPlanController.selectPlanhexs.Count then
			CS.CommonController.ConfirmBox(CS.Data.GetLang(280550),function()
					CS.DailyGameAutoPlanController.onlyuseticket = false;
					CS.DailyGameAutoPlanController.AutoSelectAllHex();
			end)
		end
	end
end
util.hotfix_ex(CS.DailyGameAutoPlanController,'MissionState',MissionState)
util.hotfix_ex(CS.DailyGameAutoPlanController,'CheckAutoPlanInDailyGame',CheckAutoPlanInDailyGame)
util.hotfix_ex(CS.DailyGameAutoPlanController,'GoToDeployment',GoToDeployment)
util.hotfix_ex(CS.DailyGameAutoPlanController,'CheckShowSelectAllHex',CheckShowSelectAllHex)
