local util = require 'xlua.util'
xlua.private_accessible(CS.CommonColorItemController)

local _Start = function(self)
	self:Start();
	if self.imgGroundColor~=nil and self.imgGroundColor.gameObject.activeSelf==true then
		self.imgGroundColor.gameObject:SetActive(false);
	end
end

util.hotfix_ex(CS.CommonColorItemController,'Start',_Start)

