local util = require 'xlua.util'
xlua.private_accessible(CS.AdjustAdjutantScaleController)

local OnClickSwitchDamaged = function(self)
	local damaged = false;	
	if self.editAdjutantInfo.GetAdjutantType == CS.AdjutantInfo.AdjutantType.GUN then		
		local picController = CS.HomeController.Instance.adjutantController:GetPicController(self.isLeftAdjutant);
		if picController ~= nil and picController.live2dHolder ~= nil and picController.transform.childCount > 1 then
			damaged = not picController.transform:GetChild(1).gameObject.activeSelf;
			picController:SwitchDamaged(damaged);
			picController:SetLayer("Live2DBG");
		else
			damaged = not picController.hurt;
			picController:SwitchDamaged(damaged);
			if picController.imagePic == nil then
				picController:SetLayer("Live2DBG");
				if self.isLeftAdjutant then
					CS.HomeController.Instance.adjutantController.isAdjutantLive2D = true;
				else
					CS.HomeController.Instance.adjutantController.isAdjutantLive2D2 = true;
				end
			end
		end
		self.editAdjutantInfo.isDamage = damaged;
	end
end

util.hotfix_ex(CS.AdjustAdjutantScaleController,'OnClickSwitchDamaged',OnClickSwitchDamaged)