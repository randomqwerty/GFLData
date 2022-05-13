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
	if self.entranceId ~= 0 then
		local missionid = self.missionInfo.Id;
		local info = CS.OPSConfig.missionEntranceInfos[self.entranceId];
		self.btnSelectDiffcluty.gameObject:SetActive(false);
		for i=0,info.missionids.Count-1 do
			if info.missionids[i]:Contains(missionid) then
				local check = 0;
				for j=0,info.missionids[i].Count-1 do
					if info.missionids[i][j] == missionid then
						check = check+1;
					end
				end
				if check == 1 then
					self.btnSelectDiffcluty.gameObject:SetActive(true);
				end
			end
		end
	end
	self:RefresCommonUI();
end
local RequestStartMissionHandle = function(self,www)
	self:RequestStartMissionHandle(www);
	if CS.OPSPanelController.Instance~=nil	and	not	CS.OPSPanelController.Instance:isNull() then
		local request=CS.RequestDrawEvent(CS.OPSPanelController.OpenCompaions);
		request:Request();
	end
end
local	InitUIElements=function(self)
	self:InitUIElements();
	local	txtUI=self.transform:Find("Groove/MultiMission/Tex_Info");
	local	txt=txtUI:GetComponent(typeof(CS.ExText));
	txt.text=CS.Data.GetLang(60097);
end
util.hotfix_ex(CS.SpecialMissionInfoController,'InitTotalTeamBaseLimit',InitTotalTeamBaseLimit)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowNewReward',ShowNewReward)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefresCommonUI',RefresCommonUI)
util.hotfix_ex(CS.SpecialMissionInfoController,'RequestStartMissionHandle',RequestStartMissionHandle)
util.hotfix_ex(CS.SpecialMissionInfoController,'InitUIElements',InitUIElements)