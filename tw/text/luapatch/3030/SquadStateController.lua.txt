local util = require 'xlua.util'
xlua.private_accessible(CS.SquadStateController)
xlua.private_accessible(CS.DormVehicleVisitLogController)

local Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Squadcultivate/Right/ChipPoint/Tex_Point");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190304);
		txtPoint = self.transform:Find("Squadcultivate/PromotionMask/ChipPoint/Tex_Point");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190304);
		txtPoint = self.transform:Find("SquadChip/Right/BatchChip/Tex_Select");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190306);
		txtPoint = self.transform:Find("SquadChip/Right/NeedResources/Need/Tex_need");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190305);
		txtPoint = self.transform:Find("SquadChip/Right/NeedResources/Up/RessourcesUp1/Tex_ResName");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190086);
		txtPoint = self.transform:Find("SquadChip/Right/NeedResources/Up/RessourcesUp2/Tex_ResName");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190087);
		txtPoint = self.transform:Find("SquadChip/Right/NeedResources/Lock/RessourcesLock2/Tex_ResName");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(190307);
	end
end

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("ToggleGroupNode/Toggle_Visitors/Text_Visitors");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(31980);
		txtPoint = self.transform:Find("Toggle_ShowDorm/Label_Confirm");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(31981);
	end
end

local FriendShopGoodController_Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("HaveMask/Img_HaveBg/Tex_Have");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(110012);
	end
end
local ShowPlayerEnergy = function(self)
	self:ShowPlayerEnergy();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.energyObj.transform:Find("Main/Text_Info");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(290159);
	end
end
local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Detail/AttriLayout/txRateMax/txName");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(10204);
	end
end
util.hotfix_ex(CS.SquadStateController,'Start',Start)
util.hotfix_ex(CS.DormVehicleVisitLogController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.FriendShopGoodController,'Start',FriendShopGoodController_Start)
util.hotfix_ex(CS.DeploymentUIController,'ShowPlayerEnergy',ShowPlayerEnergy)
util.hotfix_ex(CS.FormationShowEquipInfoController,'Awake',Awake)