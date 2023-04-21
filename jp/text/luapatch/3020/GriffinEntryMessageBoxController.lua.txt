local util = require 'xlua.util'
xlua.private_accessible(CS.GriffinEntryMessageBoxController)
local _InitUIElements = function(self)
	 
    self:InitUIElements()
    --print(self.guideType);
    if "DailyGame" == CS.CommonSceneManagerController.instance.currentSceneName  and self.guideType==CS.GuideType.isFirstGoScoreRewardPage then
    	local layerIndex = CS.UnityEngine.SortingLayer.NameToID("UI");
    	self.canvas.sortingLayerID = layerIndex;
    end
    	
end

util.hotfix_ex(CS.GriffinEntryMessageBoxController,'InitUIElements',_InitUIElements)