local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleStateCrewItemController)

local mInit = function(self,data)
	if CS.CommonSceneManagerController.instance.currentSceneName == "IllustratedBook" then
		self._data=data;
		self.objEmpty:SetActive(true);
		self.objDetail:SetActive(false);
		self.textCrewBonus.gameObject:SetActive(false);
		self.textCrewBonus.text = self._data.crew:GetCrewBonusDes();
		self.objEmptyIcon:SetActive(true);
		self.transIconHolder.gameObject:SetActive(false);
		self.textCrewName.text = self._data.crew.info.Name;
		self:LoadCrewSlotIcon(self._data.crew);
		self.textMemberType.text = self._data.crew.info.TypeDes;
        self.textMemberContent.text = self._data.crew.info.Description;
	else	 
		self:Init(data);
	end
end

util.hotfix_ex(CS.VehicleStateCrewItemController,'Init',mInit)
