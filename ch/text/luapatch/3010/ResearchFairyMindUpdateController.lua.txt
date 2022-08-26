local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchFairyMindUpdateController)

local UpdateCostItems_New = function(self, fairy)
	self:UpdateCostItems(fairy)

    local costMod = 0

    if fairy.mod < CS.FairyInfo.mindupdateCostItems:GetLength(0) then
    	costMod = fairy.mod
    else
    	costMod = 2
    end

	local objCostItem1 = self.uiHolder:GetUIElement("Right/Option/UpDescription/Img_Item1",typeof(CS.UnityEngine.GameObject));
	local objCostItem2 = self.uiHolder:GetUIElement("Right/Option/UpDescription/Img_Item2",typeof(CS.UnityEngine.GameObject));
    local costItem1 = CS.FairyInfo.mindupdateCostItems:GetValue(costMod,0);
    local costItem2 = CS.FairyInfo.mindupdateCostItems:GetValue(costMod,1);
    objCostItem1:SetActive(costItem1.amount > 0);
    objCostItem2:SetActive(costItem2.amount > 0);
end

util.hotfix_ex(CS.ResearchFairyMindUpdateController,'UpdateCostItems',UpdateCostItems_New)