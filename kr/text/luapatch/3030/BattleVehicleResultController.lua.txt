local util = require 'xlua.util'

xlua.private_accessible(CS.BattleVehicleResultController)
local FP = CS.TrueSync.FP
local Init = function(self,jsondata,curSpot)

	self:Init(jsondata,curSpot)
	self:StopAllCoroutines()
	self:StartCoroutine(self:UpdateVehicleExp())
	self:StartCoroutine(self:ShowVehicleSpine())
	self:StartCoroutine(self:ShowCrewMember())
	self:StartCoroutine(self:ShowRank())
end
local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Right/Information/BGNode/Text_VehicleEXP");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(290142);
	end
end
util.hotfix_ex(CS.BattleVehicleResultController,'Init',Init)
util.hotfix_ex(CS.BattleVehicleResultController,'InitUIElements',InitUIElements)