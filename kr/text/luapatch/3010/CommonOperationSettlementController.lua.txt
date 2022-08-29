local util = require 'xlua.util'
xlua.private_accessible(CS.CommonOperationSettlementController)
xlua.private_accessible(CS.GF.Battle.Gun)
xlua.private_accessible(CS.GF.Battle.BaseTeam)
local _SetLeaderPic = function(self,index,teamId)
	self:SetLeaderPic(index,teamId);
	if index==0 then
		local listGun = CS.GameData.dictTeam[teamId];
		local leader = listGun:GetLeader();
		if leader~=nil then
			CS.CommonAudioController.PlayCharacterVoice(leader:GetVoiceCode(), CS.VoiceType._OPERATIONOVER_);
		end
		listGun=nil;
		leader=nil;
	end
end

util.hotfix_ex(CS.CommonOperationSettlementController,'SetLeaderPic',_SetLeaderPic)
