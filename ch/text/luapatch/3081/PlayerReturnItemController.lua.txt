local util = require 'xlua.util'
xlua.private_accessible(CS.PlayerReturnItemController)


local LoadSpine = function(self)
	if self.skin_id >0 and not CS.System.String.IsNullOrEmpty(self.spineCode) then
		if string.sub(self.spineCode, -3) == "Mod" then
			print(self.spineCode)
    		self.spineCode = string.sub(self.spineCode, 1, -4)
			print(self.spineCode)
		end
	end
	self:LoadSpine()
end
util.hotfix_ex(CS.PlayerReturnItemController,'LoadSpine',LoadSpine)