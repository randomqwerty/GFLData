local util = require 'xlua.util'
xlua.private_accessible(CS.IllustratedBookController)

local Start_New = function(self)
	self:Start()
    self.characterButton.isOn = true;
end

local ShowUI_New = function(self)
    if self._illustratedBookCharacterListController~= nil and self._illustratedBookCharacterListController.gameObject.activeSelf == true then        
        self.transform:SwitchSidebar("", false);
        self.illustratedBookCharacterListController:SceneBackRefresh();          
    end

    if CS.CommonController.sceneJumpType == 11 then        
        self:SelectPlayBackPage(CS.CommonController.subJumpType);        
    end

end

util.hotfix_ex(CS.IllustratedBookController,'Start',Start_New)
util.hotfix_ex(CS.IllustratedBookController,'ShowUI',ShowUI_New)
