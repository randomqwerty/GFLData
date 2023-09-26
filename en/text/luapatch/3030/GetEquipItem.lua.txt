local util = require 'xlua.util'
xlua.private_accessible(CS.GetEquipItem)

local _PlayGetEquipAnim = function(self,equip,action)
	if CS.Utility.loadedLevelName == "Factory" or CS.Utility.loadedLevelName == "StoreRoom" then
		self:SetLayer("UI",50);

		local lable=self.goBackCard:GetComponent(typeof(CS.UnityEngine.Canvas))
		local lable1=self.textlight1R:GetComponent(typeof(CS.UnityEngine.Canvas))
		local lable2=self.textlight2S:GetComponent(typeof(CS.UnityEngine.Canvas))
		local lable3=self.textlight3F:GetComponent(typeof(CS.UnityEngine.Canvas))

		local BlockColor=self.BlockColor.gameObject:GetComponent(typeof(CS.UnityEngine.Canvas))
		if lable ~=nil then
			lable.sortingLayerName = "UI";
		end
		if lable1 ~=nil then
			lable1.sortingLayerName = "UI";
			lable1.sortingOrder = 53;
		end
		if lable2 ~=nil then
			lable2.sortingLayerName = "UI";
			lable2.sortingOrder = 53;
		end
		if lable3 ~=nil then
			lable3.sortingLayerName = "UI";
			lable3.sortingOrder = 53;
		end
		if BlockColor ~=nil then
			BlockColor.sortingLayerName = "UI";
		end
	end
	self:PlayGetEquipAnim(equip,action);
end

util.hotfix_ex(CS.GetEquipItem,'PlayGetEquipAnim',_PlayGetEquipAnim)