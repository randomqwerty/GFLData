local util = require 'xlua.util'
xlua.private_accessible(CS.AutoFormationSangvisData)

local frontGunTags = function(self)
	if CS.System.String.IsNullOrEmpty(self.front_tag_ids) then
		return CS.System.Collections.Generic.List(CS.System.Collections.Generic.List(CS.GunTagInfo))();
	end
	return self.frontGunTags;
end

local backGunTags = function(self)	
	if CS.System.String.IsNullOrEmpty(self.back_tag_ids) then
		return CS.System.Collections.Generic.List(CS.System.Collections.Generic.List(CS.GunTagInfo))();
	end
	return self.backGunTags;
end

util.hotfix_ex(CS.AutoFormationSangvisData,'get_frontGunTags',frontGunTags)
util.hotfix_ex(CS.AutoFormationSangvisData,'get_backGunTags',backGunTags)
