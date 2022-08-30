local util = require 'xlua.util'
xlua.private_accessible(CS.DormFurniturePieceController)
local InitSpine = function(self)
	self:InitSpine();
	if self.info ~= nil and self.info.code == "Space2022_backgroundWindow" then
		if self.spineMeshRenderer.sharedMaterial ~= nil then
			self.spineMeshRenderer.sharedMaterial.renderQueue = 2500;
		end
	end
end

util.hotfix_ex(CS.DormFurniturePieceController,'InitSpine',InitSpine)
