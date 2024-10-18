local util = require 'xlua.util'
xlua.private_accessible(CS.AVGController)

local mDialogueShowLog = function(self)
	self.transCircle.gameObject:SetActive(false);
	self:DialogueShowLog();
end
local mDialogueDisappearLog = function(self)
	self:DialogueDisappearLog();
	self.transCircle.gameObject:SetActive(true);
end
local mAwake = function(self)
	self:Awake();
	self.transCircle:SetParent(self.goDialogue.transform,false);
end

util.hotfix_ex(CS.AVGController,'Awake',mAwake)
--util.hotfix_ex(CS.AVGController,'DialogueShowLog',mDialogueShowLog)
--util.hotfix_ex(CS.AVGController,'DialogueDisappearLog',mDialogueDisappearLog)


