local util = require 'xlua.util'
xlua.private_accessible(CS.SquadGetPerformance)

local OpenEffect = function(self)
    self.gobjEffectNode:SetActive(false);
	CS.CommonController.Invoke(function()
		local trans = CS.CommonController.MainCanvas.transform;
        local canvas = nil;
        if trans.name == "MainController" then
            canvas = trans.parent;
        else
            canvas = trans;
        end
        local ratio = canvas.localScale.x / trans.localScale.x;
        self.gobjEffectNode:GetComponent(typeof(CS.ParticleScaler)):ManualSetScaleFromCurrent(ratio);
        self.gobjEffectNode:SetActive(true);
		end,0.1,self);
        
end


util.hotfix_ex(CS.SquadGetPerformance,'OpenEffect',OpenEffect)