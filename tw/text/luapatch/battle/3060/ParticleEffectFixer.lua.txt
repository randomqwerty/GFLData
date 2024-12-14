local util = require 'xlua.util'

Update = function()
	if not float_equal(self.transform.eulerAngles.z,0) then
		--print("Before"..self.transform.eulerAngles.x.." "..self.transform.eulerAngles.y.." "..self.transform.eulerAngles.z)
		self.transform.eulerAngles = CS.UnityEngine.Vector3(self.transform.eulerAngles.x,-self.transform.eulerAngles.z,0)
		--print("After"..self.transform.eulerAngles.x.." "..self.transform.eulerAngles.y.." "..self.transform.eulerAngles.z)
	end
end
function float_equal(lhs, rhs)
	local abs= math.abs
	return abs(lhs - rhs) <= 0.1
end
--depose
OnDestroy =function()

end

