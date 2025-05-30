local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGunStateController)

local mShowGunNumber = function(self)
	self:ShowGunNumber();
	if self.bookGunInfo ~= nil then
		if self.bookGunInfo.isAdditional == true and self.bookGunInfo.id > 100010 then
			local id = 	self.bookGunInfo.id - 100010
			self.textGunNember.text = id.."";
		end
	end
end
local mOnClickStateLableItem = function(self,enemy)
	if self.bookGunInfo ~= nil  and self.enemyState==true and enemy~=nil then
		if enemy.isAdditional == true then
			local info = CS.IllustratedBookSangvisGunInfo();
			info.enemyInfo = enemy;
        	info.enemyUnlock = true;
        	if enemy.sangvisInfo ~= nil then
        		info.captureUnlock = CS.GameData.dicSangvisGunCollect:ContainsKey(enemy.sangvisInfo.id)
        	else 
        		info.captureUnlock = false
        	end
        	self:InitData(self.currentLoadLevel, nil, info, self.enemyState,nil);
		else
			self:OnClickStateLableItem(enemy)
		end

		
	end
end
util.hotfix_ex(CS.SangvisGunStateController,'ShowGunNumber',mShowGunNumber)
util.hotfix_ex(CS.SangvisGunStateController,'OnClickStateLableItem',mOnClickStateLableItem)