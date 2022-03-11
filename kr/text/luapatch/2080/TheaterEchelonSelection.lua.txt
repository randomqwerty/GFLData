local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterEchelonSelection)

local Start  = function(self)
	theaterInfo = CS.GameData.listTheaterInfo:GetDataById(self.areaInfo.theater_id);
	maxSquad = theaterInfo.hoc_formation_number;
	local tempSquad = CS.System.Collections.Generic.List(CS.Squad)();
	for i=1,maxSquad do
		tempSquad:Add(CS.TheaterTeamData.instance:GetSquad(i));
	end
	CS.TheaterTeamData.instance.dictTeamSquad:Clear();
	for i=1,maxSquad do
		CS.TheaterTeamData.instance:AddSquad(tempSquad[i-1]);
	end
	tempSquad = nil;
	self:Start();
end

local ShowTeamFormation = function(self)
	local canshow = false;
	for i=1,CS.GameData.userInfo.maxTeam do
		if CS.TheaterTeamData.isSangvisTeam then
			local tempList = CS.GameData.listSangvisGun:FindAll(
				function(g)
					return g.teamId == i;
				end
			);
			local totalCnt = tempList.Count;
			if totalCnt > 0 then
				canshow = true;
				self.OperationTeamInfo:ShowAsTheaterTeamSel();
			end
		else
			local tempList = CS.GameData.listGun:FindAll(
				function(g)
					return g.teamId == i;
				end
			);
			local totalCnt = tempList.Count;
			if totalCnt > 0 then
				canshow = true;
				self.OperationTeamInfo:ShowAsTheaterTeamSel();
		    end
	    end
	end
	if canshow == false then
		if CS.TheaterTeamData.isSangvisTeam then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(210266));
		else
			CS.CommonController.LightMessageTips(CS.Data.GetLang(210265));
		end
	end
end
local _RefreshExtraUI = function(self)
	self.maxSangvisCost = self.areaInfo.theater_spare_sangvis_cost + CS.Data.GetConstructionGunNumEffect(self.areaInfo.theater_id, CS.TheaterTeamData.isSangvisTeam);
	CS.TheaterTeamData.instance.spareGunNum = self.areaInfo.theater_spare_gun_num + CS.Data.GetConstructionGunNumEffect(self.areaInfo.theater_id, CS.TheaterTeamData.isSangvisTeam);
	CS.TheaterTeamData.instance.spareSangvisNum = (self.areaInfo.theater_spare_sangvis_cost + CS.Data.GetConstructionGunNumEffect(self.areaInfo.theater_id, CS.TheaterTeamData.isSangvisTeam))/2;
	self:RefreshExtraUI();
end
util.hotfix_ex(CS.TheaterEchelonSelection,'Start',Start)
util.hotfix_ex(CS.TheaterEchelonSelection,'ShowTeamFormation',ShowTeamFormation)
util.hotfix_ex(CS.TheaterEchelonSelection,'RefreshExtraUI',_RefreshExtraUI)