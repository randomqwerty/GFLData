local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentLine)
--修正计划线层级
local ShowPlanLine = function(self,start,end1,lineColor,control,useworldpos)
	self:ShowPlanLine(start,end1,lineColor,control,useworldpos);
	self.lineRenderer:SetWidth(20, 20);
	local canvas = end1.parent.parent:GetComponent(typeof(CS.UnityEngine.Canvas));
	self.lineRenderer.sortingOrder = canvas.sortingOrder;
end
--修正计划线层级
local ShowTeamPlanLine = function(self,start,end1,lineColor,clip,useworldpos)
	self:ShowTeamPlanLine(start,end1,lineColor,clip,useworldpos);
	self.lineRenderer:SetWidth(20, 20);
	local canvas = end1.parent.parent:GetComponent(typeof(CS.UnityEngine.Canvas));
	self.lineRenderer.sortingOrder = canvas.sortingOrder;
end

local ShowSkillCurve = function(self,startSpot,team,lineColor,endEffectCode)
	self:ShowSkillCurve(startSpot,team,lineColor,endEffectCode);
	self.lineRenderer:SetWidth(20, 20);
end

local ShowCurve = function(self,startSpot,team,lineColor,usemorldpos)
	self:ShowCurve(startSpot,team,lineColor,usemorldpos);
	self.lineRenderer:SetWidth(20, 20);
end

local ShowMoveDirection = function(self,moveStartcolor,moveendColor,time,width)
	self:ShowMoveDirection(moveStartcolor,moveendColor,time,width);
	self.movelineRenderer:SetWidth(0, 20);
end
util.hotfix_ex(CS.DeploymentLine,'ShowPlanLine',ShowPlanLine)
util.hotfix_ex(CS.DeploymentLine,'ShowTeamPlanLine',ShowTeamPlanLine)
util.hotfix_ex(CS.DeploymentLine,'ShowSkillCurve',ShowSkillCurve)
util.hotfix_ex(CS.DeploymentLine,'ShowCurve',ShowCurve)
util.hotfix_ex(CS.DeploymentLine,'ShowMoveDirection',ShowMoveDirection)



