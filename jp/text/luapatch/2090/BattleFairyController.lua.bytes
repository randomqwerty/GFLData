local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleFairyController)
--修复特定的妖精拿到的编制数目有问题 满足条件时给全场buff来判定编制数目
local skillid = 99910101
local SetFariy = function(self,fairy)
	self:SetFariy(fairy)
	if fairy.info.type ~=  CS.FairyInfo.Fake then
		if fairy.info.id == 4 or fairy.info.id == 29 then
			local cfg = CS.GameData.listBTSkillCfg:GetDataById(skillid)
			local friendlyCharacters = CS.GF.Battle.BattleController.Instance.friendlyTeamHolder:GetCharacters()
			for i=0,friendlyCharacters.Count-1 do
				local character = friendlyCharacters[i]
				if cfg ~= nil and character~=nil and character:isNull() == false and character.listMember[0]:isNull() == false and character:IsDead() == false then
					--产生技能所带的buff
					CS.GF.Battle.SkillUtils.GenBuff(
						CS.GF.Battle.BattleSkillCfgEx(cfg, false, nil, nil),
						character.listMember[0],
						cfg.buffSelf,
						cfg.buffSelfNum,
						character.gun.number
					)
				end
			end
			
			local enemyCharacters = CS.GF.Battle.BattleController.Instance.enemyTeamHolder:GetCharacters()
			for i=0,enemyCharacters.Count-1 do
				local character = enemyCharacters[i]
				if cfg ~= nil and character~=nil and character:isNull() == false and character.listMember[0]:isNull() == false and character:IsDead() == false then
					--产生技能所带的buff
					CS.GF.Battle.SkillUtils.GenBuff(
						CS.GF.Battle.BattleSkillCfgEx(cfg, false, nil, nil),
						character.listMember[0],
						cfg.buffSelf,
						cfg.buffSelfNum,
						character.gun.number
					)
				end
			end
		end
	end
	
end

util.hotfix_ex(CS.GF.Battle.BattleFairyController,'SetFariy',SetFariy)
