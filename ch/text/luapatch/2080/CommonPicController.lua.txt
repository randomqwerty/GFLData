local util = require 'xlua.util'
xlua.private_accessible(CS.CommonPicController)

local GetCurrentPosData = function(self,sceneName,fatherName,rootName)
	if rootName == "PicHolder/TheaterMissiontSettlement(Clone)/Canvas/BattleController/" then
		rootName = "Pic/Result_New(Clone)/Canvas/BattleController/";
	end
	for i=0,self.posData.Count-1 do
		local data = self.posData[i];
		if data.path == "SkinHolder/Left/SkinDisplay(Clone)/CommodityHolder/SafeRect/Canvas/" then
			data.path = "SkinHolder/Left/SkinDisplay(Clone)/CommodityHolder/SafeRact/Canvas/";
		end
	end
	return self:GetCurrentPosData(sceneName,fatherName,rootName);
end

local SwitchDamaged = function(self,isHurt,image)
	self:SwitchDamaged(isHurt,image);
	local forceHide = false;
	if self.path == "PicHolder/DamagedPerformance(Clone)/Canvas/BattleController/" then
		forceHide = true;
	end
	if self.path == "PicHolder/UICombatSettlement(Clone)/Canvas/" then
		forceHide = true;
	end
	local bg = self.transform:Find("Bg");
	if bg ~= nil then
		local image = bg:GetComponent(typeof(CS.ExImage));
		if image.material ~= nil then
			image.material.renderQueue = 2990;
		end
		if self.hurt or forceHide then
			bg.gameObject:SetActive(false);
		else
			bg.gameObject:SetActive(true);
		end
	end
	local bg_D = self.transform:Find("Bg_D");
	if bg_D ~= nil then
		local image = bg_D:GetComponent(typeof(CS.ExImage));
		if image.material ~= nil then
			image.material.renderQueue = 2990;
		end
		if not self.hurt or forceHide then
			bg_D.gameObject:SetActive(false);
		else
			bg_D.gameObject:SetActive(true);
		end 
	end
end
util.hotfix_ex(CS.CommonPicController,'GetCurrentPosData',GetCurrentPosData)
util.hotfix_ex(CS.CommonPicController,'SwitchDamaged',SwitchDamaged)

