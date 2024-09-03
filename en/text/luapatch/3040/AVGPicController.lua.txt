local util = require 'xlua.util'
xlua.private_accessible(CS.AVGPicController)


local DoFadePosition = function(self,isSlowInOrDisappear)
	self.tweenFade.switchMode = false;
	self:DoFadePosition(isSlowInOrDisappear);
end


util.hotfix_ex(CS.AVGPicController,'DoFadePosition',DoFadePosition)



