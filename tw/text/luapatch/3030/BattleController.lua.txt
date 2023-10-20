local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleMemberData)
local FP = CS.TrueSync.FP
local GetBoneLocalPos = function(self,curFrame,boneName)
	local characterdata =  self.parentData
	if characterdata.isVehicleComponent or characterdata.isVehicle then
		print(characterdata.switchDistance)
		return self:GetBoneLocalPos(curFrame,boneName) * characterdata.switchDistance
	else
		return self:GetBoneLocalPos(curFrame,boneName)
	end
end
local Scout = function(self)
	local range = self.data.realtimeRange:AsFloat()
	if range <= 30 then
		return
	end
	self:Scout()
end
local DeathClear = function(self)
	
	self:DeathClear()
end
local CreateFriendlyCharacter = function(self)
	
	local v = self:CreateFriendlyCharacter()
	--if CS.GF.Battle.BattleDynamicData.isVehicleBattle then
	--	util.hotfix_ex(CS.GF.Battle.BattleMemberData,'GetBoneLocalPos',GetBoneLocalPos)
	--else
	--	xlua.hotfix(CS.GF.Battle.BattleMemberData,'GetBoneLocalPos',nil)
	--end
	if CS.GF.Battle.BattleDynamicData.isRemoteBattle then
		util.hotfix_ex(CS.GF.Battle.BattleEnemyCharacterManager,'Scout',Scout)
	else
		xlua.hotfix(CS.GF.Battle.BattleEnemyCharacterManager,'Scout',nil)
	end
	if self.EntranceType == CS.BattleEntranceType.Theater then
		util.hotfix_ex(CS.GF.Battle.BattleCharacterManager,'DeathClear',DeathClear)
	else
		xlua.hotfix(CS.GF.Battle.BattleCharacterManager,'DeathClear',nil)
	end
	
	self.transform:Find("Canvas/DynamicCanvas/DPS").localPosition = CS.UnityEngine.Vector3(807,296.6,60)
	return v
end

local NeedShowVehicleForwardBtn = function(self)
	local fp2 = FP.FromFloat(1.5)
	self.nearEnemyDistance = self.nearEnemyDistance - fp2
	local ans = self:NeedShowVehicleForwardBtn()
	self.nearEnemyDistance = self.nearEnemyDistance + fp2
	return ans
end

local CloseDeploymentMoni = function()
	if CS.GF.Battle.BattleController.renderTexture ~= nil then
		CS.GF.Battle.BattleController.renderTexture:Release();
	end
	CS.GF.Battle.BattleController.CloseDeploymentMoni();
end

local CheckTheaterEnemyTypeNum = function(self)
	self.DictEnemyTypeDieTimeStatistic = CS.GF.Battle.BattleDynamicData.DictEnemyTypeDieTimeStatistic
end

util.hotfix_ex(CS.GF.Battle.BattleController,'CreateFriendlyCharacter',CreateFriendlyCharacter)
util.hotfix_ex(CS.GF.Battle.BattleController,'NeedShowVehicleForwardBtn',NeedShowVehicleForwardBtn)
util.hotfix_ex(CS.GF.Battle.BattleController,'CloseDeploymentMoni',CloseDeploymentMoni)
util.hotfix_ex(CS.GF.Battle.BattleController,'CheckTheaterEnemyTypeNum',CheckTheaterEnemyTypeNum)
