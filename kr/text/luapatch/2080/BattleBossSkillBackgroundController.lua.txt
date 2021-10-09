local util = require 'xlua.util'
xlua.private_accessible(CS.BattleBossSkillBackgroundController)

local TriggerSkillFlow3= function(self,spine)

	--print(self.CameraTransform.localPosition)
	if self.CameraTransform.localPosition.y ~= 0 then
		self.CameraTransform:DOLocalMove(CS.UnityEngine.Vector3(0,0,-1.2),0.4):SetUpdate(true):Play()
	end
	self:TriggerSkillFlow3(spine)
end

util.hotfix_ex(CS.BattleBossSkillBackgroundController,'TriggerSkillFlow3',TriggerSkillFlow3)

