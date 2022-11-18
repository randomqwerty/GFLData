local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterDetailUIController)

local ShowTheaterReward = function(self)
	if self.m_TheaterOccupiedReward ~= nil then
		self:CheckHasNewTheaterReward();
		CS.TheaterRewardBoxUIController.Show(self.transform, CS.GameData.listTheaterEventInfo:GetDataById(self.info.theater_event_id), self.m_TheaterOccupiedReward);
		return;
	end
	
	local createConnection = xlua.get_generic_method(CS.ConnectionController, 'CreateConnection');
	local createRequest = createConnection(CS.RequestTheaterRewardState);
	createRequest(CS.RequestTheaterRewardState(), function(req)
			self.m_TheaterOccupiedReward = req.Result;
			self:CheckHasNewTheaterReward();
			CS.TheaterRewardBoxUIController.Show(self.transform, CS.GameData.listTheaterEventInfo:GetDataById(self.info.theater_event_id), self.m_TheaterOccupiedReward);
		end, nil);
	createConnection = nil;
	createRequest = nil;
end

util.hotfix_ex(CS.TheaterDetailUIController,'ShowTheaterReward',ShowTheaterReward)