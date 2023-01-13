local util = require 'xlua.util'
xlua.private_accessible(CS.FetterStoryMilestone)

local InitUIElements = function(self)
	
end
local InitData = function(self,fetterInfo)
	if self.listRewardBtn.Count == 0 then
	self.listRewardBtn:Add(self.btnReward1);
	for i=0,3 do
		local rewardBtn = CS.UnityEngine.Object.Instantiate(self.btnReward1):GetComponent(typeof(CS.ExButton));
		rewardBtn.transform:SetParent(self.btnReward1.transform.parent,false);
		rewardBtn:AddOnClick(function()
				self:OnClickReward(i + 1);
		end
			, CS.AudioUI.UI_Fetter_MilestoneClick);
		self.listRewardBtn:Add(rewardBtn);
	end
	
	
	
	self.btnReward1:AddOnClick(function()
			self:OnClickReward(0);
	end, CS.AudioUI.UI_Fetter_MilestoneClick);
	self.btnTask:AddOnClick(function()
			self:OnTaskBtnClicke();
	end, CS.AudioUI.UI_Fetter_ClickDefault);
	
	self.btnDone:AddOnClick(function()
			self:OnBtnDoneClick();
	end,CS.AudioUI.UI_default);
		
	end
	
	self:InitData(fetterInfo);
end


util.hotfix_ex(CS.FetterStoryMilestone,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.FetterStoryMilestone,'InitData',InitData)