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

util.hotfix_ex(CS.OPSPanelController,'Start',Start)
util.hotfix_ex(CS.OPSPanelController,'ShowItemLimitUINew',ShowItemLimitUINew)


