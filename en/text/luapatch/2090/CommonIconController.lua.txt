local util = require 'xlua.util'
xlua.private_accessible(CS.CommonIconController)
local Awake = function(self)
   self:Awake();
	local txtTrans = self.transform:Find("HaveDropGun/Image/UI_Text");
	if txtTrans ~= nil then
		local txt = txtTrans:GetComponent(typeof(CS.ExText));
		txt.text = CS.Data.GetLang(30494);
	end
end
util.hotfix_ex(CS.CommonIconController,'Awake',Awake)