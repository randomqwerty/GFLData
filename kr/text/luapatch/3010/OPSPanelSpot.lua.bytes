local util = require 'xlua.util'
local panelController = require("3010/OPSPanelController")
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.OPSPanelSpot)

local CanShow = function(self)
	if CS.OPSPanelController.Instance.campaionId == -57 then
		if CS.OPSPanelController.Instance.currentPanelConfig.spotShowInfos:ContainsKey(self.id) then
			local onMissionaction = false;
			local newTag = false;
			local show = false;
			local info = CS.OPSPanelController.Instance.currentPanelConfig.spotShowInfos[self.id];
			local missionid = 0;
			for i=0,info.missionids.Count -1 do
				missionid = info.missionids[i][CS.OPSPanelController.difficulty];				
				local mission = CS.GameData.listMission:GetDataById(missionid);	
				if mission ~= nil then
					if endMissionIds:Contains(missionid) and CurrentType() == 4 then
						if currentSetType == 4 or currentSetType == 3 then
							show = true;
							if mission.winCount == 0 then
								newTag = true;
							end
							if CS.GameData.missionAction ~= nil and CS.GameData.missionAction.mission == mission then
								onMissionaction = true;
							end
						end
					elseif CheckAllMissionIdSpotShow(missionid) then
						show = true;
						if mission.winCount == 0 then
							newTag = true;
						end
						if CS.GameData.missionAction ~= nil and CS.GameData.missionAction.mission == mission then
							onMissionaction = true;
						end
					end
				end
			end
			if show then
				--print("显示spot"..self.id);
				self.transform:Find("PanelLayout/SpotPanel/Img_New").gameObject:SetActive(newTag);
				self.transform:Find("PanelLayout/SpotPanel/Img_InProgress").gameObject:SetActive(onMissionaction);
				local btnavg = self.transform:Find("PanelLayout/MissionList/Mission/Btn_PlayStory"):GetComponent(typeof(CS.ExButton));
				local info = GetAvgInfo(missionid);
				if info ~= nil then
					btnavg.gameObject:SetActive(true);
					btnavg.onClick:RemoveAllListeners();
					btnavg:AddOnClick(function()
						ShowAvg(info[2]);
					end)
				else
					btnavg.gameObject:SetActive(false);
				end
			end
			return show;
		end
		return false;
		--local uilist = self.transform:Find("MissionSpotMissionList_2021(Clone)/MissionSpotMissionList/MissionLayout")
		--if uilist == nil then
			--return false;
		--end
		--uilist.transform.localRotation = CS.UnityEngine.Quaternion.Euler(CS.UnityEngine.Vector3(-60,0,0));
		--for i=0,uilist.childCount-1 do
			--local item = uilist:GetChild(i):GetComponent(typeof(CS.CommonListHolder));
			--if item ~= nil then
				--if item.info.mission ~= nil and CheckMissionIdShow(item.info.mission:GetID()) then
					--item.gameObject:SetActive(true);
					--finalshow = true;
				--else
					--item.gameObject:SetActive(false);
				--end
			--end
		--end
		--if finalshow then
			--print("显示spot"..self.id);
		--end
		--return finalshow;
	end
	return self.CanShow;
end

local Init = function(self)
	self:Init();
	self.transform.localRotation = CS.UnityEngine.Quaternion.Euler(CS.OPSPanelBackGround.Instance.spotAngle);
	if CS.OPSPanelController.Instance.campaionId == -57 then
		local btnTouch = self.transform:Find("Btn_TouchArea"):GetComponent(typeof(CS.ExButton));
		btnTouch:AddOnClick(function()
			CS.OPSPanelController.Instance:SelectMissionSpot(self);
		end)
	end
end
util.hotfix_ex(CS.OPSPanelSpot,'get_CanShow',CanShow)
util.hotfix_ex(CS.OPSPanelSpot,'Init',Init)
