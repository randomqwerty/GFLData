local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterTeamData)

local MergeTeamIntoDictTeam  = function(self)
	CS.GameData.dictTeam[10001] = self.mainTeamGun;
	fairy = self:GetFairy();
	if(fairy == nil) then
		--CS.GameData.dictTeamFairy[10001] = nil;
		CS.GameData.dictTeamFairy:Remove(10001);
	else
		CS.GameData.dictTeamFairy[10001] = fairy;
	end
    
end

util.hotfix_ex(CS.TheaterTeamData,'MergeTeamIntoDictTeam',MergeTeamIntoDictTeam)