local util = require 'xlua.util'

local nightView = function(self)
	if self.spotBuffInfo == nil or self.spotBuffInfo.nightView == nil then
		return -1;
	end
	return self.nightView;
end

local InitData = function(self)
	if not CS.System.String.IsNullOrEmpty(self.consumption_item) then
		local txt = Split(self.consumption_item,";");
		for j=1,#txt do
			local mtxt = txt[j];
			local temp = Split(mtxt,":");
			local itemid = tonumber(temp[1]);
			local num = tonumber(temp[2]);
			if not self.itemCose:ContainsKey(itemid) then
				self.itemCose:Add(itemid,num);
			end
		end
		self.consumption_item = "";
	end
	if not CS.System.String.IsNullOrEmpty(self.drop_item) then
		local txt = Split(self.drop_item,";");
		for j=1,#txt do
			local mtxt = txt[j];
			local temp = Split(mtxt,":");
			local itemid = tonumber(temp[1]);
			local num = tonumber(temp[2]);
			if not self.itemDrop:ContainsKey(itemid) then
				self.itemDrop:Add(itemid,num);
			end
		end
		self.drop_item = "";
	end
	self:InitData();	
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
util.hotfix_ex(CS.SpecialSpotAction,'get_nightView',nightView)
util.hotfix_ex(CS.MissionSkillCfg,'InitData',InitData)
