local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterTeamData)

local ChangeLifeToOrigin = function(self)
	if not self.isSangvisTeam then
		local iter = self.dictOriginalLifeWithGwuId:GetEnumerator();
		while iter:MoveNext() do
			local id = iter.Current.Key;
			local hp = iter.Current.Value;
			local gun = CS.GameData.listGun:GetDataById(id);
			if gun ~= nil then
				gun.life = hp;
				if gun.status == CS.GunStatus.mission then
					gun.status = CS.GunStatus.normal;
				end
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
				if gun.status == CS.GunStatus.mission then
					gun.status = CS.GunStatus.normal;
				end
			end
		end
	end
end

util.hotfix_ex(CS.TheaterTeamData,'ChangeLifeToOrigin',ChangeLifeToOrigin)