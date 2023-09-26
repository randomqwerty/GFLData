local util = require 'xlua.util'
xlua.private_accessible(CS.ReinforcementController)

local mRequestStartFixHandle = function(self,www)
	self:RequestStartFixHandle(www);
	if self.listLabel.Count > 0 then

		for i=0,self.listLabel.Count-1 do
		 	self.listLabel[i]:CancelInvokeTimer();
		 	self.listLabel[i].isLocked = self.listLabel[i].id > CS.GameData.userInfo.maxFixSlot;
            self.listLabel[i]:UpdateInfo();
		end
	end
end


util.hotfix_ex(CS.ReinforcementController,'RequestStartFixHandle',mRequestStartFixHandle)

