local util = require 'xlua.util'
xlua.private_accessible(CS.SquadStateController)

local Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Squadcultivate/Right/ChipPoint/Tex_Point");
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

util.hotfix_ex(CS.SquadStateController,'Start',Start)