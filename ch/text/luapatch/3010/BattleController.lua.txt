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

util.hotfix_ex(CS.GF.Battle.BattleController,'GetDayNight',GetDayNight)