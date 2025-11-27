local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialActivityController)

local CheckSpotPathState= function(self,play,userecord)
	for i=0,self.spots.Count-1 do
		if self.spots[i].missionInfo.campaign == CS.SpecialActivityController.currentCampaign then
			if self.spots[i].mission~= nil then
				for j=self.spots[i].nextMissionSpots.Count-1,0,-1 do
					if self.spots[i].nextMissionSpots[j].mission == nil then
						self.spots[i].nextMissionSpots:RemoveAt(j);			
					end
				end
			end
		end
	end
	self:CheckSpotPathState(play,userecord);
	for i=0,self.paths.Count-1 do
		local path = self.paths[i];
		if not path.startSpot.nextMissionSpots:Contains(path.endSpot) then
			path.startSpot.nextMissionSpots:Add(path.endSpot);
		end
	end
end

util.hotfix_ex(CS.SpecialActivityController,'CheckSpotPathState',CheckSpotPathState)
