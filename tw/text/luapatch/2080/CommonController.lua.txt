local util = require 'xlua.util'
xlua.private_accessible(CS.CommonController)

local LoadBigPicHD = function(oldPic,handler)
	if oldPic ~= nil and not oldPic:isNull() then
		CS.CommonController.LoadBigPicHD(oldPic,handler);
	end
end

util.hotfix_ex(CS.CommonController,'LoadBigPicHD',LoadBigPicHD)


