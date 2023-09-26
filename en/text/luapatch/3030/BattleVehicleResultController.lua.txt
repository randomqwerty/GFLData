local util = require 'xlua.util'

xlua.private_accessible(CS.BattleVehicleResultController)
local FP = CS.TrueSync.FP
local Init = function(self,jsondata,curSpot)

	self:Init(jsondata,curSpot)
	self:StopAllCoroutines()
	self:StartCoroutine(self:UpdateVehicleExp())
	self:StartCoroutine(self:ShowVehicleSpine())
	self:StartCoroutine(self:ShowCrewMember())
	self:StartCoroutine(self:ShowRank())
end

util.hotfix_ex(CS.BattleVehicleResultController,'Init',Init)