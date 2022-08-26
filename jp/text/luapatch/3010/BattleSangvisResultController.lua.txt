local util = require 'xlua.util'
xlua.private_accessible(CS.BattleSangvisResultController)
local get_transSquadHolder = function(self)
	return self.uiHolder:GetUIElement("CommanderInfo/SquadLabelHolder",typeof(CS.UnityEngine.Transform));
end
util.hotfix_ex(CS.BattleSangvisResultController,'get_transSquadHolder',get_transSquadHolder)