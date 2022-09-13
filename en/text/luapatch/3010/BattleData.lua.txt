local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleData)
local GetGridPositionFromClick = function(hitPosition)

	local x = 0
	local y = 0
	local clickPosition = CS.UnityEngine.Vector2(hitPosition.x - CS.GF.Battle.BattleController.Instance.friendlyArmyOffset + 7.5, hitPosition.z + 7.2)
	if clickPosition.x > 5 then
		x = 2
	else 
		if clickPosition.x > 2.5 then
			x = 1
		end
	end
	if clickPosition.y > 7.2666667 then
		y = 2
	else 
		if clickPosition.y > 3.633333 then
			y = 1
		end
	end
	return CS.GF.Battle.GridPos(x, y)
end

xlua.hotfix(CS.GF.Battle.BattleData,'GetGridPositionFromClick',GetGridPositionFromClick)