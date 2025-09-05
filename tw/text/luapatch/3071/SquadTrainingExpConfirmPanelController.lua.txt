local util = require 'xlua.util'
xlua.private_accessible(CS.SquadTrainingExpConfirmPanelController)

local CheckCanStart = function(self)
	if CS.GameData.userInfo.buildCoin == 0 then
		CS.CommonController.MessageBox(CS.Data.GetLang(190151))
		return false
	else
		return self:CheckCanStart()
	end
end
util.hotfix_ex(CS.SquadTrainingExpConfirmPanelController,'CheckCanStart',CheckCanStart)