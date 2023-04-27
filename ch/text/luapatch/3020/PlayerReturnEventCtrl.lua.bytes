local util = require 'xlua.util'
xlua.private_accessible(CS.PlayerReturnEventCtrl)

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local imageTrans1 = self.transform:Find("FundsContent/ActivateCard/Img_Bg");
		if imageTrans1~= nil then
			local obj1 = CS.ResManager.GetObjectByPath("AtlasClips3010/回归基金");
			imageTrans1:GetComponent(typeof(CS.ExImage)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
		end
	end
end

util.hotfix_ex(CS.PlayerReturnEventCtrl,'Awake',Awake)
