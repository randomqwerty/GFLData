local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAutoBattleController)

local DataClear = function()
	CS.DeploymentAutoBattleController.lastautoFairySkill = CS.ConfigData.autoFairySkill;
	CS.DeploymentAutoBattleController.DataClear();
end
util.hotfix_ex(CS.DeploymentAutoBattleController,'DataClear',DataClear)