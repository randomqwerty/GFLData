local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionHolder)

local AllCount = function(self)
	if self.groupInfo ~= nil then
		return  self.groupInfo.missionids.Count;
	end
	if self.opsMission ~= nil then
		return  self.opsMission:AllCount();
	end
	return 0;
end

local Awake = function(self)
	self:Awake();
	self.xPos = CS.UnityEngine.Vector2(300,-300);
end

local CanShow = function(self)
	if self.prefabCode == "2023RougeSpring_BossMissionPanelTitle" then
		return true;
	end
	return self.CanShow;
end

local PlayLabel = function(self)
	self:PlayLabel();
	if self.prefabCode == "2023RougeSpring_BossMissionPanelTitle" then
		self.currentLabel.transform:Find("GQ_bl_rongjie").gameObject:SetActive(true);
	end
end

local RefreshUI = function(self)
	if CS.OPSPanelBackGround.currentContainerId == self.containerId and self.CanShow then
		if self.groupInfo ~= nil then
			self.gameObject:SetActive(true);
			if self.currentLabel ~= nil then
				self.currentLabel:PlayShow();
			end
			return;
		end
	end
	self:RefreshUI();
end
util.hotfix_ex(CS.OPSPanelMissionHolder,'Awake',Awake)
util.hotfix_ex(CS.OPSPanelMissionHolder,'AllCount',AllCount)
util.hotfix_ex(CS.OPSPanelMissionHolder,'get_CanShow',CanShow)
util.hotfix_ex(CS.OPSPanelMissionHolder,'PlayLabel',PlayLabel)
util.hotfix_ex(CS.OPSPanelMissionHolder,'RefreshUI',RefreshUI)




