local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSquadListLabelController)
local myimgStarChild_train = function(self, index)
	local path = string.format("List/StateSquadExp/Star/Star%d/Image", index);
    return self.transform:Find(path):GetComponent(typeof(CS.ExImage));
end
util.hotfix_ex(CS.CommonSquadListLabelController,'imgStarChild_train',myimgStarChild_train)