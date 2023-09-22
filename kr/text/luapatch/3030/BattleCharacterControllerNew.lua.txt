local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleCharacterControllerNew)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleMemberControllerNew)
local FP = CS.TrueSync.FP
local Init = function(self,data)

	self:Init(data)
	if(data.isVehicleComponent and data.slotid > 0) then
		data.vehicleOffset = data.vehicleOffset + CS.TrueSync.TSVector(0.75,0,0)
		data.vehicleOffset = data.vehicleOffset * FP.FromFloat(self.spineScale)
		data.vehicleOffset = data.vehicleOffset - CS.TrueSync.TSVector(0.75,0,0)
	end
	if(data.isVehicleComponent or data.isVehicle) then
		data.switchDistance = FP.FromFloat(self.spineScale)
	end
	if self.isCutin and data.summonData ~= nil and data.summonData.vehicle ~= nil then
		local member = self.gameObject:GetComponentInChildren(typeof(CS.GF.Battle.BattleMemberControllerNew))
		member.parent = self
		member:Init(data.listMemberData[0])
		self.listMembers:Add(member)
		self.gameObject.transform.localRotation = CS.UnityEngine.Quaternion.Euler(0,0,0)
	end
end
local AddEffectCollision = function(self)
	
	if CS.GF.Battle.BattleDynamicData.isVehicleBattle then
		self:AddEffectCollision()
	end
end
local OnSwitch = function(self,sender,e)
	if self.data.isSummon then
		return
	end
	self:OnSwitch(sender,e)
end
util.hotfix_ex(CS.GF.Battle.BattleCharacterControllerNew,'Init',Init)
util.hotfix_ex(CS.GF.Battle.BattleCharacterControllerNew,'AddEffectCollision',AddEffectCollision)
util.hotfix_ex(CS.GF.Battle.BattleCharacterControllerNew,'OnSwitch',OnSwitch)