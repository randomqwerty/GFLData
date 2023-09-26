local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEffectivenessController)

local VehicleCondition2_Crew2Base = function(self)
	if self.vehicle.vehicleCrewsArr.Length <= 1 then
		self.conditionVehicle2:Find("TypeScroll/TypeList/TypeCard2").gameObject:SetActive(false);
		return true;
	end
	return self:VehicleCondition2_Crew2Base();
end
local VehicleCondition2_Crew3Base = function(self)
	if self.vehicle.vehicleCrewsArr.Length <= 2 then
		self.conditionVehicle2:Find("TypeScroll/TypeList/TypeCard3").gameObject:SetActive(false);
		return true;
	end
	return self:VehicleCondition2_Crew3Base();
end
local VehicleCondition2_Crew4Base = function(self)
	if self.vehicle.vehicleCrewsArr.Length <= 3 then
		self.conditionVehicle2:Find("TypeScroll/TypeList/TypeCard4").gameObject:SetActive(false);
		return true;
	end
	return self:VehicleCondition2_Crew4Base();
end
local VehicleCondition3_Crew2 = function(self)
	if self.vehicle.vehicleCrewsArr.Length <= 1 then
		self.conditionVehicle3:Find("TypeScroll/TypeList/TypeCard2").gameObject:SetActive(false);
		return true;
	end
	local txt = self.conditionVehicle3:Find("TypeScroll/TypeList/TypeCard2/Img_Finish/Tex_TypeContent");
	txt:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(100318);
	return self:VehicleCondition3_Crew2();
end
local VehicleCondition3_Crew3 = function(self)
	if self.vehicle.vehicleCrewsArr.Length <= 2 then
		self.conditionVehicle3:Find("TypeScroll/TypeList/TypeCard3").gameObject:SetActive(false);
		return true;
	end
	return self:VehicleCondition3_Crew3();
end
local VehicleCondition3_Crew4 = function(self)
	if self.vehicle.vehicleCrewsArr.Length <= 3 then
		self.conditionVehicle3:Find("TypeScroll/TypeList/TypeCard4").gameObject:SetActive(false);
		return true;
	end
	return self:VehicleCondition3_Crew4();
end
local CheckSquadEfficiency = function(self)
	for i=0,self.LVParent.childCount-1 do
		self.LVParent:GetChild(i).gameObject:SetActive(false);
	end
	local effect = self.squad:GetCurrentEfficiency();
	if self.fitsuggest then
		effect = effect +1;
	end
	self.LVParent:GetChild(effect).gameObject:SetActive(true);
	if effect> 1 then
		effect = effect -5;
	end
	self.LVText.text = tostring(effect);
end
local GotoStroeRoomVehicle = function(self)
	if CS.Utility.loadedLevelName == "StoreRoom" then
		self:CloseUI();
		return;
	end
	self:GotoStroeRoomVehicle();
end

local SqaudCondition1_FullResolution = function(self)
	local finish = self:SqaudCondition1_FullResolution();
	local jump = self.conditionSquad1:Find("TypeScroll/TypeList/TypeCard1/Btn_Jump"):GetComponent(typeof(CS.ExButton));
	jump.onClick:RemoveAllListeners();
	jump:AddOnClick(function()
		if CS.Utility.loadedLevelName == "StoreRoom" then
			self:CloseUI();
			return;
		end
		CS.CommonController.GotoScene("StoreRoom", -15);
	end);
	return finish;
end
local SqaudCondition2_FullAndvance = function(self)
	local finish = self:SqaudCondition2_FullAndvance();
	local jump = self.conditionSquad2:Find("TypeScroll/TypeList/TypeCard1/Btn_Jump"):GetComponent(typeof(CS.ExButton));
	jump.onClick:RemoveAllListeners();
	jump:AddOnClick(function()
			if CS.Utility.loadedLevelName == "StoreRoom" then
				self:CloseUI();
				return;
			end
			CS.CommonController.GotoScene("StoreRoom", -15);
		end);
	return finish;
end
local SqaudCondition3_FullSkill = function(self)
	local finish = self:SqaudCondition3_FullSkill();
	local jump = self.conditionSquad3:Find("TypeScroll/TypeList/TypeCard1/Btn_Jump"):GetComponent(typeof(CS.ExButton));
	jump.onClick:RemoveAllListeners();
	jump:AddOnClick(function()
			if CS.Utility.loadedLevelName == "StoreRoom" then
				self:CloseUI();
				return;
			end
			CS.CommonController.GotoScene("StoreRoom", -15);
		end);
	return finish;
end
local SqaudCondition4_ChipOn = function(self)
	local finish = self:SqaudCondition4_ChipOn();
	local jump = self.conditionSquad4:Find("TypeScroll/TypeList/TypeCard1/Btn_Jump"):GetComponent(typeof(CS.ExButton));
	jump.onClick:RemoveAllListeners();
	jump:AddOnClick(function()
			if CS.Utility.loadedLevelName == "StoreRoom" then
				self:CloseUI();
				return;
			end
			CS.CommonController.GotoScene("StoreRoom", -15);
		end);
	return finish;
end
local SqaudCondition5_ChipFull = function(self)
	local finish = self:SqaudCondition5_ChipFull();
	local jump = self.conditionSquad5:Find("TypeScroll/TypeList/TypeCard1/Btn_Jump"):GetComponent(typeof(CS.ExButton));
	jump.onClick:RemoveAllListeners();
	jump:AddOnClick(function()
			if CS.Utility.loadedLevelName == "StoreRoom" then
				self:CloseUI();
				return;
			end
			CS.CommonController.GotoScene("StoreRoom", -15);
		end);
	return finish;
end
util.hotfix_ex(CS.DeploymentEffectivenessController,'VehicleCondition2_Crew2Base',VehicleCondition2_Crew2Base)
util.hotfix_ex(CS.DeploymentEffectivenessController,'VehicleCondition2_Crew3Base',VehicleCondition2_Crew3Base)
util.hotfix_ex(CS.DeploymentEffectivenessController,'VehicleCondition2_Crew4Base',VehicleCondition2_Crew4Base)
util.hotfix_ex(CS.DeploymentEffectivenessController,'VehicleCondition3_Crew2',VehicleCondition3_Crew2)
util.hotfix_ex(CS.DeploymentEffectivenessController,'VehicleCondition3_Crew3',VehicleCondition3_Crew3)
util.hotfix_ex(CS.DeploymentEffectivenessController,'VehicleCondition3_Crew4',VehicleCondition3_Crew4)
util.hotfix_ex(CS.DeploymentEffectivenessController,'CheckSquadEfficiency',CheckSquadEfficiency)
util.hotfix_ex(CS.DeploymentEffectivenessController,'GotoStroeRoomVehicle',GotoStroeRoomVehicle)
util.hotfix_ex(CS.DeploymentEffectivenessController,'SqaudCondition1_FullResolution',SqaudCondition1_FullResolution)
util.hotfix_ex(CS.DeploymentEffectivenessController,'SqaudCondition2_FullAndvance',SqaudCondition2_FullAndvance)
util.hotfix_ex(CS.DeploymentEffectivenessController,'SqaudCondition3_FullSkill',SqaudCondition3_FullSkill)
util.hotfix_ex(CS.DeploymentEffectivenessController,'SqaudCondition4_ChipOn',SqaudCondition4_ChipOn)
util.hotfix_ex(CS.DeploymentEffectivenessController,'SqaudCondition5_ChipFull',SqaudCondition5_ChipFull)