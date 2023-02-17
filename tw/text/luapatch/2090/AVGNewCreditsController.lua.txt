local util = require 'xlua.util'
xlua.private_accessible(CS.AVGNewCreditsController)
xlua.private_accessible(CS.UnityEngine.Camera)
xlua.private_accessible(CS.UnityEngine.PostProcessing.PostProcessingBehaviour)

local _Start = function(self)
	self:Start();
	if CS.UnityEngine.Camera.main~=nil then
		CS.UnityEngine.Camera.main.gameObject:AddComponent(typeof(CS.UnityEngine.PostProcessing.PostProcessingBehaviour));
		local process=CS.UnityEngine.Camera.main.gameObject:GetComponent(typeof(CS.UnityEngine.PostProcessing.PostProcessingBehaviour));
		--local prof = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("PostProcessing/TVEffect",".asset"));
		process.profile = CS.ResManager.GetObjectByPath("PostProcessing/TVEffect",".asset");
	end
end
local _DestroyCredits = function(self)
	self:DestroyCredits();
	if CS.UnityEngine.Camera.main~=nil then
		local process=CS.UnityEngine.Camera.main.gameObject:GetComponent(typeof(CS.UnityEngine.PostProcessing.PostProcessingBehaviour));
		if process~=nil then
			CS.UnityEngine.Object.Destroy(process);
		end
	end
end
util.hotfix_ex(CS.AVGNewCreditsController,'Start',_Start)
util.hotfix_ex(CS.AVGNewCreditsController,'DestroyCredits',_DestroyCredits)