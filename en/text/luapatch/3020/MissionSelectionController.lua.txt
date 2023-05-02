local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionController)
local Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtTrans1 = self.transform:Find("DailyGame/Top/Btn_Rank/Tex_Rank");
		if txtTrans1~= nil then
			txtTrans1:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40061);
		end
		local txtTrans2 = self.transform:Find("DailyGame/Bottom/Img_TitleBg/Tex_Title");
		if txtTrans2~= nil then
			txtTrans2:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40464);
		end
		local txtTrans3 = self.transform:Find("DailyGame/Top/Btn_Records/Tex_Records");
		if txtTrans3~= nil then
			txtTrans3:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40463);
		end
		local txtTrans4 = self.transform:Find("DailyGame/Bottom/Btn_Points/Tex_Points");
		if txtTrans4~= nil then
			txtTrans4:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(11004);
		end
		local txtTrans5 = self.transform:Find("DailyGame/Bottom/Img_BottomBg/Tex_MissionInfo");
		if txtTrans5~= nil then
			txtTrans5:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40461);
		end
	end
end
util.hotfix_ex(CS.MissionSelectionController,'Start',Start)
