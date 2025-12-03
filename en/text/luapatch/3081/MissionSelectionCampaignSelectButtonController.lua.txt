local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionCampaignSelectButtonController)
xlua.private_accessible(CS.MissionSelectionIntroduceController)

xlua.private_accessible(CS.MissionSelectionMissionBarController)
xlua.private_accessible(CS.MissionSelectionMissionDetailController)
xlua.private_accessible(CS.MissionSelectionController)

local mPlayUITweens = function(self)
	if self.goOperationMisson.gameObject.activeSelf==true then
			self.listCampaignBar[14].gameObject:SetActive(false);
		else
			self.listCampaignBar[14].gameObject:SetActive(true);
		end
	self:PlayUITweens()	
end
local mInit = function(self,...)
	--local jsondata = select(1, ...);
	self:Init(...)
	if self.campaignId==14 then
		self.textNum1.text ="A"
		self.textNum2.text ="A"

		self.textChinese1.text = CS.Data.GetLang(14)..CS.Data.GetLang(1229)
		self.textChinese2.text = CS.Data.GetLang(14)..CS.Data.GetLang(1229)
	end
end
local mUpdateInfo = function(self,missionSelectionController)
	self:UpdateInfo(missionSelectionController)
	if CS.MissionSelectionController.currentSelectedCampaignId==14 then
		self.txChapterNum.text ="A"

		self.txChapterName.text = CS.Data.GetLang(14)..CS.Data.GetLang(1229)
	end
end
local mShowDrawEventIcon = function(self)
	self:ShowDrawEventIcon()
	if self.mission~=nil and self.mission.missionInfo.campaign ==14 then
		self.textCode.text ="A-"..self.mission.missionInfo.sub
	end
end
local mRequestMissionCombinationHandle = function(self,data)
	self:RequestMissionCombinationHandle(data)
	 
	if self.mission~=nil and self.mission.missionInfo.campaign ==14 and self._goMissionBar ~=nil  then
		local itemCS = self._goMissionBar.transform:GetComponent(typeof(CS.MissionSelectionMissionBarController));
		itemCS.textCode.text ="A-"..self.mission.missionInfo.sub
	end
end
util.hotfix_ex(CS.MissionSelectionController,'PlayUITweens',mPlayUITweens)
util.hotfix_ex(CS.MissionSelectionCampaignSelectButtonController,'Init',mInit)
util.hotfix_ex(CS.MissionSelectionIntroduceController,'UpdateInfo',mUpdateInfo)
util.hotfix_ex(CS.MissionSelectionMissionBarController,'ShowDrawEventIcon',mShowDrawEventIcon)
util.hotfix_ex(CS.MissionSelectionMissionDetailController,'RequestMissionCombinationHandle',mRequestMissionCombinationHandle)