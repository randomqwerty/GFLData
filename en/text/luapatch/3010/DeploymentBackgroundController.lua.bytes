local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBackgroundController)
--修正下背景显示
local CheckSize = function(self)
	local mapsize = CS.DeploymentBackgroundController.currentLayerData.mapSize;
	local size = CS.Mathf.Max(mapsize.x,mapsize.y);
	self.cloudMaterial:SetFloat("_AddDistance",size*2);
end

local CreateMap = function(self)
	CheckChildEnable(self.transfromSpots);
	CheckChildEnable(self.buildParent);	
	CheckChildEnable(self.lines);	
	CheckChildEnable(self.teamParent);
	CheckChildEnable(self.background);
	self:CreateMap();	
	local mapcanvas = self.transform:Find("CanvasMap"):GetComponent(typeof(CS.UnityEngine.Canvas));
	mapcanvas.sortingOrder = -1000;
end

function CheckChildEnable(trans)
	if trans == nil then
		return;
	end
	for i=0,trans.childCount -1 do
		trans:GetChild(i).gameObject:SetActive(false);
	end
end

local CreateSpots = function(self)
	self:CreateSpots();
	for i=0,self.listSpotPath.Count-1 do
		self.listSpotPath[i]:Rest();
	end
end

local ShowShade = function(self,play,duration)
	self:ShowShade(play,duration);
	local spothq = nil;
	local spotDta = nil;
	local spotteam = nil;
	for i=0,CS.DeploymentBackgroundController.currentLayerData.spots.Count-1 do
		local s = CS.DeploymentBackgroundController.currentLayerData.spots[i];
		if s.belong == CS.Belong.friendly then
			if s.type == CS.SpotType.headQuarter then
				spothq = s;
			end
			if s.type == CS.SpotType.DTA or s.type == CS.SpotType.HeavyDTA then
				spotDta = s;
			end		
		end
		if s:HasFriendlyTeam() then
			spotteam = s;
		end
	end
	local pos = CS.DeploymentBackgroundController.currentLayerData.offset;
	if spothq ~= nil then
		 pos = CS.UnityEngine.Vector2(spothq.transform.localPosition.x,spothq.transform.localPosition.y);		
	elseif spotDta ~= nil then
		pos = CS.UnityEngine.Vector2(spotDta.transform.localPosition.x,spotDta.transform.localPosition.y);		
	elseif 	spotteam ~= nil then
		pos = CS.UnityEngine.Vector2(spotteam.transform.localPosition.x,spotteam.transform.localPosition.y);		
	end
	CS.DeploymentController.TriggerMoveCameraEvent(pos,play);	
end
util.hotfix_ex(CS.DeploymentBackgroundController,'CheckSize',CheckSize)
util.hotfix_ex(CS.DeploymentBackgroundController,'CreateMap',CreateMap)
util.hotfix_ex(CS.DeploymentBackgroundController,'CreateSpots',CreateSpots)
util.hotfix_ex(CS.DeploymentBackgroundController,'ShowShade',ShowShade)


