local util = require 'xlua.util'
xlua.private_accessible(CS.ReinforcementFixAllConfirmBoxController)

local InitFixAlly = function(self,allyteam,spotid,onComplete)
	self:InitFixAlly(allyteam,spotid,onComplete);
	for i=self.uiData.listGunToFix.Count-1,0,-1 do
		self.uiData.listGunToFix[i].teamId = allyteam.teamId;
		if self.uiData.listGunToFix[i].life == self.uiData.listGunToFix[i].maxLife then
			self.uiData.listGunToFix:RemoveAt(i);			
		end
	end
	for i=self.uiData.listSangvisToFix.Count-1,0,-1 do
		self.uiData.listSangvisToFix[i].teamId = allyteam.teamId;
		if self.uiData.listSangvisToFix[i].life == self.uiData.listSangvisToFix[i].maxLife then
			self.uiData.listSangvisToFix:RemoveAt(i);			
		end
	end
end


util.hotfix_ex(CS.ReinforcementFixAllConfirmBoxController,'InitFixAlly',InitFixAlly)
