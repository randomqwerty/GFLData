local util = require 'xlua.util'
local endBG = 0;
local OnVideoPlayEnd = function()
	CS.AVGController.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = true;
	if endBG > 0 then
		local bgCon = CS.AVGController.Instance.backgroundController;
		if bgCon.backgroundInfo ~= nil then
			bgCon:ChangeBackgroundImage(bgCon.imageBackground,endBG);
		end
	end
end

Awake = function()
end

Start = function()
	if self.transform.childCount > 0 then
		local childCount = self.transform.childCount
		for i=1,childCount do
			local name = self.transform:GetChild(i-1).name.."(Clone)"
			local target = self.transform.parent:Find(name)
			if target ~= nil then
				CS.Utility.Destroy(target.gameObject)
			end
		end
	end
	
end