local util = require 'xlua.util'
xlua.private_accessible(CS.CommonBundleConfirmBoxController)

local Init = function(self,mallGood,package)
	self:Init(mallGood,package);
	if self.SkinGunCode == "NPC_Kalina" then
		self.objPrompt:SetActive(false);
	end
end
util.hotfix_ex(CS.CommonBundleConfirmBoxController,'Init',Init)
