local util = require 'xlua.util'
xlua.private_accessible(CS.AdjustAdjutantScaleController)

local OnClickReset = function(self)
	if self.isLeftAdjutant then
		local pic = self.nowRectTransform:GetComponent(typeof(CS.CommonPicController));
		if pic ~= nil then
			pic:CheckPos();
		end
	else
		local pic = self.nowRectTransform2:GetComponent(typeof(CS.CommonPicController));
		if pic ~= nil then
			pic:CheckPos();
		end		
	end
end

local Init = function(self,info,rightInfo,bFromEditBtn,bEditBg)
	if bEditBg ~= nil then
		self:Init(info,rightInfo,bFromEditBtn,bEditBg);
	else
		self:Init(info,rightInfo,bFromEditBtn);
	end
	self:OnClickReset();
end
util.hotfix_ex(CS.AdjustAdjutantScaleController,'OnClickReset',OnClickReset)
util.hotfix_ex(CS.AdjustAdjutantScaleController,'Init',Init)




