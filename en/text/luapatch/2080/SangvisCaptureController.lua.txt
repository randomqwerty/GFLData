local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisCaptureController)
local myRefreshLeftDogItemUI = function(self)
    for i=0, self.sangvisDogItemList.Count - 1 do
		self.sangvisDogItemList[i].gameObject:SetActive(false);
	end
    self:RefreshLeftDogItemUI()
end
util.hotfix_ex(CS.SangvisCaptureController,'RefreshLeftDogItemUI',myRefreshLeftDogItemUI)