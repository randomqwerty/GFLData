local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreBattleWindow)

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtTrans1 = self.transform:Find("Bottom/Tips/Tex_Tip");
		if txtTrans1~= nil then
			txtTrans1:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(280530);
		end
	end
end


util.hotfix_ex(CS.DailyExploreBattleWindow,'Awake',Awake)