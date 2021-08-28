local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionSangvisSimDungeonBoxController)

local _OnClickShowList = function(self,pos)
	if CS.CommonCharacterListController.Instance == nil then 
		self.CharacterController.transform:SetParent(CS.CommonController.MainCanvas.transform);

		self.currentSelectedCharacterLabelId = pos; 
		self.gameObject:SetActive(false);
		CS.CommonCharacterListController.Instance:CreateList(CS.ListType.sangvis_sim, self.gameObject);
	else
		self.currentSelectedCharacterLabelId = pos; 
		self.gameObject:SetActive(false);
		CS.CommonCharacterListController.Instance:CreateList(CS.ListType.sangvis_sim, self.gameObject);
	end
end

util.hotfix_ex(CS.MissionSelectionSangvisSimDungeonBoxController,'OnClickShowList',_OnClickShowList)


