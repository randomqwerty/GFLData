local util = require 'xlua.util'

local Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("UI/Main/NormalMission/Condition/AutoCombat/Text_AutoCombat");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(40040);
	end
end

util.hotfix_ex(CS.MissionSelectionMissionDetailController,'Start',Start)

