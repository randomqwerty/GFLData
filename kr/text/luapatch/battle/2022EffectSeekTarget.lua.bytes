local util = require 'xlua.util'
xlua.private_accessible(CS.BattleFieldTeamHolder)
xlua.private_accessible(CS.GF.Battle.BattleController)

local targetCharacter
local targetcode = "DesertEagle_6501"
local offset = CS.UnityEngine.Vector3(-0.5,0,0.1)

--Start: 加载组件
Start = function()
	--offset = self.transform.localPosition
	targetCharacter = CS.BattleLuaUtility.GetCharacterByCode(targetcode)

end
Update = function()
	if targetCharacter ~= nil then
		self.transform.position = targetCharacter.gameObject.transform.position + offset
	end
end
--depose
OnDestroy =function()

end

