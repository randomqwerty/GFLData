local util = require 'xlua.util'
xlua.private_accessible(CS.AdjustAdjutantScaleController)

local CheckAssistPic_New = function(self,...)        
    if self.mAdjutantInfo.GetAdjutantType == CS.AdjutantInfo.AdjutantType.FAIRY then
    	return
    end       
    self:CheckAssistPic(...)
end

util.hotfix_ex(CS.AdjustAdjutantScaleController,'CheckAssistPic',CheckAssistPic_New)
