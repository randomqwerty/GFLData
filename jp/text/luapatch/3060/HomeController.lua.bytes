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
local mOnClickScaleUI = function(self,isScale)
	self:OnClickScaleUI(isScale)
	local canvasGroup = self.btnReturnPlayerObj:GetComponent(typeof(CS.UnityEngine.CanvasGroup));
	if canvasGroup==nil or canvasGroup:isNull() then
		canvasGroup=self.btnReturnPlayerObj:AddComponent(typeof(CS.UnityEngine.CanvasGroup));
	end
	if canvasGroup ~= nil and not canvasGroup:isNull() then
		if isScale==true then
			canvasGroup.alpha = 0.3;
		else		
			canvasGroup.alpha = 1;
		end		
	end
end
util.hotfix_ex(CS.HomeController,'ShowUI',ShowUI)
util.hotfix_ex(CS.HomeController,'CheckItemData',CheckItemData)
util.hotfix_ex(CS.HomeController,'OnClickScaleUI',mOnClickScaleUI)


