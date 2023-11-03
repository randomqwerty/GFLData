local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterMissiontSettlementController)

local InitData = function(self,result)
	self:InitData(result);
	local tween = self.picHolder:GetComponent(typeof(CS.TweenPosition));
	tween.Rememberform = false;
	tween.from = CS.UnityEngine.Vector3(820,320,0);
end


util.hotfix_ex(CS.TheaterMissiontSettlementController,'InitData',InitData)