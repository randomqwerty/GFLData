local util = require 'xlua.util'
xlua.private_accessible(CS.AVGCreditsController)

local Start = function(self)
	if CS.IllustratedBookController.Instance ~= nil and not CS.IllustratedBookController.Instance:isNull() then
		CS.GameData.currentSelectedMissionInfo = CS.GameData.listMissionInfo:GetDataById(CS.IllustratedBookCGPlayBackController.currentSelectedMissionId);
	end
	self:Start();
end

local Request = function(self)
	if CS.IllustratedBookController.Instance ~= nil and not CS.IllustratedBookController.Instance:isNull() then
		CS.GameData.currentSelectedMissionInfo = CS.GameData.listMissionInfo:GetDataById(CS.IllustratedBookCGPlayBackController.currentSelectedMissionId);
	end
	self:Request();
end
util.hotfix_ex(CS.AVGCreditsController,'Start',Start)
util.hotfix_ex(CS.RequestCredits,'Request',Request)