local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialOPSController)
xlua.private_accessible(CS.OPSConfig)
xlua.private_accessible(CS.OPSPanelBackGround)
xlua.private_accessible(CS.CommonSceneManagerController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ExButton)
xlua.private_accessible(CS.ResManager)
local myLoadReturn = function(self)
	local Obj = CS.ResManager.GetObjectByPath(string.format("Pics/ActivityMap/%s", CS.OPSConfig.Instance.OPSReturn));
	if (Obj ~= nil) then
		local returnObject = CS.UnityEngine.Object.Instantiate(Obj):GetComponent(typeof(CS.ExButton));
		returnObject.transform:SetParent(self.Top, false);
		returnObject.transform:SetAsLastSibling();
		returnObject:AddOnClickBack(function ()
				CS.CommonSceneManagerController.instance:PopController();
				CS.CommonController.GotoScene("MissionSelection");
			end);
	end
end
util.hotfix_ex(CS.SpecialOPSController,'LoadReturn',myLoadReturn)