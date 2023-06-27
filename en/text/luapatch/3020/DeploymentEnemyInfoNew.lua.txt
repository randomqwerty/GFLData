local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyInfoNew)

local ShowBuildInfo = function(self,spot)
	for i=0,self.buildSpots.Count-1 do
		if self.buildSpots[i] ~= nil then
			if self.buildSpots[i].spot ~= nil then
				self.buildSpots[i].spot:CloseBuildRangeTip();
			end
		end
	end
	self:ShowBuildInfo(spot);
end
local ShowFriendTeamGun = function(self,friend)
	self.image_LogoMyteam.gameObject:SetActive(true);
	self.txt_Logo.text = CS.Data.GetLang(1336);
	self.AITypeTrans.gameObject:SetActive(true);
	self.txt_AIType.text = friend.CurrentTeamAI.Name;
	self.currentTeamAI = friend.CurrentTeamAI;
	self.image_AITypeIcon.sprite = CS.CommonController.LoadPngCreateSprite("Pics/Icons/AI/"..friend.CurrentTeamAI.pic);
	self.BattleTypeTrans.gameObject:SetActive(false);
	self.btn_CollectionAdd.gameObject:SetActive(false);
	self.btn_CollectionCancel.gameObject:SetActive(false);
	self.btn_ShowBattle.gameObject:SetActive(false);
	self.image_BattleTip.gameObject:SetActive(false);
	self.recommendedTip.gameObject:SetActive(false);
	if friend.sangvisTeam ~= nil then
		self:ShowSelfGuns(friend.sangvisTeam.listGun,CS.UnityEngine.Color32(179,208,37,255));
	else
		self:ShowSelfGuns(friend.useGuns.listGun,CS.UnityEngine.Color32(179,208,37,255));
	end
end
util.hotfix_ex(CS.DeploymentEnemyInfoNew,'ShowBuildInfo',ShowBuildInfo)
util.hotfix_ex(CS.DeploymentEnemyInfoNew,'ShowFriendTeamGun',ShowFriendTeamGun)