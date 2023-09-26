local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

local RefreshItemUI = function(self)
	if self.itemObj == nil or self.itemObj:isNull() then
		return;
	end
	self.itemObj:SetActive(not CS.DeploymentController.isDeplyment);
	local name = self.itemObj.name;
	if name == "2023Se_Buff_Theater(Clone)" or name == "2023Se_Buff_Arms(Clone)" or name == "2023Se_Buff_PA(Clone)" then
		local itemid = self.config.showItemIds[0];
		local itemnum = CS.GameData.GetItem(itemid);
		local child = self.itemObj.transform;
		for i=0,4 do
			child:GetChild(i).gameObject:SetActive(false);
		end
		if itemnum >= 8 then
			child:GetChild(4).gameObject:SetActive(true);
		elseif itemnum>=6 then
			child:GetChild(3).gameObject:SetActive(true);
		elseif itemnum>=4 then
			child:GetChild(2).gameObject:SetActive(true);
		elseif itemnum>=2 then
			child:GetChild(1).gameObject:SetActive(true);
		else
			child:GetChild(0).gameObject:SetActive(true);
		end
		local txtNum = child:Find("Tex_Num"):GetComponent(typeof(CS.ExText));
		txtNum.text =tostring(itemnum);
		local btnInfo = child:Find("TipsButton").gameObject:GetComponent(typeof(CS.ExButton));
		local url = child:Find("TipsButton/URL"):GetComponent(typeof(CS.ExText)).text;
		btnInfo.onClick:RemoveAllListeners();
		btnInfo:AddOnClick(function()
				CS.OPSWebWindows.Show(url);
			end);
	elseif name == "2023Se_All(Clone)" then
		for i=0,self.config.showItemIds.Count-1 do
			local itemid = self.config.showItemIds[i];
			local num = CS.GameData.GetItem(itemid);
			local child = self.itemObj.transform:GetChild(0):GetChild(i);
			for j=0,4 do
				child:GetChild(j).gameObject:SetActive(false);
			end
			if num >= 8 then
				child:GetChild(4).gameObject:SetActive(true);
			elseif num>=6 then
				child:GetChild(3).gameObject:SetActive(true);
			elseif num>=4 then
				child:GetChild(2).gameObject:SetActive(true);
			elseif num>=2 then
				child:GetChild(1).gameObject:SetActive(true);
			else
				child:GetChild(0).gameObject:SetActive(true);
			end
			local txtNum = child:Find("Tex_Num"):GetComponent(typeof(CS.ExText));
			txtNum.text =tostring(num);
			local btnInfo = child:Find("TipsButton").gameObject:GetComponent(typeof(CS.ExButton));
			local url = child:Find("TipsButton/URL"):GetComponent(typeof(CS.ExText)).text;
			btnInfo.onClick:RemoveAllListeners();
			btnInfo:AddOnClick(function()
					CS.OPSWebWindows.Show(url);
				end);
		end
	else
		self:RefreshItemUI();
	end
end

local OnClickAutoBattleConfirm = function(self)
	if CS.DeploymentController.isDeplyment then
		if not CS.DeploymentAutoBattleController.CheckTeamLimit() then
			if CS.DeploymentAutoBattleController.isDailyMissionInfo(CS.DailyMapHexType.Squad) then
				if CS.DeploymentController.Instance.SquadTeamsCount == 0 then
					CS.CommonController.MessageBox(CS.Data.GetLang(30556));
					self:OnClickStopAutoBattle();
					return;
				end
			elseif CS.DeploymentAutoBattleController.isDailyMissionInfo(CS.DailyMapHexType.Vehicle) then
				if CS.DeploymentController.Instance.VehicleTeamCount == 0 then
					CS.CommonController.MessageBox(CS.Data.GetLang(30556));
					self:OnClickStopAutoBattle();
					return;
				end		
			end			
		end
	end
	self:OnClickAutoBattleConfirm();
end

local CheckAllSpotTypeNum = function(missionwintypeid,logic,process,showTarget,medal,checkWin)
	local logicResult = true;
	local txt = Split(logic,",");
	process = "";
	for j=1,#txt do
		local count = 0;
		local mtxt = txt[j];
		local temp = Split(mtxt,":");
		local typeid = tonumber(temp[1]);
		local num = tonumber(temp[2]);
		local type = CS.DeploymentExplainItem.CheckSpotType(typeid);
		for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
			local spot = CS.DeploymentBackgroundController.Instance.listSpot[i];
			if spot.type == type and spot.belong == CS.Belong.friendly then
				count = count+1;
			end
		end
		local result = count >= num;
		process = process..tostring(count).."/"..tostring(num).." ";
		if showTarget then			
			for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
				local spot = CS.DeploymentBackgroundController.Instance.listSpot[i];
				if spot.type == type then
					if not result then
						if spot.belong ~= CS.Belong.friendly then
							spot:ShowWinTarget(missionwintypeid,false,medal,checkWin);
						end
					else
						spot:CloseWinTarget(missionwintypeid);
					end
				end
			end
		end	
		logicResult = logicResult and result;	
	end
	return logicResult,process;
end

function Split(szFullString, szSeparator)
	local nFindStartIndex = 1
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end
util.hotfix_ex(CS.DeploymentUIController,'RefreshItemUI',RefreshItemUI)
util.hotfix_ex(CS.DeploymentUIController,'OnClickAutoBattleConfirm',OnClickAutoBattleConfirm)
util.hotfix_ex(CS.DeploymentUIController,'CheckAllSpotTypeNum',CheckAllSpotTypeNum)
