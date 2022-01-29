local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUIDefenseTrialTeamSelectionController)
xlua.private_accessible(CS.BattleUIDefenseTrialTeamLabelController)

local InitData_New = function(self, ...)
	self:InitData(...)
	
	local team = CS.GameData.dictTeam[self.defaultTeamId]
	if team ~= nil and team.CostRes ~= nil then
		for i = 0, CS.GameData.defenseTrialAction.teamIds.Length - 1 do
			local tmpId = CS.GameData.defenseTrialAction.teamIds[i]
			if CS.GameData.dictTeam[tmpId].CostRes == nil then
				self.defaultTeamId = tmpId
				break
			end
		end
	end	

    self:SetToggleStateByTeamId(self.defaultTeamId);
end

local SetToggleStateByTeamId_New = function(self, id)
	if id == 0 then
		local exist = self.listTeamLabels:Exists(
			function ( s )
				return s.teamId == self.selectedTeamId
			end)
		if exist then
			id = self.selectedTeamId
		else
			for i = 0, self.listTeamLabels.Count -1 do
				if self.listTeamLabels[i].teamId ~= 0 then
					id = self.listTeamLabels[i].teamId
					break
				end
			end
		end
	end

	for i = 0, self.listTeamLabels.Count -1 do
		self.listTeamLabels[i]:SetState(self.listTeamLabels[i].teamId == id and id ~= 0)		
	end
	self.selectedTeamId = id
end

local ClearData_New = function(self)
	self:ClearData()
	self.teamId = 0
end

local InitDataLabel_New = function(self, index, teamId, ...)
    self.toggleIndex = index
    self:ClearData()

    if teamId ~= 0 then
    	if CS.GameData.dictTeam[teamId].CostRes ~= nil then
    		self.teamId = 0
    		--铁血梯队
    		return
    	end
    end
	
	self:InitData(index, teamId, ...)
	if self.listIcon.Count == 0 then
		self.teamId = 0
	end
end

util.hotfix_ex(CS.BattleUIDefenseTrialTeamSelectionController,'InitData',InitData_New)
util.hotfix_ex(CS.BattleUIDefenseTrialTeamSelectionController,'SetToggleStateByTeamId',SetToggleStateByTeamId_New)
util.hotfix_ex(CS.BattleUIDefenseTrialTeamLabelController,'ClearData',ClearData_New)
util.hotfix_ex(CS.BattleUIDefenseTrialTeamLabelController,'InitData',InitDataLabel_New)



