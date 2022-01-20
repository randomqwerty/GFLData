local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentCampaignExplain)

local CheckNightText = function(self,textSCondition)
	local txt;
	if CS.GameData.currentSelectedMissionInfo.expectedFriendlyDieNumber == 0 then		
		txt = CS.Data.GetLang(30488);
	else
		txt = CS.System.String.Format(CS.Data.GetLang(30489), CS.GameData.currentSelectedMissionInfo.expectedFriendlyDieNumber);
	end
	if CS.GameData.currentSelectedMissionInfo.expectedTurn ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30490), CS.GameData.currentSelectedMissionInfo.expectedTurn);
	end
	if CS.GameData.currentSelectedMissionInfo.expectedEnemyDieNumber ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30491), CS.GameData.currentSelectedMissionInfo.expectedEnemyDieNumber);
	end
	if CS.GameData.currentSelectedMissionInfo.hostageTotalNum ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30492), CS.GameData.currentSelectedMissionInfo.hostageTotalNum);
	end
	if CS.GameData.currentSelectedMissionInfo.expectLineTurn ~= 0 then
		txt = txt.."\n"..CS.System.String.Format(CS.Data.GetLang(30493), CS.GameData.currentSelectedMissionInfo.expectLineTurn);
	end
	textSCondition.text = txt;
end


util.hotfix_ex(CS.DeploymentCampaignExplain,'CheckNightText',CheckNightText)



