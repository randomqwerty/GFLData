local util = require 'xlua.util'
xlua.private_accessible(CS.FormationEffectItemController)
local _SetData = function(self,gun,skinId)
	 self:SetData(gun,skinId);
	 
	 if  CS.SangvisGunStateController.Instance ~= nil and self.currentGun ~= nil then
	 	local scale =self.currentGun:GetSpineScale()
		self.meshRenderer.gameObject.transform.localScale = CS.UnityEngine.Vector3(170 * scale.x, 170 * scale.y,170 * scale.z);
	 end
end
util.hotfix_ex(CS.FormationEffectItemController,'SetData',_SetData)


