local util = require 'xlua.util'
xlua.private_accessible(CS.PassOrderController)
xlua.private_accessible(CS.ExText)
xlua.private_accessible(CS.Data)
xlua.private_accessible(CS.CommonTopController)
local myScrollCallBack = function(self,index)
    self.specialItem.isSpecialView = false;
    self:ScrollCallBack(index)
end
local myStart = function(self)
	self:Start();
	local txt1 = self.transform:Find("BuyPass/NormalPass/Btn_Buy/Img_Bought/Tex_Bought");
	if txt1 ~= nil then
		local textshow = txt1:GetComponent(typeof(CS.ExText));
		textshow.text = CS.Data.GetLang(1215);
	end	
	local txt2 = self.transform:Find("BuyPass/DeluxePass/Btn_Buy/Img_Bought/Tex_Bought");
	if txt2 ~= nil then
		local textshow = txt2:GetComponent(typeof(CS.ExText));
		textshow.text = CS.Data.GetLang(1215);
	end	
end
local myRequestGetAllBonusHandle = function(self,request)
	self:RequestGetAllBonusHandle(request)
	CS.CommonTopController.TriggerRefershResourceEvent();
end
util.hotfix_ex(CS.PassOrderController,'ScrollCallBack',myScrollCallBack)
util.hotfix_ex(CS.PassOrderController,'Start',myStart)	
util.hotfix_ex(CS.PassOrderController,'RequestGetAllBonusHandle',myRequestGetAllBonusHandle)	