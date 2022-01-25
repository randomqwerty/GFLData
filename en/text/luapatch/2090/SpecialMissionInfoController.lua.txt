local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialMissionInfoController)

local InitTotalTeamBaseLimit = function(self)
	self:InitTotalTeamBaseLimit();
	local imag_OK = self.PlanDetail.transform:Find("PlanNode/PlanItemTeam/Img_OK");
	if self.missionInfo.totalTeamLimitBase <= 0 then
		imag_OK.gameObject:SetActive(true);
	else
		imag_OK.gameObject:SetActive(false);
	end
end

local ShowNewReward = function(self)
	self:ShowNewReward();
	local parent = self.RewardBg:Find("IconScrollView/Rect");
	for i=0,parent.childCount-1 do
		local child = parent:GetChild(i);
		if i == 2 then
			local get = child:Find("GetIcon").gameObject.activeSelf;
			local image = child:Find("DiffcultyOnly"):GetComponent(typeof(CS.ExImage));
			image.gameObject:SetActive(true);
			image.enabled = get;			
			child:Find("DiffcultyOnly/Img_Diffculty1").gameObject:SetActive(true);
			child:Find("DiffcultyOnly/Img_Diffculty2").gameObject:SetActive(false);
			local image1 = child:Find("DiffcultyOnly/Img_Diffculty1"):GetComponent(typeof(CS.ExImage));
			image1.color = CS.UnityEngine.Color(212/255, 118/255, 0, 1);
		elseif i == 3 then
			local get = child:Find("GetIcon").gameObject.activeSelf;
			local image = child:Find("DiffcultyOnly"):GetComponent(typeof(CS.ExImage));
			image.gameObject:SetActive(true);
			image.enabled = get;
			child:Find("DiffcultyOnly/Img_Diffculty1").gameObject:SetActive(false);
			child:Find("DiffcultyOnly/Img_Diffculty2").gameObject:SetActive(true);
			local image1 = child:Find("DiffcultyOnly/Img_Diffculty2"):GetComponent(typeof(CS.ExImage));
			image1.color = CS.UnityEngine.Color(1, 16/255, 11/255, 1);		
		end
	end
end

local RefresCommonUI = function(self)
	self.theaterTransform:Find("FightType").gameObject:SetActive(false);
	self:RefresCommonUI();
end
util.hotfix_ex(CS.SpecialMissionInfoController,'InitTotalTeamBaseLimit',InitTotalTeamBaseLimit)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowNewReward',ShowNewReward)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefresCommonUI',RefresCommonUI)