local util = require 'xlua.util'
xlua.private_accessible(CS.SettingController)

local InitUIElements = function(self)
	self:InitUIElements();
	local text = self.transform:Find("Main/BackGround游戏/Switchs/Items/FunctionSetting/自动播放速度 /SliderNode/TextNode/Min");
	if text ~= nil then
		text:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(52149);
	end
end

util.hotfix_ex(CS.SettingController,'InitUIElements',InitUIElements)


