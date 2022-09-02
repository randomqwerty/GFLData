local util = require 'xlua.util'
xlua.private_accessible(CS.MallController)
xlua.private_accessible(CS.CommonSceneManagerController)
xlua.private_accessible(CS.DormUIController)
local myBackHome = function(self)
    self:BackHome()
	if(CS.CommonSceneManagerController.instance.stackPeekController.sceneName == "Dorm") then
		CS.DormUIController.Instance:GetComponent(typeof(CS.UnityEngine.Canvas)).enabled = true;
	end
end
util.hotfix_ex(CS.MallController,'BackHome',myBackHome)