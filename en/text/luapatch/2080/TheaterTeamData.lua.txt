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

local ReplaceTeamByTeamId= function(self,teamid)
	self:ReplaceTeamByTeamId(teamid);
	if self._isSangvis then
		for i=1,9 do
			local gunCopy;
			if self.mainTeamGun.dictLocation:ContainsKey(i) then
				gunCopy = self.mainTeamGun.dictLocation[i];
			end
			if(gunCopy ~= nil and gunCopy:IsLeader()) then
				for k,v in pairs(self.dictTeamSquad) do
					if v~=nil and v.id == gunCopy.id then 
						self:RemoveMainTeamGun(gunCopy);
					   break;
					end
			   end
			end
			
		end
	end
end

util.hotfix_ex(CS.TheaterTeamData,'MergeTeamIntoDictTeam',MergeTeamIntoDictTeam)
util.hotfix_ex(CS.TheaterTeamData,'ReplaceTeamByTeamId',ReplaceTeamByTeamId)