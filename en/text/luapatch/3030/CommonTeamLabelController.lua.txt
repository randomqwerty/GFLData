local util = require 'xlua.util'
xlua.private_accessible(CS.CommonTeamLabelController)

local OnClick = function(self)
	for i=0,self.toggleGroup.listToggle.Count -1 do
		local toggle = self.toggleGroup.listToggle[i];
		if toggle.arrSprite[0] == nil then
			toggle.arrSprite[0] = toggle.image.sprite;
		end
	end
	self:OnClick();
end
util.hotfix_ex(CS.CommonTeamLabelController,'OnClick',OnClick)