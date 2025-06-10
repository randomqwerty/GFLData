local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local Start = function(self)
	self:Start();
	if CS.CommonVideoPlayer.Instance ~= nil and not CS.CommonVideoPlayer.Instance:isNull() then
		if not CS.CommonVideoPlayer.Instance.gameObject.activeInHierarchy then
			CS.UnityEngine.Object.DestroyImmediate(CS.CommonVideoPlayer.Instance.gameObject);
			CS.OPSConfig.CheckVideo = false;
		end
	end		
end

local ShowItemLimitUINew = function(self,itemids)
	self:ShowItemLimitUINew(itemids);
	if self.itemuiObjNew ~= nil and not self.itemuiObjNew:isNull() then
		local itemabout = self.item_use:GetDataById(itemids[0]);
		local showTipObj =self.itemuiObjNew.transform:Find("TouchArea");
		if showTipObj ~= nil then
			local tip = showTipObj:GetComponent(typeof(CS.CommonShowTip));
			tip.strTitle = itemabout.iteminfo.name;
		end
	end
end
spotshowinfo = {};
local Load = function(self,campaion)
	self:Load(campaion);
	local textAsset = CS.ResManager.GetObjectByPath("ProfilesConfig/OPSPanel/Campion"..tostring(campaion), ".txt");
	if textAsset == nil then
		return;
	end
	spotshowinfo = {};
	local lineTxt = Split(textAsset.text,"\n");
	for i = 1, #lineTxt do
		local index = string.find(lineTxt[i],"SpotSelectShow");
		if index ~= nil then
			local temp = Split(lineTxt[i],"|");
			if temp[1] == "SpotSelectShow" then
				local info = {};
				info[1] = tonumber(temp[2]);
				info[2] = temp[3];
				table.insert(spotshowinfo,info);
			end			
		end
	end
end	

local TriggerSelectOPSMissionBase = function(self,missionBase)
	self:TriggerSelectOPSMissionBase(missionBase);
	for i=1,#spotshowinfo do
		local index = spotshowinfo[i][1];
		local path = spotshowinfo[i][2];	
		local trans = self.transform.parent:Find(path);
		if trans == nil then
			CS.NDebug.LogError("未找到组件",path);
		else			
			if missionBase ~= nil and missionBase.order == index then
				--CS.NDebug.Log("激活",trans);
				trans.gameObject:SetActive(true);
			else
				--CS.NDebug.Log("隐藏",trans);
				trans.gameObject:SetActive(false);
			end
		end
	end
end

local TriggerSelectOPSSpot = function(self,oPSPanelSpot)
	self:TriggerSelectOPSSpot(oPSPanelSpot);
	for i=1,#spotshowinfo do
		local index = spotshowinfo[i][1];
		local path = spotshowinfo[i][2];
		local trans = self.transform.parent:Find(path);
		if trans == nil then
			CS.NDebug.LogError("未找到组件",path);
		else
			if oPSPanelSpot ~= nil and oPSPanelSpot.missionHolderOrder == index then
				--CS.NDebug.Log("激活",trans);
				trans.gameObject:SetActive(true);
			else
				--CS.NDebug.Log("隐藏",trans);
				trans.gameObject:SetActive(false);
			end
		end
	end
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

util.hotfix_ex(CS.OPSPanelController,'Start',Start)
util.hotfix_ex(CS.OPSPanelController,'ShowItemLimitUINew',ShowItemLimitUINew)
util.hotfix_ex(CS.OPSPanelController,'Load',Load)
util.hotfix_ex(CS.OPSPanelController,'TriggerSelectOPSSpot',TriggerSelectOPSSpot)
util.hotfix_ex(CS.OPSPanelController,'TriggerSelectOPSMissionBase',TriggerSelectOPSMissionBase)

