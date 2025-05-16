local util = require 'xlua.util'
xlua.private_accessible(CS.CommonGuideController)

local InstantiateGuideCanvas = function(self,txtPath,currentGuide,canInit)
	if currentGuide == CS.GuideType.dailyStep1 then
		local check = false;
		for i=0,CS.GameData.listDailyPointPrize.Count-1 do
			local prize = CS.GameData.listDailyPointPrize[i];
			if prize.Type == 1 and prize:isOpenTime() then
				check = true;
			end
		end
		if not check then
			return;
		end
	end
	self:InstantiateGuideCanvas(txtPath,currentGuide,canInit);
end

util.hotfix_ex(CS.CommonGuideController,'InstantiateGuideCanvas',InstantiateGuideCanvas)

