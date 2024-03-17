local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.CSkillInstance)
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)

local _HandleAVGEvent = function(self,pEvent)
	if self.mSelf == nil then
		return;
	end
	local play = CS.ConfigData.playReplay;
	local index = string.find(pEvent.AVGScriptName,"always-");
	if index ~= nil then
		CS.ConfigData.playReplay = true;
	end
	self:_HandleAVGEvent(pEvent);
	CS.ConfigData.playReplay = play;
end

util.hotfix_ex(CS.GF.Battle.CSkillInstance,'_HandleAVGEvent',_HandleAVGEvent)