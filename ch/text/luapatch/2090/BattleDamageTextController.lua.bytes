local util = require 'xlua.util'
xlua.private_accessible(CS.BattleDamageTextController)

local Awake= function(self)
	self:Awake();
	local topTime = self.transform:Find("Text/CommonTextHolder");
	local obj1 = CS.ResManager.GetObjectByPath("AtlasClips2090/免疫");
	if obj1 ~= nil then
		--print("载入图片");
		topTime:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
	end
end
util.hotfix_ex(CS.BattleDamageTextController,'Awake',Awake)

