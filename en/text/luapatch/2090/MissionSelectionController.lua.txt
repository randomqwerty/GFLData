local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionController)

local InitUIElements = function(self)
	self:InitUIElements();
	local txt = self.transform:Find("SimCombat/Introduce/Header/Btn_CurrentSimEnergy/Tex_Empty")
	if txt ~= nil then
		local textE = txt:GetComponent(typeof(CS.ExText));
		textE.text = CS.Data.GetLang(40406);
	end
	local txt1 = self.transform:Find("SimCombat/Introduce/Header/Btn_CurrentPotentialEnergy/Tex_Empty")
	if txt1 ~= nil then
		local textE = txt1:GetComponent(typeof(CS.ExText));
		textE.text = CS.Data.GetLang(40406);
	end
end
local SwitchToSimBattle  = function(self,btn)
	self:SwitchToSimBattle(btn)
	if CS.GameData.userInfo.level < 12 then
		return
	else
		self:OnClickSimCampaign(CS.MissionSelectionController.currentSelectedSimCoinTypeId)
	end
end
util.hotfix_ex(CS.MissionSelectionController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.MissionSelectionController,'SwitchToSimBattle',SwitchToSimBattle)


