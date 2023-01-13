local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionBase)

local RefreshUI = function(self)
	if self.holder.prefabCode == "2023RougeSpring_BossMissionPanelTitle" then
		local missionNameText = self.transform:Find("Uper/Txt_MissionName"):GetComponent(typeof(CS.ExText)); 
		missionNameText.text = self.currentMissionInfo.name;
		if self.currentMission == nil then
			self.transform:Find("Locked").gameObject:SetActive(true);
			self.transform:Find("Unlocked").gameObject:SetActive(false);
		else
			self.transform:Find("Locked").gameObject:SetActive(false);
			local time = CS.UnityEngine.PlayerPrefs.GetFloat("2023_Rouge_Time",0);
			local second = CS.Mathf.FloorToInt(time);
			if second == 0 then
				self.transform:Find("Unlocked").gameObject:SetActive(true);			
			else
				self.transform:Find("Unlocked").gameObject:SetActive(false);
				self.transform:Find("Completed").gameObject:SetActive(true);
				local timetext = self.transform:Find("Completed/RealTime/Txt_Time"):GetComponent(typeof(CS.ExText));
				timetext.text = CS.GameData.FormatLongToTimeStr2(second);
			end
		end
		return;
	end
	self:RefreshUI();
end

local InitData = function(self,data)
	self:InitData(data);
	if self.holder.prefabCode == "2023RougeSpring_BossMissionPanelTitle" then
		local btn = self.transform:GetComponent(typeof(CS.ExButton));
		btn.onClick:RemoveAllListeners();
		btn:AddOnClick(function()
			if CS.OPSPanelBackGround.Instance.isDrag then
				return;	
			end
			if self.currentMission ~= nil then	
				CS.OPSPanelController.Instance:SelectMissionPanel(self);
			end
			end);
	end
end
util.hotfix_ex(CS.OPSPanelMissionBase,'RefreshUI',RefreshUI)
util.hotfix_ex(CS.OPSPanelMissionBase,'InitData',InitData)




