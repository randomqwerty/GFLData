local util = require 'xlua.util'
xlua.private_accessible(CS.CanvasEquipGroupInfoFrameController)
xlua.private_accessible(CS.ExImage)
xlua.private_accessible(CS.EquipGourpEquipListController)
local mInitUIElements = function(self)
	self:InitUIElements();
	print("InitUIElements")
	local img1 =self:equipGourpEquipList(1).noHave:GetComponent(typeof(CS.ExImage));
	local img2 =self:equipGourpEquipList(2).noHave:GetComponent(typeof(CS.ExImage));
	img2.sprite = img1.sprite;
	img1=nil;
	img2=nil;
end

util.hotfix_ex(CS.CanvasEquipGroupInfoFrameController,'InitUIElements',mInitUIElements)

