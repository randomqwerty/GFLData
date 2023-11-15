local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterTeamData)

local _CheckSquadValid = function(self)
	self:CheckSquadValid();
	if self.mainTeamGun ~= nil and self._isSangvis then
		local sangvis = self.mainTeamGun.dictLocation[1];
		if sangvis ~= nil then
			local sa = CS.GameData.listSangvisGun:GetDataById(sangvis.id)
			local assistTeamId = self:GetSangvisAssistTeamId(sa);
			if assistTeamId > 0 then
				self:SetSquad(assistTeamId, nil);
			end
		end
	end
end

local ChangeLifeToOrigin = function(self)
	if not self.isSangvisTeam then
		local iter = self.dictOriginalLifeWithGwuId:GetEnumerator();
		while iter:MoveNext() do
			local id = iter.Current.Key;
			local hp = iter.Current.Value;
			local gun = CS.GameData.listGun:GetDataById(id);
			if gun ~= nil then
				gun.life = hp;
			end
		end
	else
		local iter = self.dictOriginalLifeWithGwuId:GetEnumerator();
		while iter:MoveNext() do
			local id = iter.Current.Key;
			local hp = iter.Current.Value;
			local gun = CS.GameData.listSangvisGun:GetDataById(id);
			if gun ~= nil then
				gun.life = hp;
			end
		end
	end
end
util.hotfix_ex(CS.TheaterTeamData,'CheckSquadValid',_CheckSquadValid)
util.hotfix_ex(CS.TheaterTeamData,'ChangeLifeToOrigin',ChangeLifeToOrigin)