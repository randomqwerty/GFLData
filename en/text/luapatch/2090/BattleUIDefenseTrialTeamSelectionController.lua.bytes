local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUIDefenseTrialTeamSelectionController)
xlua.private_accessible(CS.BattleUIDefenseTrialTeamLabelController)

local InitData_New = function(self, ...)
	self:InitData(...)
	
	local teamCount = GetAvalableTeamCount()
	for i=0, 3 do
		if self:GetTeamLabelByIndex(i).btnChangeTeam.gameObject.activeSelf then
        	self:GetTeamLabelByIndex(i):ShowChangeTeam(i < teamCount)
    	end
    end
end

GetAvalableTeamCount = function()
	local count = 0
    for i = 1, CS.GameData.userInfo.maxTeam do
        local listGun = CS.GameData.listGun:FindAll(
				function(s)
					return s.teamId == i
				end);

        if listGun.Count > 0 then
                --看血量和状态是否符合
            local tempList = listGun:FindAll(
            	function (s)
            		return s.status == CS.GunStatus.normal and s.life > 0
            	end);

            if tempList.Count == listGun.Count then
                if CS.GameData.dictTeam[i].Fairy == nil or CS.GameData.dictTeam[i].Fairy.status == CS.FairyStatus.inTeam then--排除梯队内有正在训练的妖精
                    count = count + 1
                end
            end            
        end
    end
    
    return count
end


util.hotfix_ex(CS.BattleUIDefenseTrialTeamSelectionController,'InitData',InitData_New)
