local util = require 'xlua.util'
xlua.private_accessible(CS.FormationController)

local useteamrecord = false;
local ShowApplyTeamRecord = function(self,teamRecord)
	useteamrecord = true;
	self:ShowApplyTeamRecord(teamRecord);
end

local RequestChangeTeamTotal = function(self,force)
	if useteamrecord then
		CS.FormationController.forceReplace = force;
		local createConnection = xlua.get_generic_method(CS.ConnectionController, 'CreateConnection');
		local createRequest = createConnection(CS.RequestApplyTeamRecord);
		createRequest(CS.RequestApplyTeamRecord(self.currentSelectedTeam, self.teamRecord, force),function(data)
				self:RequestChangeTeamTotalHandle(data);
			end);
		useteamrecord = false;
	else
		self:RequestChangeTeamTotal(force);
	end
end

local RequestChangeTeamTotalHandle = function(self,request)
	self:RequestChangeTeamTotalHandle(request);
	if CS.FormationSettingController.Instance ~= nil and CS.FormationSettingController.Instance.gameObject.activeInHierarchy then
		CS.FormationSettingController.Instance:OnClickOK();
	end
end
util.hotfix_ex(CS.FormationController,'ShowApplyTeamRecord',ShowApplyTeamRecord)
util.hotfix_ex(CS.FormationController,'RequestChangeTeamTotal',RequestChangeTeamTotal)
util.hotfix_ex(CS.FormationController,'RequestChangeTeamTotalHandle',RequestChangeTeamTotalHandle)