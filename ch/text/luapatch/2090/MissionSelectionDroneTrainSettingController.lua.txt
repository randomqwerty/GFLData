local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionDroneTrainSettingController)

local RefreshCollectionShow = function(self)
	self:RefreshCollectionShow();
	local id = self.TargetTraindata:GetEnemyTeamID();
	if id >0 then
		local enemyTeamInfo = CS.GameData.listEnemyTeamInfo:GetDataById(id);
		if enemyTeamInfo.effect_ext<0 then
			local effect = CS.Mathf.CeilToInt(CS.Mathf.Abs(enemyTeamInfo.effect_ext));
			self.TextEnemyPower.text = tostring(effect);
		end
	end
end

util.hotfix_ex(CS.MissionSelectionDroneTrainSettingController,'RefreshCollectionShow',RefreshCollectionShow)



