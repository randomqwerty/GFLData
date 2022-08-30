local util = require 'xlua.util'
xlua.private_accessible(CS.SquadProgressBarController)
local InitUIElements = function(self)
	
end
local Awake = function(self)
	self.initWidth = self.gridStage.cellSize.x;
	self.initHeight = self.gridStage.cellSize.y;
	self.initSpacingX = self.gridStage.spacing.x;
	self.initSpacingY = self.gridStage.spacing.y;
end
util.hotfix_ex(CS.SquadProgressBarController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.SquadProgressBarController,'Awake',Awake)