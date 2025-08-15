local util = require 'xlua.util'
xlua.private_accessible(CS.BattleBackgroundSortingController)
local SetTextureScale = function(self,meshRenderer)
	if self.gameObject.name == "airport_slg(Clone)" then
		meshRenderer.material.renderQueue = 2450;
	end
end
util.hotfix_ex(CS.BattleBackgroundSortingController,'SetTextureScale',SetTextureScale)

