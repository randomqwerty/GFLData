local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchFairyStrengthenController)
xlua.private_accessible(CS.CommonFairyListLabelController) 


local _RefreshUI = function(self)
	self:RefreshUI(); 
	if self.currentLabel~=nil then
		self.currentLabel.btnButton.canHold=false;
	end
end
util.hotfix_ex(CS.ResearchFairyStrengthenController,'RefreshUI',_RefreshUI) 

