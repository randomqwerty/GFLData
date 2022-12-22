local util = require 'xlua.util'
xlua.private_accessible(CS.AdjustAdjutantScaleController)

local OnClickReset = function(self)
	if self.isLeftAdjutant then
		if self.nowRectTransform ~= nil then
			local pic = self.nowRectTransform:GetComponent(typeof(CS.CommonPicController));
			if pic ~= nil then
				pic:CheckPos();
			end
		end
	else
		if self.nowRectTransform2 ~= nil then
			local pic = self.nowRectTransform2:GetComponent(typeof(CS.CommonPicController));
			if pic ~= nil then
				pic:CheckPos();
			end
		end		
	end
end

util.hotfix_ex(CS.AdjustAdjutantScaleController,'OnClickReset',OnClickReset)




