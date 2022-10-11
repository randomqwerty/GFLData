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

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local image = self.transform:Find("Top/ExternLayout/Collect/Image");
		image.gameObject:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips3010/圆");
		local image1 = self.transform:Find("Top/ExternLayout/EquipCollect/Img_CommonRate");
		image1.gameObject:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips3010/圆");
		local image2 = self.transform:Find("Top/ExternLayout/EquipCollect/Img_ExclusiveRate");
		image2.gameObject:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips3010/圆");
	end
end
util.hotfix_ex(CS.IllustratedBookController,'Start',Start_New)
util.hotfix_ex(CS.IllustratedBookController,'ShowUI',ShowUI_New)
util.hotfix_ex(CS.IllustratedBookController,'Awake',Awake)
