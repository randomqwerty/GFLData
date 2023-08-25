local util = require 'xlua.util'
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.BattleManualSkillController)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleCharacterControllerNew)
xlua.private_accessible(CS.GF.Battle.BattleMemberControllerNew)
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleStatistics)
xlua.private_accessible(CS.GF.Battle.BattleFrameTimer)
xlua.private_accessible(CS.BattleUIPauseController)
xlua.private_accessible(CS.GF.Battle.BattleConditionList)
xlua.private_accessible(CS.GF.Battle.CharacterCondition)
xlua.private_accessible(CS.GF.Battle.EffectManager)
xlua.private_accessible(CS.GF.Battle.BattleFairyData)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
local TargetBuffID = 0
local TargetBuffID_A = 4097
local TargetBuffID_B = 4101
local TargetBuffID_C = 4102
local TargetBuffID_D = 4117
local TargetSkillID_A = 40621701
local TargetSkillID_B = 40621801
local TargetSkillID_C = 40621901
local TargetSkillID_Switch = 40622001
local character
local characterData
local trigger = false
--找到带Buff的人 然后把它举起来= =
Start = function()

	--local character = nil
	
end
Update = function()
	if not trigger  and Info.transform.position.x < 500 then
		local findFlag = false
		local Scale = Info.transform.localScale
		if Scale.x == 1 then
			TargetBuffID = TargetBuffID_A
		end
		if Scale.x == 2 then
			TargetBuffID = TargetBuffID_B
		end
		if Scale.x == 3 then
			TargetBuffID = TargetBuffID_C
		end
		if Scale.x == 4 then
			TargetBuffID = TargetBuffID_D
		end
		--print(Scale.x)
		local team = CS.GF.Battle.BattleController.Instance.listFriendlyCharacterControllers
		if team ~= nil then
			for i=0,team.Count-1 do
				character = team[i]
				local currentTier = nil
				local dutarion = nil
				currentTier,dutarion = character.data.conditionListSelf:GetTierByID(TargetBuffID)
				--print(character.gameObject.name.." "..TargetBuffID.." "..currentTier.." "..character.data.status:ToString())
				if currentTier ~= 0 then
					if (character.data.isSummon == false and character.data:CanBeFound()) and (character.data.status == CS.GF.Battle.CharacterStatus.fighting or character.data.status == CS.GF.Battle.CharacterStatus.standby) then
						if character.holder.localPosition.y == 0 then
							character.lifeBar.source = character.holder
							HandleFloat(character.holder)
							TriggerDestroy(character.data)
						end
						
					end
				end
			end
		end
		trigger = true
	end
	if Info.transform.position.x > 500 then
		trigger = false
	end
end
HandleFloat = function(trans)
	
	local seq = CS.DG.Tweening.DOTween.Sequence()
	seq:Append(trans:DOLocalMoveY(2.8,0.65))
	seq:Append(trans:DOLocalMoveY(2,0.6))
	seq:Append(trans:DOLocalMoveY(2.6,0.6))
	seq:Append(trans:DOLocalMoveY(2,0.55))
	seq:Append(trans:DOLocalMoveY(2.8,0.6))
	seq:Append(trans:DOLocalMoveY(0,0.25))


end

TriggerDestroy= function(character)
	local eulerAngles = Info.transform.localScale

	if eulerAngles.x == 1 then
		local cfg = CS.GameData.listBTSkillCfg:GetDataById(TargetSkillID_A)
		if cfg ~= nil and character~=nil and character.isDead == false then
			character:CastSkillUsingCfg(cfg)
			
		end
	end
	if eulerAngles.x == 2 then
		local cfg = CS.GameData.listBTSkillCfg:GetDataById(TargetSkillID_B)
		if cfg ~= nil and character~=nil and character.isDead == false then
			character:CastSkillUsingCfg(cfg)
		end
	end
	if eulerAngles.x == 3 then
		local cfg = CS.GameData.listBTSkillCfg:GetDataById(TargetSkillID_C)
		if cfg ~= nil and character~=nil and character.isDead == false then
			character:CastSkillUsingCfg(cfg)
		end
	end
	-- 这里把占位技能上给单位使得它无法换位
	local cfg = CS.GameData.listBTSkillCfg:GetDataById(TargetSkillID_Switch)
	if cfg ~= nil and character~=nil and character.isDead == false then
		--产生技能所带的buff
		character:CastSkillUsingCfg(cfg)	
	end
end
