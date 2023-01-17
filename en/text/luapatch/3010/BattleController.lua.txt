local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.TheaterEchelonSelection)
xlua.private_accessible(CS.TheaterEchelonSelectionEnemyUIController)

local GetDayNight = function(self)
	if self.EntranceType == CS.BattleEntranceType.BattlePreview then
		if CS.TheaterEchelonSelection.Instance ~= nil and CS.TheaterEchelonSelection.Instance.enemyUI~=nil then
			local t=CS.TheaterEchelonSelection.Instance.enemyUI
			return t.areaInfo:GetMapSpecialType(t.mCurrentEnemyGroupId) == CS.MapSpecialType.Night
		end
	end
	return self:GetDayNight()

end
local CreateBackground = function(self,name)
	
	
	if self.EntranceType == CS.BattleEntranceType.Normal and (self.enemyTeamidUse == 6560401 or self.enemyTeamidUse == 6561401) then
		self:CreateBackground("scarbossbattle")
		CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/2022ScarBattle"))
	else
		
		self:CreateBackground(name)
		if self.EntranceType == CS.BattleEntranceType.Normal and self.enemyTeamidUse == 590000 then
			CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2023RougeSpring_BossTimer"))
			CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2023RougeSpring_BossSettle"))
		end
	end
	
end

util.hotfix_ex(CS.GF.Battle.BattleController,'GetDayNight',GetDayNight)
util.hotfix_ex(CS.GF.Battle.BattleController,'CreateBackground',CreateBackground)