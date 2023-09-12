local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSquadListLabelController)
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.DeploymentSquadListInfoController)
xlua.private_accessible(CS.TheaterSquadListContainer)
xlua.private_accessible(CS.TargetTrainSquadListContainer)

local myChoose = function(self,choose)
	if CS.DeploymentTeamInfoController.Instance ~= nil then
		self:Choose(choose)
	else
		self.select = choose;
		self:ChangeSelectStatus(choose);
		CS.CommonAudioController.PlayUI(CS.AudioUI.UI_selete);
		if (CS.DeploymentSquadListInfoController.Instance ~= nil) then
			CS.DeploymentSquadListInfoController.Instance.currentSelectSquad = self;
		end
		if CS.TheaterSquadListContainer.Instance ~= nil then
			CS.TheaterSquadListContainer.Instance:SelectSquad(self.squad);
		end
		if CS.TargetTrainSquadListContainer.Instance ~= nil then
			CS.TargetTrainSquadListContainer.Instance:SelectSquad(self.squad);
		end
	end
end
util.hotfix_ex(CS.CommonSquadListLabelController,'Choose',myChoose)