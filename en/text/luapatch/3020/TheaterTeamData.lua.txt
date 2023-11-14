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
util.hotfix_ex(CS.TheaterTeamData,'CheckSquadValid',_CheckSquadValid)