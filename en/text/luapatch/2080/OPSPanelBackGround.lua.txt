local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelBackGround)

local OnPointerUp = function(self,eventData)
	if self.isDrag then
		return;
	end
	if CS.OPSPanelBackGround.currentContainerId ~= 0 and CS.OPSPanelController.Instance.currentPanelConfig.ContainerClockInfos:ContainsKey(CS.OPSPanelBackGround.currentContainerId) then				
		CS.OPSPanelController.Instance:ReturnContainer();
		return;
	end
	CS.OPSPanelController.Instance:CancelMission();	
end

local OpenBackgroundClick = function()
	CS.OPSPanelBackGround.Instance:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = true;
end

local MoveClockContainer = function(self,container,play)
	self:MoveClockContainer(container,play);
	CS.CommonController.Invoke(OpenBackgroundClick,0.8,CS.OPSPanelController.Instance);
end

local ReadRecord = function(self)
	if CS.OPSPanelController.Instance.campaionId == -48 and CS.OPSPanelBackGround.currentContainerId == 0 then
		return false;
	end
	return self:ReadRecord();
end
local SaveRecord = function(self)
	if not self.pointerDown then
		return;
	end
	self:SaveRecord();
end
util.hotfix_ex(CS.OPSPanelBackGround,'MoveClockContainer',MoveClockContainer)
util.hotfix_ex(CS.OPSPanelBackGround,'OnPointerUp',OnPointerUp)
util.hotfix_ex(CS.OPSPanelBackGround,'ReadRecord',ReadRecord)
util.hotfix_ex(CS.OPSPanelBackGround,'SaveRecord',SaveRecord)


