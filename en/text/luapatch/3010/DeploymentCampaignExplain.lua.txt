local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentCampaignExplain)

local CreateWinSplitLine = function(self)
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local txt1 = self.transform:Find("Frame/BackGround/NewMissionIntroduce/MissionTarget/ScrollRect/Viewport/Grid/WinSplitLine/Tex_Win");
		local textshow = txt1:GetComponent(typeof(CS.ExText));
		textshow.text = CS.Data.GetLang(40133);		
	end
	return self:CreateWinSplitLine();
end

local CreateLoseSplitLine = function(self)
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local txt2 = self.transform:Find("Frame/BackGround/NewMissionIntroduce/MissionTarget/ScrollRect/Viewport/Grid/LoseSplitLine/Tex_Lose");
		local textshow1 = txt2:GetComponent(typeof(CS.ExText));
		textshow1.text = CS.Data.GetLang(30463);	
	end
	return self:CreateLoseSplitLine();
end
util.hotfix_ex(CS.DeploymentCampaignExplain,'CreateWinSplitLine',CreateWinSplitLine)
util.hotfix_ex(CS.DeploymentCampaignExplain,'CreateLoseSplitLine',CreateLoseSplitLine)
