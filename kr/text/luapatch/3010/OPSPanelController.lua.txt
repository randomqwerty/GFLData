local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.OPSConfig)
xlua.private_accessible(CS.OPSPanelBackGround)
xlua.private_accessible(CS.CommonSceneManagerController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ExButton)
xlua.private_accessible(CS.ResManager)
local ShowOPSSpineMissionUI = function(self,code)
	self:ShowOPSSpineMissionUI(code);
	if not self.moudleSpineUIObj.gameObject.activeInHierarchy then
		self.useOPSmissions:Clear();
		local trans = self.panalMissionTrans:GetEnumerator();
		while trans:MoveNext() do
			local key = trans.Current.Key;
			local value = trans.Current.Value;
			self:CheckOPSMissionItem(key,value);
			if value.gameObject.activeSelf then
				self.useOPSmissions:Add(key);
			end
		end
		self.num = self.useOPSmissions.Count;
		self.checkPosMax = self.currentPanelConfig.moudleSpineUI.selectPosX;
		self.distance = self.currentPanelConfig.moudleSpineUI.eachDistance;
		self.moudleSpineUIObj.gameObject:SetActive(true);
	end
end

local CanGetPoint = function(self,itemid)
	if CS.MissionSelectionController.normalActivityCampaion:Contains(self.campaionId) then
		return true;
	end
	return self:CanGetPoint(itemid);
end
local myLoadReturn = function(self)
	if (CS.OPSConfig.Instance.OPSCamapionReturn:ContainsKey(self.campaionId)) then
		return self:LoadReturn();
	else
		local Obj = CS.ResManager.GetObjectByPath(string.format("Pics/ActivityMap/%s", CS.OPSConfig.Instance.OPSReturn));
		if (Obj ~= nil) then
			local returnObject = CS.UnityEngine.Object.Instantiate(Obj):GetComponent(typeof(CS.ExButton));
			returnObject.transform:SetParent(self.Top, false);
			returnObject.transform:SetAsLastSibling();
			returnObject:AddOnClickBack(function ()
					CS.OPSPanelBackGround.Instance:SaveRecord();
					CS.CommonSceneManagerController.instance:PopController();
					CS.CommonController.GotoScene("MissionSelection");
			end);
		end
	end
end
util.hotfix_ex(CS.OPSPanelController,'ShowOPSSpineMissionUI',ShowOPSSpineMissionUI)
util.hotfix_ex(CS.OPSPanelController,'CanGetPoint',CanGetPoint)
util.hotfix_ex(CS.OPSPanelController,'LoadReturn',myLoadReturn)