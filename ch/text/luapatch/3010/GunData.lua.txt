local util = require 'xlua.util'
xlua.private_accessible(CS.GunInfo)

local _CheckSkinIdCanShowDamage = function(self,s_id)

	if CS.System.String.IsNullOrEmpty(self.show_damage_skin) then
		return false;
	else
		local s=","..s_id..",";
		--print(s);
		--print(self.show_damage_skin);
		return self.show_damage_skin:find(s);
	end 
end

util.hotfix_ex(CS.GunInfo,'CheckSkinIdCanShowDamage',_CheckSkinIdCanShowDamage)



