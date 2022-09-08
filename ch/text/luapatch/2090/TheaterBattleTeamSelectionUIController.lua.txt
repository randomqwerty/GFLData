local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterBattleTeamSelectionUIController)
local InitUIElements = function(self)
	self:InitUIElements();
	local type = self.transform:Find("Right/MissionInfo/Img_EnemyTypeC/Tex_EnemyType");
	if type ~= nil then
		local textType = type:GetComponent(typeof(CS.ExText));
		textType.text = CS.Data.GetLang(210104);
	end	
end
util.hotfix_ex(CS.TheaterBattleTeamSelectionUIController,'InitUIElements',InitUIElements)