local util = require 'xlua.util'
xlua.private_accessible(CS.DormFurniturePieceController)
local InitSpine = function(self)
	self:InitSpine();
	self.spineMeshRenderer.sharedMaterial.renderQueue = 2500;
end

util.hotfix_ex(CS.DormFurniturePieceController,'InitSpine',InitSpine)
