local util = require 'xlua.util'
xlua.private_accessible(CS.SquadProgressBarController)

local hasSet=false;
local InitUIElements = function(self)
	
end
local _UpdateStage = function(self) 
	if hasSet==false then
		self.initWidth = self.gridStage.cellSize.x;
		self.initHeight = self.gridStage.cellSize.y;
		self.initSpacingX = self.gridStage.spacing.x;
		self.initSpacingY = self.gridStage.spacing.y;
		hasSet=true;
	end
	self:UpdateStage();
end
util.hotfix_ex(CS.SquadProgressBarController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.SquadProgressBarController,'UpdateStage',_UpdateStage)