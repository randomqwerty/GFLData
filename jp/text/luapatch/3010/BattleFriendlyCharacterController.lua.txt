local util = require 'xlua.util'
xlua.private_accessible(CS.BattleFriendlyCharacterController)
local OpenCollider = function(self)

	self:OpenCollider()
	local t = self.Pos.y
	local height = 1.3
	if t == 0 then
		
	else
		if t == 1 then
			height = 1.8
		else
			height = 2
		end
	end
	for i=0,self.listCollider.Count-1 do
		if self.listCollider[i] ~= nil then
			self.listCollider[i].center = CS.UnityEngine.Vector3(0, 0.1 + height / 2, 0);
			self.listCollider[i].size = CS.UnityEngine.Vector3(1, height, 0.1);
		end
	end

end

util.hotfix_ex(CS.BattleFriendlyCharacterController,'OpenCollider',OpenCollider)