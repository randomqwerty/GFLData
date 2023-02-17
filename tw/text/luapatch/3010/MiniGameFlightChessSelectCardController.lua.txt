local util = require 'xlua.util'
xlua.private_accessible(CS.MiniGameFlightChessSelectCardController)
local mySetOptionList = function(self,options,isItem,targetNum)
	self.transform.localScale = CS.UnityEngine.Vector3(1, 1, 1);
    self:SetOptionList(options,isItem,targetNum)
end
util.hotfix_ex(CS.MiniGameFlightChessSelectCardController,'SetOptionList',mySetOptionList)