local util = require 'xlua.util'
xlua.private_accessible(CS.CommonTopStoryController)

local GetFrontImage = function(self,picName)        
    self:GetFrontImage(picName);
	if CS.System.String.IsNullOrEmpty(picName) then
		self.imgFront.gameObject:SetActive(false);
	else
		self.imgFront.gameObject:SetActive(true);
	end
end

util.hotfix_ex(CS.CommonTopStoryController,'GetFrontImage',GetFrontImage)

