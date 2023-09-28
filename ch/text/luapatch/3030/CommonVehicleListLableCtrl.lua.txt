local util = require 'xlua.util'
xlua.private_accessible(CS.CommonVehicleListLableCtrl)

local ShowEfficiencyUI = function(self)
	if CS.DeploymentUIController.Instance ~= nil then
		CS.DeploymentEffectivenessController.OpenVehicleUI(self.vehicle, CS.DeploymentUIController.Instance.transform);
	else
		local parent = CS.CommonController.MainCanvas.transform;
		CS.DeploymentEffectivenessController.OpenVehicleUI(self.vehicle, parent);
	end
end

function RequstVehicleQuickFinish(vehicle,label)
	local action = nil;
	for i=0,CS.GameData.listSquadFixAction.Count-1 do
		if CS.GameData.listSquadFixAction[i].vehicleId == vehicle.id then
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

function RequestVehicleQuick(vehicle,label)
	local costQuickNum = vehicle.vehicleInfo.costQuickFixNum;
	if CS.GameData.userInfo.quickReinforce < costQuickNum then
		local count = costQuickNum - CS.GameData.userInfo.quickReinforce;
		local package = CS.OneClickBuyPackage(CS.GoodType.gemToItem,4,count,1,10);
		CS.CommonController.ConfirmBox(CS.Data.GetLang(50014),function()
				RequstQuickFinish(vehicle,label);
		end,package);
		return;
	end
	RequstVehicleQuickFinish(vehicle,label);
end

local QucikFix = function(self)
	if self.vehicle.status == CS.VehicleStatus.fix then
		RequestVehicleQuick(self.vehicle,self);
		return;
	end
	self:QucikFix();
end

util.hotfix_ex(CS.CommonVehicleListLableCtrl,'ShowEfficiencyUI',ShowEfficiencyUI)
util.hotfix_ex(CS.CommonVehicleListLableCtrl,'QucikFix',QucikFix)

