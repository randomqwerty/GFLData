local util = require 'xlua.util'
xlua.private_accessible(CS.GunStateRelatedStoryController)

xlua.private_accessible(CS.GunStateNumericalInfoController)
local Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local trans = self.transform:Find("Tilte/Tex_Tilte");
		if trans ~= nil then
			local tex = trans:GetComponent(typeof(CS.ExText));
			tex.text = CS.Data.GetLang(35169);
		end	
	end
end
local GotoCombine = function(self)
	if self.gun.status == CS.GunStatus.exploring then
		local msg = CS.Data.GetLang(100167);
		CS.CommonController.LightMessageTips(msg);
		msg=nil;
	else
		self:GotoCombine();
	end
end
local GotoStrength = function(self)
	if self.gun.status == CS.GunStatus.exploring then
		local msg = CS.Data.GetLang(100167);
		CS.CommonController.LightMessageTips(msg);
		msg=nil;
	else
		self:GotoStrength();
	end
end
util.hotfix_ex(CS.GunStateRelatedStoryController,'Start',Start)
util.hotfix_ex(CS.GunStateNumericalInfoController,'GotoCombine',GotoCombine)
util.hotfix_ex(CS.GunStateNumericalInfoController,'GotoStrength',GotoStrength)


