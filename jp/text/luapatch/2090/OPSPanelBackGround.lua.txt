local util = require 'xlua.util'
local panelController = require("2090/OPSPanelController")
xlua.private_accessible(CS.OPSPanelBackGround)


local ResetClockContainer = function(self,play)
	if self.container ~= nil and not self.container:isNull() then
		local check = 1.0*self.container:ClearCount() / self.container:AllCount();
		local angle = CS.Mathf.Lerp(0, 180, check);
		CS.OPSPanelController.Instance.order_angle[self.container.id] = angle;
	end
	self:ResetClockContainer(play);
end

local Start = function(self)
	self:Start();
	self:UpdateScalePos();
	CS.CommonController.Invoke(function()
		self.oldscale = self.scale;	
		self.oldpos = -CS.UnityEngine.Vector3(self.targetPosition.x,self.targetPosition.y,0);	
		end,0.01,CS.OPSPanelController.Instance);
end

local ReadRecord = function(self)
	if checkScale then
		checkScale = false;
		return false;
	end
	return  self:ReadRecord();
end
util.hotfix_ex(CS.OPSPanelBackGround,'ResetClockContainer',ResetClockContainer)
util.hotfix_ex(CS.OPSPanelBackGround,'Start',Start)
util.hotfix_ex(CS.OPSPanelBackGround,'ReadRecord',ReadRecord)


