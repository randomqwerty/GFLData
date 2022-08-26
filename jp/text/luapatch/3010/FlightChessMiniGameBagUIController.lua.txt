local util = require 'xlua.util'
xlua.private_accessible(CS.FlightChessMiniGameBagUIController)
local mySetPlayerEnsureData = function(self, count, selfSure)
	if(count == 0) then
		self:SetPlayerEnsureData(count, selfSure);
	end
	if count == 1 and selfSure == true then
		self:SetPlayerEnsureData(count, selfSure);
	end
	if(selfSure == true) then
		self:SetPlayerEnsureData(count, selfSure);
	else
		self.count = count;
		self.selfSure = selfSure;
		self.sureItemObjList[0]:SetStatus(false);
		for i = 0, count - 1 do
			self.sureItemObjList[i + 1]:SetStatus(true);
		end
		for i = count, self.sureItemObjList.Count - 2 do
			self.sureItemObjList[i + 1]:SetStatus(false);
		end
	end
    
end
util.hotfix_ex(CS.FlightChessMiniGameBagUIController,'SetPlayerEnsureData',mySetPlayerEnsureData)