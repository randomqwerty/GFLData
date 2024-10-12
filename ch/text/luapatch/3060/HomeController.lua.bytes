local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.HomeUserInfoNewController)
local ShowUI = function(self)
	self:ShowUI()
	
	--修复从首页指挥官信息跳转至指挥官服装商城返回后，spine和emoji未刷新
	if CS.HomeUserInfoNewController.InstanceExitAndCanUse and CS.HomeUserInfoNewController.Instance.commanderSpine ~= nil then
		CS.HomeUserInfoNewController.Instance.commanderSpine:RefreshSpineClothes()
		CS.HomeUserInfoNewController.Instance:InitEmoji()
	end
end

local CheckItemData = function(self)
	if CS.GameData.missionAction ~= nil then
		if CS.GameData.missionAction.missionInfo.campaign == 0 then
			return;
		end
	end
	self:CheckItemData();
end
util.hotfix_ex(CS.HomeController,'ShowUI',ShowUI)
util.hotfix_ex(CS.HomeController,'CheckItemData',CheckItemData)


