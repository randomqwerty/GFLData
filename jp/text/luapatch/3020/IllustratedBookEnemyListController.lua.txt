local util = require 'xlua.util'
xlua.private_accessible(CS.IllustratedBookEnemyListController)
local tag = false;
local myShowAutoFormationEnemyList = function(self,gunTagsList,needBossList)
	tag = true;
    self:ShowAutoFormationEnemyList(gunTagsList,needBossList)
end
local myCreateCharacterList = function(self)
	self:CreateCharacterList()
	if tag then
		self.allBookSangvisGunInfo = self.captureBookSangvisGunInfo;
	end
	tag = false;
end
util.hotfix_ex(CS.IllustratedBookEnemyListController,'ShowAutoFormationEnemyList',myShowAutoFormationEnemyList)
util.hotfix_ex(CS.IllustratedBookEnemyListController,'CreateCharacterList',myCreateCharacterList)