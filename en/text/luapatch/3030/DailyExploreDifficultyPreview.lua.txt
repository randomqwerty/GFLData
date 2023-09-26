local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreDifficultyPreview)

local _RefreshUI = function(self)
	for i=0,self.transVehicleIconHolder.childCount-1 do
		CS.UnityEngine.Object.Destroy(self.transVehicleIconHolder:GetChild(i).gameObject);
	end
	self:RefreshUI();
end


util.hotfix_ex(CS.DailyExploreDifficultyPreview,'RefreshUI',_RefreshUI)

