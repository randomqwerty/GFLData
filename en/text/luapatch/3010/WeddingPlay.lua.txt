local util = require 'xlua.util'
xlua.private_accessible(CS.WeddingPlay)

local Awake = function(self)
	self:Awake();
	local dialog = self.transform:Find("border/Dialogue"):GetComponent(typeof(CS.UnityEngine.UI.Text));
	dialog.resizeTextForBestFit = true;
end

util.hotfix_ex(CS.WeddingPlay,'Awake',Awake)
