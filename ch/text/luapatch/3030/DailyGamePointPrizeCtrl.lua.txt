local util = require 'xlua.util'
xlua.private_accessible(CS.DailyGamePointPrizeCtrl)

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtTrans1 = self.transform:Find("Left/First/Tex_First");
		if txtTrans1~= nil then
			txtTrans1:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40465);
		end
		local txtTrans2 = self.transform:Find("Content/Reward/RewardScroll/RewardList/RewardCard/Img_First/Tex_First");
		if txtTrans2~= nil then
			txtTrans2:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40465);
		end
		local txtTrans3 = self.transform:Find("Left/PointsView/Tex_Now");
		if txtTrans3~= nil then
			txtTrans3:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(10068);
		end
	end
end


util.hotfix_ex(CS.DailyGamePointPrizeCtrl,'Awake',Awake)