local util = require 'xlua.util'
xlua.private_accessible(CS.OPSSpineControl)

local Show = function(self,play)
	self:Show(play);
	if self.spinecode == "operationBed" then
		self.shadow:SetActive(false);
	elseif self.spinecode == "monitor" then
		self.shadow:SetActive(false);
	elseif self.spinecode == "passingWindow" then
		self.shadow:SetActive(false);
	elseif self.spinecode == "filter" then
		self.shadow:SetActive(false);
	end
end


util.hotfix_ex(CS.OPSSpineControl,'Show',Show)
