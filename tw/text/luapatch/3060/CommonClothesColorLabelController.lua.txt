local util = require 'xlua.util'
xlua.private_accessible(CS.CommonClothesColorLabelController)
 
local mInitUIElements = function(self)
	self:InitUIElements();
	 
	self.btnColorranRandomProbability.transform.localPosition=CS.UnityEngine.Vector3(self.btnColorranRandom.transform.localPosition.x+18,self.btnColorranRandom.transform.localPosition.y-150,0);
end


if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then		
util.hotfix_ex(CS.CommonClothesColorLabelController,'InitUIElements',mInitUIElements)
end


