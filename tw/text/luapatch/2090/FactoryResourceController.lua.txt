local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryResourceController)

local OnCommitClicked_New = function(self)
	self.package = nil
	self:OnCommitClicked()
end

util.hotfix_ex(CS.FactoryResourceController,'OnCommitClicked',OnCommitClicked_New)
