local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.SpecialMissionInfoController)
local CheckSpineMove = function(self)
	self:CheckSpineMove();
	if self.moveSpots.Count == 0 then
		self:CheckDiskMission();
	end
end

local Start = function(self)
	self:Start();
	CS.ImageBufferBlurRefraction.depthonlyCamain.cullingMask = 1 << 18;
end

function hasSameMission(info)
	local order = 0;
	if info.index < 0 then
		order = CS.OPSConfig.missionEntranceSelectOrder[info.entranceId];
	else
		order = info.index;
	end
	if order>info.missionids.Count then
		return false;
	end
	local temp = info.missionids[order];
	local missionid = temp[0];
	local hasSame = true;
	for i=1,temp.count-1 do
		if missionid ~= temp[i] then
			hasSame = false;
		end
	end
	return hasSame;
end

local RefreshEntranceUI = function(self)
	self:RefreshEntranceUI();
	if self.entranceId == 0 then
		return;
	end
	local info = CS.OPSConfig.missionEntranceInfos[self.entranceId];
	local active = hasSameMission(info);
	if active then
		self.btnSelectDiffcluty.gameObject:SetActive(false);
	else
		self.btnSelectDiffcluty.gameObject:SetActive(true);
	end
end
util.hotfix_ex(CS.OPSPanelController,'CheckSpineMove',CheckSpineMove)
util.hotfix_ex(CS.OPSPanelController,'Start',Start)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefreshEntranceUI',RefreshEntranceUI)
