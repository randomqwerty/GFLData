local util = require 'xlua.util'
xlua.private_accessible(CS.GuideManagerController)

local SetParentAndLayer = function(self)
	self:SetParentAndLayer();
	if CS.Utility.loadedLevelName == "Formation" or CS.Utility.loadedLevelName == "Factory" then
	 	local transformCanvas = CS.CommonController.MainCanvas.transform;
		local topcanvas = transformCanvas:Find("Top"):GetComponent(typeof(CS.UnityEngine.Canvas));
		topcanvas.sortingLayerName = "Default";
	end
end

local GetStatuseCount = function(arrGuideStatus)
	local count = 0;
	for i=0,arrGuideStatus.Length-1 do
		if arrGuideStatus[i] == true then
			count = count +1;
		end
	end
	return count;
end

local ChangeGuideStatus = function(self,url)
	local check0 = GetStatuseCount(self.arrGuideStatus);
	self:ChangeGuideStatus(url);
	local check1 = GetStatuseCount(self.arrGuideStatus);
	if check0 ~= check1 then
		CS.CommonGuideController.Instance:RequestSetGuideInfo();
	end
end
util.hotfix_ex(CS.GuideManagerController,'SetParentAndLayer',SetParentAndLayer)
util.hotfix_ex(CS.CommonGuideController,'ChangeGuideStatus',ChangeGuideStatus)
