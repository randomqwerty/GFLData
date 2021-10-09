local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

local RefreshText = function(self)
	self:RefreshText();
	if CS.GameData.missionAction ~= nil then
		local num = CS.GameData.missionAction.enemyDieNumber + CS.GameData.missionAction.alldieallyNum;
		self.textDeadRestEnemyCount.text = tostring(num);
	end
end

local CheckWinTypeOr = function(logic,showTarget,medal)
	if medal == 1 then
		CS.DeploymentUIController.CheckWinTypeOr(logic,true,medal);
	else
		CS.DeploymentUIController.CheckWinTypeOr(logic,showTarget,medal);
	end	
end

local CheckTypeComplete = function(winTypeInfo,showTarget,process,medal)
	if winTypeInfo.type == 2302 then
		showTarget = false;
	end
	local result,process = CS.DeploymentUIController.CheckTypeComplete(winTypeInfo,showTarget,process,medal);
	return result,process;
end

local SwitchAbovePanel = function(self,show)
	self.goAbove:SetActive(show);
	self.goAbove.transform:SetAsLastSibling();
end
util.hotfix_ex(CS.DeploymentUIController,'RefreshText',RefreshText)
util.hotfix_ex(CS.DeploymentUIController,'CheckWinTypeOr',CheckWinTypeOr)
util.hotfix_ex(CS.DeploymentUIController,'CheckTypeComplete',CheckTypeComplete)
util.hotfix_ex(CS.DeploymentUIController,'SwitchAbovePanel',SwitchAbovePanel)



