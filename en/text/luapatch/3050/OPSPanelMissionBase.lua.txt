local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionBase)
xlua.private_accessible(CS.OPSPanelMissionHolder)

local ChectSelect = function(self,oPSPanelMissionBase)
	self:ChectSelect(oPSPanelMissionBase);
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

local Awake = function(self)
	self:Awake();
	if CS.OPSPanelController.Instance.campaionId == -69 then
		self.checkChoose = false;
	end
end
util.hotfix_ex(CS.OPSPanelMissionBase,'ChectSelect',ChectSelect)
util.hotfix_ex(CS.OPSPanelMissionHolder,'Awake',Awake)