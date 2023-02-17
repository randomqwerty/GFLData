local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamFloatingInfo)

local UpdateInfo = function(self)
	self:UpdateInfo();
	for i=0,self.buffItemList.Count-1 do
		local buffItem = self.buffItemList[i];
		if buffItem ~= nil and not buffItem:isNull() then
			if self.useenemyUI then
				buffItem.transform:SetParent(self.enemybufflist, false);
			else
				buffItem.transform:SetParent(self.allybufflist, false);
			end
		end
	end
end

util.hotfix_ex(CS.DeploymentAllyTeamFloatingInfo,'UpdateInfo',UpdateInfo)



