local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSquadListLabelController)
local myimgStarChild_train = function(self, index)
	local path = string.format("List/StateSquadExp/Star/Star%d/Image", index);
    return self.transform:Find(path):GetComponent(typeof(CS.ExImage));
end

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local txt = self.transform:Find("Tips/AdvanceTips/UI_Text");
		txt.gameObject:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190275);
	end
end
util.hotfix_ex(CS.CommonSquadListLabelController,'imgStarChild_train',myimgStarChild_train)
util.hotfix_ex(CS.CommonSquadListLabelController,'Awake',Awake)