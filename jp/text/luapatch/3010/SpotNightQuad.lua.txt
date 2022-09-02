local util = require 'xlua.util'
xlua.private_accessible(CS.SpotNightQuad)

local Awake = function(self)
	self:Awake();
	self.transform.localPosition = CS.UnityEngine.Vector3(0,0,50);
end

util.hotfix_ex(CS.SpotNightQuad,'Awake',Awake)




