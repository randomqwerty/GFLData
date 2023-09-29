local util = require 'xlua.util'
xlua.private_accessible(CS.RequestAllyReinforce)

local RequestAllyReinforce = function(self,allyteam,spotId)
	self.allyTeam = allyteam;
	self.sb = CS.System.Text.StringBuilder();
	local writer = CS.LitJson.JsonWriter(self.sb);
	writer:WriteObjectStart();
	writer:WritePropertyName("ally_team_id");
	writer:Write(allyteam.allyTeamInfo.id);
	writer:WritePropertyName("spot_id");
	writer:Write(spotId);
	writer:WritePropertyName("myside_data");
	writer:WriteObjectStart();
	writer:WritePropertyName("sangvis");
	if allyteam.sangvisTeam ~= nil and allyteam.FriendAllyGuns ~= nil then
		writer:WriteObjectStart();
		for i=0,allyteam.FriendAllyGuns.listGun.Count-1 do
			local gun = allyteam.FriendAllyGuns.listGun[i];
			writer:WritePropertyName(tostring(gun.location));
			writer:WriteObjectStart();
			writer:WritePropertyName("edit_type");
			if gun.allySangvisCfg == nil then
				writer:Write(1);
			else
				writer:Write(2);
			end
			writer:WritePropertyName("id");
			if gun.allySangvisCfg == nil then
				writer:Write(gun.id);
			else
				writer:Write(gun.allySangvisCfg.id);
			end
			writer:WritePropertyName("position");
			writer:Write(gun.pos:ToId(CS.GF.Battle.GridPos.GridType.grid5x5));
			writer:WriteObjectEnd();
		end
		writer:WriteObjectEnd();
	else
		writer:WriteArrayStart();
		writer:WriteArrayEnd();
	end
	writer:WritePropertyName("gun");
	if allyteam.sangvisTeam == nil and allyteam.FriendAllyGuns ~= nil and allyteam.vehicleTeam == nil then
		writer:WriteObjectStart();
		for i=0,allyteam.FriendAllyGuns.listGun.Count-1 do
			local gun = allyteam.FriendAllyGuns.listGun[i];
			writer:WritePropertyName(tostring(gun.location));
			writer:WriteObjectStart();
			writer:WritePropertyName("edit_type");
			if gun.allyGunInfo == nil then
				writer:Write(1);
			else
				writer:Write(2);
			end
			writer:WritePropertyName("id");
			if gun.allyGunInfo == nil then
				writer:Write(gun.id);
			else
				writer:Write(gun.allyGunInfo.id);
			end
			writer:WritePropertyName("position");
			writer:Write(gun.pos:ToId());
			writer:WriteObjectEnd();
		end
		writer:WriteObjectEnd();
	else
		writer:WriteArrayStart();
		writer:WriteArrayEnd();
	end
	writer:WritePropertyName("fairy");
	if allyteam.currentFairy ~= nil then
		writer:WriteObjectStart();
		writer:WritePropertyName("edit_type");
		if allyteam.currentFairy.allyFairyCfg == nil then
			writer:Write(1);
		else
			writer:Write(2);
		end
		writer:WritePropertyName("id");
		if allyteam.currentFairy.allyFairyCfg == nil then
			writer:Write(allyteam.currentFairy.id);
		else
			writer:Write(allyteam.currentFairy.allyFairyCfg.id);
		end
		writer:WriteObjectEnd();
	else
		writer:WriteArrayStart();
		writer:WriteArrayEnd();
	end
	writer:WritePropertyName("squad");
	if allyteam.friendSquadTeam ~= nil then
		writer:WriteObjectStart();
		writer:WritePropertyName("edit_type");
		if allyteam.friendSquadTeam.squadData.allySquadCfg == nil then
			writer:Write(1);
		else
			writer:Write(2);
		end
		writer:WritePropertyName("id");
		if allyteam.friendSquadTeam.squadData.allySquadCfg == nil then
			writer:Write(allyteam.friendSquadTeam.squadData.id);
		else
			writer:Write(allyteam.friendSquadTeam.squadData.allySquadCfg.id);
		end
		writer:WriteObjectEnd();
	else
		writer:WriteArrayStart();
		writer:WriteArrayEnd();
	end
	writer:WritePropertyName("vehicle");
	if allyteam.vehicleTeam ~= nil then
		writer:WriteObjectStart();
		writer:WritePropertyName("edit_type");
		if allyteam.vehicleTeam.vehicle.allyVehicleCfg == nil then
			writer:Write(1);
		else
			writer:Write(2);
		end
		writer:WritePropertyName("id");
		if allyteam.vehicleTeam.vehicle.allyVehicleCfg == nil then
			writer:Write(allyteam.vehicleTeam.vehicle.id);
		else
			writer:Write(allyteam.vehicleTeam.vehicle.allyVehicleCfg.id);
		end
		writer:WriteObjectEnd();
	else
		writer:WriteArrayStart();
		writer:WriteArrayEnd();
	end
	writer:WriteObjectEnd();
	writer:WriteObjectEnd();
end


util.hotfix_ex(CS.RequestAllyReinforce,'.ctor',RequestAllyReinforce)

