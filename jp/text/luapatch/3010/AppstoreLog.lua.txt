local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
local myCheckRepeatingFixAndOperation = function(self)
    self:CheckRepeatingFixAndOperation();
	local goodStr = CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent')	
	if(CS.System.String.IsNullOrEmpty(goodStr) == false) then	    
		self:AddiOSEvent();		
	end
end

util.hotfix_ex(CS.HomeController,'CheckRepeatingFixAndOperation',myCheckRepeatingFixAndOperation)