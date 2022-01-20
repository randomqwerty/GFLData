local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingInfo)

local ShowDropItem = function(self)
	self:ShowDropItem();
	for i=0,self.itemParent.childCount-1 do
		local trans =self.itemParent:GetChild(i):Find("Img_NumBg/Tex_Num"):GetComponent(typeof(CS.UnityEngine.RectTransform));
		trans.anchorMin = CS.UnityEngine.Vector2.zero;
		trans.anchorMax = CS.UnityEngine.Vector2.one;
		trans.offsetMin = CS.UnityEngine.Vector2.zero;
		trans.offsetMax = CS.UnityEngine.Vector2.zero;
	end
end


util.hotfix_ex(CS.DeploymentBuildingInfo,'ShowDropItem',ShowDropItem)



