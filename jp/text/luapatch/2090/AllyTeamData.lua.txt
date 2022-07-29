local util = require 'xlua.util'
xlua.private_accessible(CS.AllyTeam)

local sangvisTeam = function(self)
	if self._sangvisTeam ~= nil then
		for i=0,self._sangvisTeam.listGun.Count-1 do
			local gun = self._sangvisTeam.listGun[i];
			if gun ~= nil then
				gun.status = CS.GunStatus.mission;
			end
		end
	end
	return self.sangvisTeam;
end

local SetHp = function(self,jsonData)
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
		self.ally_guns = jsonData:GetValue("ally_guns"):ToJson();
		self.ally_sangvis = jsonData:GetValue("ally_sangvis"):ToJson();
	end
	self:SetHp(jsonData);
end
util.hotfix_ex(CS.AllyTeam,'get_sangvisTeam',sangvisTeam)
util.hotfix_ex(CS.AllyTeam,'SetHp',SetHp)


