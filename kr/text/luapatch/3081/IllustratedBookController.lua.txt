local util = require 'xlua.util'
xlua.private_accessible(CS.IllustratedMusicCollectionCtrl)



local mShowMusicView = function(self)
	self:ShowMusicView()
	if CS.Utility.rr > 1.01 then
		local trans = self.tweenPlay.transform:GetComponent(typeof(CS.UnityEngine.RectTransform));
		local margin = 0.5 * (CS.Utility.rr - 1) * 2048;
		trans.offsetMin = CS.UnityEngine.Vector2(margin,0);
		trans.offsetMax = CS.UnityEngine.Vector2(-margin,0);
	end
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw 
	or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
util.hotfix_ex(CS.IllustratedMusicCollectionCtrl,'ShowMusicView',mShowMusicView)
end