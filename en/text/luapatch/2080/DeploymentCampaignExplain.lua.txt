local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentCampaignExplain)

local ShowOldMedal = function(self)
	self:ShowOldMedal();	 
	local num = CS.GameData.currentSelectedMissionInfo.expectedFriendlyDieNumber;
	if num >0 then
		local textSCondition = self.newMedal.transform:Find("condition"):GetComponent(typeof(CS.ExText));		
		textSCondition.text = CS.System.String.Format(CS.Data.GetLang(30465), tostring(num));
	end
end

local InitShowGoldTarget = function(self)
	self:InitShowGoldTarget();
	if CS.GameData.currentSelectedMissionInfo.hostageTotalNum > 0  then
		self.itemsGold[2].winTypeInfo.type = 1404;
		self.itemsGold[2].winTypeInfo.arguments = CS.GameData.currentSelectedMissionInfo.hostageTotalNum;
	end
end
util.hotfix_ex(CS.DeploymentCampaignExplain,'ShowOldMedal',ShowOldMedal)
util.hotfix_ex(CS.DeploymentCampaignExplain,'InitShowGoldTarget',InitShowGoldTarget)


