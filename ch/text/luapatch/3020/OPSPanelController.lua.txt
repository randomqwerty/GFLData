local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local CheckMapAnimator = function(self)
	local playGroup = self.leftMain.gameObject:GetComponent(typeof(CS.TweenPlayGroup));
	if playGroup == nil or playGroup:isNull() then
		playGroup = self.leftMain.gameObject:AddComponent(typeof(CS.TweenPlayGroup));
	end
	if self.lastSelectOrder == -1 then
		playGroup.CurrentTweenPlayOrder = (CS.OPSPanelController.currentSelectOrder + 1) * 10 + (CS.OPSPanelController.currentSelectOrder + 1);
		CS.CommonController.Invoke(function()
				playGroup:PlayCurrentAllyOrderTween();
			end,0.3,CS.OPSPanelController.Instance);
	elseif self.lastSelectOrder ~= CS.OPSPanelController.currentSelectOrder then
		playGroup.CurrentTweenPlayOrder = (self.lastSelectOrder + 1) * 10 + (CS.OPSPanelController.currentSelectOrder + 1);
		playGroup:PlayCurrentAllyOrderTween();
	end
	self:CheckMapAnimator();
end

util.hotfix_ex(CS.OPSPanelController,'CheckMapAnimator',CheckMapAnimator)

