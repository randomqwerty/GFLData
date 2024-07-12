local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionBase)
xlua.private_accessible(CS.OPSPanelMissionHolder)

local ChectSelect = function(self,oPSPanelMissionBase)
	self:ChectSelect(oPSPanelMissionBase);
	if self.holder == nil  then
		return;
	end
	if self.holder.opsDiskMission == nil then
		return;
	end
	local parent = self.transform.parent.parent.parent:Find("Img_Guide");
	if parent == nil then
		return;
	end
	if oPSPanelMissionBase == nil then
		parent:Find("CombatMission").gameObject:SetActive(false);
		parent:Find("StoryOnly").gameObject:SetActive(false);
	elseif oPSPanelMissionBase == self then
		local show = oPSPanelMissionBase.currentMission.missionInfo.specialType == CS.MapSpecialType.Story;
		parent:Find("CombatMission").gameObject:SetActive(not show);
		parent:Find("StoryOnly").gameObject:SetActive(show);
	end
end
local ChecckCampaion = function()
	if CS.OPSPanelController.Instance.campaionId == -69 then
		return true;
	end
	if CS.OPSPanelController.Instance.campaionId == -70 then
		return true;
	end
	return false;
end
local Awake = function(self)
	self:Awake();
	if ChecckCampaion() then
		self.checkChoose = false;
	end
end
local Start = function(self)
	self:Start();
	if self.opsDiskMission ~= nil then
		self.transform.rotation = CS.UnityEngine.Quaternion.Euler(0, 0, 0);
	end
	if ChecckCampaion() then
		if self.opsDiskMission == nil then
			--print("实例化到Left");
			self.transform:SetParent(CS.OPSPanelController.Instance.leftMain,false);
			local rectTrans = self.transform:GetComponent(typeof(CS.UnityEngine.RectTransform));
			rectTrans.anchorMin = CS.UnityEngine.Vector2(0,0.5);
			rectTrans.anchorMax = CS.UnityEngine.Vector2(0,0.5);
			rectTrans.pivot = CS.UnityEngine.Vector2(0.5,0.5);
			rectTrans.anchoredPosition = CS.UnityEngine.Vector2(120,-340);
			rectTrans.localScale = CS.UnityEngine.Vector3(1.5,1.5,1.5);
		end
	end
end

local CheckCommonUI = function(self)
	self:CheckCommonUI();
	local combat = self.transform:Find("InCombat");
	if combat ~= nil then
		combat.gameObject:SetActive(self.opsMission:isInCombat());
		if self.holder.opsDiskMission ~= nil then
			local control = combat:GetComponent(typeof(CS.ImageRotateControl));
			if control ~= nil then
				control.fatherEffectRotateControl = self.holder.opsDiskMission.oPSDiskConfig.diskRotalControl;
			end
		end
	end
end
local RefreshUI = function(self)
	self:RefreshUI();
	if self.holder ~= nil and self.holder.prefabCode == "2023RougeSpring_BossMissionPanelTitle" then
		if self.currentMission ~= nil then
			local countdownTimer = CS.UnityEngine.PlayerPrefs.GetFloat("2023_Rouge_Time",-1);
			if countdownTimer < 0 then
				return;
			end
			local _textTime = self.transform:Find("Completed/RealTime/Txt_Time"):GetComponent(typeof(CS.ExText));
			local countdownMinute = math.modf(countdownTimer / 60);
			local countdownSec = math.modf(countdownTimer - countdownMinute * 60);
			local countdownRemain = countdownTimer - (countdownMinute * 60) - (countdownSec);
			_textTime.text = string.format("%02d",(countdownMinute))..":"..string.format("%02d",(countdownSec))..":"..string.format("%02d",(math.modf(countdownRemain*100)));
		end
	end
end
util.hotfix_ex(CS.OPSPanelMissionBase,'ChectSelect',ChectSelect)
util.hotfix_ex(CS.OPSPanelMissionHolder,'Awake',Awake)
util.hotfix_ex(CS.OPSPanelMissionHolder,'Start',Start)
util.hotfix_ex(CS.OPSPanelMissionBase,'CheckCommonUI',CheckCommonUI)
util.hotfix_ex(CS.OPSPanelMissionBase,'RefreshUI',RefreshUI)