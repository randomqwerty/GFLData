local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterBattleTeamSelectionUIController)

local _CreateSquadList = function(self)
	for i=0,self.listTeamSquadUIItem.Count-1 do
		CS.UnityEngine.Object.Destroy(self.listTeamSquadUIItem[i].gameObject)
	end
	self.listTeamSquadUIItem:Clear();
	self:CreateSquadList();
	
end


util.hotfix_ex(CS.TheaterBattleTeamSelectionUIController,'CreateSquadList',_CreateSquadList)