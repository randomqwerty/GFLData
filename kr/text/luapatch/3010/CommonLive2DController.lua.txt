local util = require 'xlua.util'
xlua.private_accessible(CS.CommonLive2DController)

local SetScenePosNew = function(self)
	local scale = self.currModel.transform.localScale;
	self:SetScenePosNew();
	print(self.currModel.transform.localScale.x);
	if self.currModel.transform.localScale.x == 1 then
		self.currModel.transform.localScale = scale;
	end
end

util.hotfix_ex(CS.CommonLive2DController,'SetScenePosNew',SetScenePosNew)




