local util = require 'xlua.util'
xlua.private_accessible(CS.NavigationItemStationController)

local InitGnaku= function(self)
	self:InitGnaku()
	self.texTime.gameObject:SetActive(false)
end

util.hotfix_ex(CS.NavigationItemStationController,'InitGnaku',InitGnaku)