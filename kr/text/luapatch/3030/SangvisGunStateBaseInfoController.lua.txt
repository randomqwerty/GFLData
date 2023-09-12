local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGunStateBaseInfoController)

local _Start = function(self)
	self:Start();
	local cost = self.transform:Find("Frame/CostBG");
	if cost ~=nil then
		cost.gameObject:SetActive(true);
		cost.localPosition= CS.UnityEngine.Vector3(38.6,224.2,0);
	end
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal 
	or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw 
	or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
	util.hotfix_ex(CS.SangvisGunStateBaseInfoController,'Start',_Start)
end
