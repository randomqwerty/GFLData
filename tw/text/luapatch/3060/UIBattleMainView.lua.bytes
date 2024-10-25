local util = require 'xlua.util'
xlua.private_accessible(CS.BattleTarkovUIBubbleTips)
-- 似乎Tarkov命名空间没添加到xlua热更下面
local HideAll = function(self)
	self:HideAll()
	self.transform.parent:Find("Main/Img_Mask").gameObject:SetActive(true)
end

util.hotfix_ex(CS.BattleTarkovUIBubbleTips,'HideAll',HideAll)


