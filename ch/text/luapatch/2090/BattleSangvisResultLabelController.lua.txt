local util = require 'xlua.util'
xlua.private_accessible(CS.BattleSangvisResultLabelController)



local UpdateInfo = function(self)
	
	self:UpdateInfo()
	local scale =self.gun:GetSpineScale()
	self.SpineAnime.gameObject.transform.localScale = CS.UnityEngine.Vector3(130 * scale.x, 130 * scale.y,0) 
end


util.hotfix_ex(CS.BattleSangvisResultLabelController,'UpdateInfo',UpdateInfo)
