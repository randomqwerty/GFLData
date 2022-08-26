local util = require 'xlua.util'
xlua.private_accessible(CS.CommanderSpineAnimation)
local myLoadAttachmentPic = function(self,go,cloth,attachment,color)
    go.layer = self.transform.root.gameObject.layer;
	self:LoadAttachmentPic(go,cloth,attachment,color)
end
util.hotfix_ex(CS.CommanderSpineAnimation,'LoadAttachmentPic',myLoadAttachmentPic)