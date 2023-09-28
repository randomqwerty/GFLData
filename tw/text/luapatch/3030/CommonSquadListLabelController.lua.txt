local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSquadListLabelController)

local ShowEfficiencyUI = function(self)
	if CS.DeploymentUIController.Instance ~= nil then
		CS.DeploymentEffectivenessController.OpenSquadUI(self.squad, CS.DeploymentUIController.Instance.transform);
	else
		local parent = CS.CommonController.MainCanvas.transform;
		CS.DeploymentEffectivenessController.OpenSquadUI(self.squad, parent);
	end
end

local Awake = function(self)
	self:Awake();
	local list = self.transform:Find("List");
	list:SetAsLastSibling();
end

function RequstSquadQuickFinish(squad,label)
	local action = nil;
	for i=0,CS.GameData.listSquadFixAction.Count-1 do
		if CS.GameData.listSquadFixAction[i].squadId == squad.id then
			action = CS.GameData.listSquadFixAction[i];
		end
	end
	if action ~= nil then
		local createConnection = xlua.get_generic_method(CS.ConnectionController, 'CreateConnection');
		local createRequest = createConnection(CS.RequestVehicleFinishFix);
		createRequest(CS.RequestVehicleFinishFix(action, 1),function(data)
				label:RefreshUI();
			end);
	end
end

function RequestSquadQuick(squad,label)
	local costQuickNum = squad.info.costQuickFixNum;
	if CS.GameData.userInfo.quickReinforce < costQuickNum then
		local count = costQuickNum - CS.GameData.userInfo.quickReinforce;
		local package = CS.OneClickBuyPackage(CS.GoodType.gemToItem,4,count,1,10);
		CS.CommonController.ConfirmBox(CS.Data.GetLang(50014),function()
				RequstSquadQuickFinish(squad,label);
			end,package);
		return;
	end
	local text = CS.System.String.Format(CS.Data.GetLang(50015), costQuickNum);
	CS.CommonController.ConfirmBox(text,function()
			RequstSquadQuickFinish(squad,label);
		end);
end

local QucikFix = function(self)
	if self.squad.status == CS.SquadStatus.fix then
		RequestSquadQuick(self.squad,self);
		return;
	end
	self:QucikFix();
end

util.hotfix_ex(CS.CommonSquadListLabelController,'ShowEfficiencyUI',ShowEfficiencyUI)
util.hotfix_ex(CS.CommonSquadListLabelController,'Awake',Awake)
util.hotfix_ex(CS.CommonSquadListLabelController,'QucikFix',QucikFix)
