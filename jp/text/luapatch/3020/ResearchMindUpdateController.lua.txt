local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchMindUpdateController)

local Awake = function(self)
	self:Awake();
	local txt = self.transform:Find("Right/Confirm/Text_Confirm"):GetComponent(typeof(CS.ExText));
	txt.raycastTarget = false;
end

util.hotfix_ex(CS.ResearchMindUpdateController,'Awake',Awake)

