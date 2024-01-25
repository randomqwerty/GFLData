local util = require 'xlua.util'
xlua.private_accessible(CS.BattleVehicleResultController)


local BattleVehicleResultControllerInitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local txt = self.transform:Find("Right/Information/BGNode/Text_VehicleEXP"):GetComponent(typeof(CS.ExText));
		txt.text = CS.Data.GetLang(290142);
	end
end

local VehicleStateControllerInitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local txt = self.transform:Find("VehicleDetail/Main/Detail/CurrentComponentInfo/ComponentRollSkill/ComponentRollSkillTitle/Text_ComponentRollSkil"):GetComponent(typeof(CS.ExText));
		txt.text = CS.Data.GetLang(290115);
	end
end
util.hotfix_ex(CS.BattleVehicleResultController,'InitUIElements',BattleVehicleResultControllerInitUIElements)
util.hotfix_ex(CS.VehicleStateController,'InitUIElements',VehicleStateControllerInitUIElements)