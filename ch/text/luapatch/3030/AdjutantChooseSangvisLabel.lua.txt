local util = require 'xlua.util'
xlua.private_accessible(CS.AdjutantChooseSangvisLabel)
xlua.private_accessible(CS.SangvisSmallPicController)

local CheckPicControllerSkin = function(self)
	self:CheckPicControllerSkin();
	if self.sangvisPicController ~= nil and  not self.sangvisPicController:isNull() then
		if self.adjutantInfo ~= nil and self.adjutantInfo.adjutantSkinId ~= 0 then
			self.sangvisPicController.dontFlip = true;
			self.sangvisPicController:CheckDirection();
		end
	end
end

util.hotfix_ex(CS.AdjutantChooseSangvisLabel,'CheckPicControllerSkin',CheckPicControllerSkin)