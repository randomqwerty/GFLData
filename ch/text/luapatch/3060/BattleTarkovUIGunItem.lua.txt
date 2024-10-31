local util = require 'xlua.util'
xlua.private_accessible(CS.BattleTarkovUIGunItem)
--xlua.private_accessible(CS.GF.Tarkov.TarkovDragItem)


local UpdateGunState = function(self,data)
	self:UpdateGunState(data)
	if self.showLevel >=2 then
		self.transCard1:Find("Img_CardBG/Img_Lv1BG").gameObject:SetActive(true)
		self.transCard2:Find("Img_CardBG/Img_Lv1BG").gameObject:SetActive(true)
		self.transCard3:Find("Img_CardBG/Img_Lv1BG").gameObject:SetActive(true)
		self.transCardUnavailable:Find("Img_CardBG/Img_Lv1BG").gameObject:SetActive(true)
	end
	if self.showLevel >=3 then
		self.transCard1:Find("Img_CardBG/Img_Lv2BG").gameObject:SetActive(true)
		self.transCard2:Find("Img_CardBG/Img_Lv2BG").gameObject:SetActive(true)
		self.transCard3:Find("Img_CardBG/Img_Lv2BG").gameObject:SetActive(true)
		self.transCardUnavailable:Find("Img_CardBG/Img_Lv2BG").gameObject:SetActive(true)
	end
	
end
local lastFrameAvailable
local UpdateUpgradeStatus = function(self)
	--update each frame
	lastFrameAvailable = self.goCard1MPAvailable.activeSelf
	self:UpdateUpgradeStatus()
	if lastFrameAvailable == false and self.goCard1MPAvailable.activeSelf then
		local goEffect = self.goCard1MPAvailable.transform:Find("AQLD_gq_liang").gameObject
		goEffect:SetActive(false)
		goEffect:SetActive(true)
		goEffect = self.goCard2MPAvailable.transform:Find("AQLD_gq_liang").gameObject
		goEffect:SetActive(false)
		goEffect:SetActive(true)
		goEffect = self.goCard3MPAvailable.transform:Find("AQLD_gq_liang").gameObject
		goEffect:SetActive(false)
		goEffect:SetActive(true)

	end
	local onBattleField = self.gunData.maxStock - self.gunData.remainStock
	local deadCount = self.gunData.deadCount
	local diff = onBattleField - deadCount
	if diff < 0 then
		diff = 0 
	end
	if onBattleField > 0 then
		self.transform:Find("Survived").gameObject:SetActive(true)
		local text = self.transform:Find("Survived/Text_Survived").gameObject:GetComponent(typeof(CS.ExText))
		text.text =  CS.Data.GetLang(60832):gsub("{0}",tostring(diff))		
	end
end

util.hotfix_ex(CS.BattleTarkovUIGunItem,'UpdateGunState',UpdateGunState)
util.hotfix_ex(CS.BattleTarkovUIGunItem,'UpdateUpgradeStatus',UpdateUpgradeStatus)

