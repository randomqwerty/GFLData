local util = require 'xlua.util'
xlua.private_accessible(CS.BreakoutIntelligenceItem)

local InitData = function(self, data)
	self.itemData = data
	self.txtPhase.text = data.phaseName

	local info = CS.GameData.listItemInfo:GetDataById(data.itemId)
	if info == nil then        
	    CS.NDebug.LogError("找不到item id = ", data.itemId)
	    return
	end

	self.imgIcon.sprite = CS.CommonController.LoadPngCreateSprite("DaBao/WorldCollide/ArenaBreakout/Intelligence/"..info.code);
	self.isLock = CS.GameData.GetItem(data.itemId) == 0;
	self.objLock:SetActive(self.isLock);
end

local OnClickSelf = function(self)
	if self.isLock then
		local tip = CS.System.String.Format(CS.Data.GetLang(280601),  self.itemData.phaseName);
		CS.CommonController.LightMessageTips(tip);
		return
	end

	self:OnClickSelf()
end


util.hotfix_ex(CS.BreakoutIntelligenceItem,'InitData',InitData)
util.hotfix_ex(CS.BreakoutIntelligenceItem,'OnClickSelf',OnClickSelf)



