local util = require 'xlua.util'
xlua.private_accessible(CS.TargetTrainGameData)

local SetDamageLog  = function(self,log)
	self:SetDamageLog(log)
	local BattleController = CS.GF.Battle.BattleController.Instance
	if BattleController ~= nil then
		local t_fun = util.cs_generator(function()
				coroutine.yield(CS.UnityEngine.WaitForEndOfFrame())
				CS.GF.Battle.CSkillManager.Instance:UninitSkill()
			end)
		--local co = CS.XLua.Cast.IEnumerator(t_fun)
		BattleController:StartCoroutine(t_fun)
	end
end

util.hotfix_ex(CS.TargetTrainGameData,'SetDamageLog',SetDamageLog)