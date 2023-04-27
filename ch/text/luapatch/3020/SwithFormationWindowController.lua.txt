local util = require 'xlua.util'
xlua.private_accessible(CS.SwithFormationWindowController)
local myInitWithGun = function(self,gunData,gunList,gunPosMap)
	local t = {}
	local c = 1;
	for i = 0, gunList.Count - 1 do
		for j = gunList.Count - 1, i + 1, -1 do
			if gunList[i].info.id == (gunList[j].info.id - 20000) then
				t[c] = gunList[j].id;
				c = c+1;
			end
			if gunList[i].info.id == (gunList[j].info.id + 20000) then
				t[c] = gunList[j].id;
				c = c+1;
			end
		end
	end
	for i = 1, #t do
		gunPosMap:Remove(t[i]);
		gunList:RemoveAll(function (s)
				return s.id == t[i]
			end)
	end
    self:InitWithGun(gunData,gunList,gunPosMap)
end
util.hotfix_ex(CS.SwithFormationWindowController,'InitWithGun',myInitWithGun)