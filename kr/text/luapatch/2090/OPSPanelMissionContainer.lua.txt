local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionContainer)

local rotateControl = function(self)
	if self.rotateControl ~= nil then
		return self.rotateControl;
	end
	local ro = self.gameObject:GetComponent(typeof(CS.ImageRotateControl));
	if ro == nil then
		ro = self.gameObject:AddComponent(typeof(CS.ImageRotateControl));
	end
	return ro;
end

local RefreshClockUI = function(self)
	self:RefreshClockUI();
	if CS.OPSPanelController.Instance.campaionId == -51 then
		local triangle = self.transform:Find("DialPlateHolder");
		if 	triangle ~= nil then
			local rotateControl = triangle:GetComponent(typeof(CS.ImageRotateControl));
			local check = 1.0*self:ClearCount() / self:AllCount();
			--print(self.id.."/"..check);
			local angle = CS.Mathf.Lerp(0, 180, check);
			--rotateControl.angle = angle;
			if rotateControl.angle ~= angle then
				CS.DG.Tweening.DOTween.To(
					function ()
						return rotateControl.angle;
					end,
					function (v)
						rotateControl.angle = v;
					end,
					angle,1):SetDelay(0.5);
			end
		end
	end
end

local ClearCount = function(self)
	if self.clockinfo ~= nil then
		local num = 0;
		for i=0,self.clockinfo.missionIds.Count-1 do
			local mids = self.clockinfo.missionIds[i];
			local pass = false;
			for j=0,mids.Count-1 do
				local missionid = mids[j];
				local mission = CS.GameData.listMission:GetDataById(missionid);
				if mission ~= nil and mission.winCount>0 then
					pass = true;
				end
			end
			if pass then
				num = num + 1;
			end
		end
		return  num;
	end	
	return 0;	
end
local AllCount = function(self)
	if self.clockinfo ~= nil then
		local num = self.clockinfo.missionIds.Count;
		return num;
	end	
	return 0;
end
util.hotfix_ex(CS.OPSPanelMissionContainer,'get_rotateControl',rotateControl)
util.hotfix_ex(CS.OPSPanelMissionContainer,'RefreshClockUI',RefreshClockUI)
util.hotfix_ex(CS.OPSPanelMissionContainer,'ClearCount',ClearCount)
util.hotfix_ex(CS.OPSPanelMissionContainer,'AllCount',AllCount)