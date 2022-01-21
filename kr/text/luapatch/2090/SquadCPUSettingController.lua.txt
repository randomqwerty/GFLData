local util = require 'xlua.util'
xlua.private_accessible(CS.SquadCPUSettingController)
local chipinfo = {}
local cancelled = false
local CalcChip = function(self,selectedChips)
	cancelled = false
	if selectedChips.Count <= 5 then
		CS.GF.SquadChipCalculator.SquadChipCalculator.Instance.mode = CS.GF.SquadChipCalculator.ChipCalculatorMode.DLXBasic
	end
	self:CalcChip(selectedChips)
	for i=0, CS.GameData.listSquadChip.Count-1 do
		if CS.GameData.listSquadChip:GetDataByIndex(i).tempSquadId == CS.SquadChipListController.Instance.currentSquad.id then
			CS.GameData.listSquadChip:GetDataByIndex(i).tempSquadId = 0
		end
	end
end
local SetAutoChipAbout = function(self)
	cancelled = true
	self.autoChipFlag = true
	self.chipStates:Clear()
	
end

util.hotfix_ex(CS.SquadCPUSettingController,'CalcChip',CalcChip)
util.hotfix_ex(CS.SquadCPUSettingController,'SetAutoChipAbout',SetAutoChipAbout)
