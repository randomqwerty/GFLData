local util = require 'xlua.util'
xlua.private_accessible(CS.PresentItemController)

local SetGun = function(self,gunInfo)
	self:SetGun(gunInfo);
	if gunInfo ~= nil then
		if CS.GameData.userInfo.dctGunCollect:ContainsKey(gunInfo.id) then
		self.objHave:SetActive(true);
		else
		self.objHave:SetActive(false);
		end
	end
end

local SetSangvis = function(self,sangvisGun)
	self:SetSangvis(sangvisGun);
	if sangvisGun ~= nil then
		if CS.GameData.dicSangvisGunCollect:ContainsKey(sangvisGun.id) then
			self.objHave:SetActive(true);
		else
			self.objHave:SetActive(false);
		end
	end
end

local SetFairy = function(self,fairyInfo)
	self:SetFairy(fairyInfo);
	if fairyInfo ~= nil then
		if CS.GameData.userInfo.dictFairyCollect:ContainsKey(fairyInfo.id) then
			self.objHave:SetActive(true);
		else
			self.objHave:SetActive(false);
		end
	end
end

util.hotfix_ex(CS.PresentItemController,'SetGun',SetGun)
util.hotfix_ex(CS.PresentItemController,'SetSangvis',SetSangvis)
util.hotfix_ex(CS.PresentItemController,'SetFairy',SetFairy)