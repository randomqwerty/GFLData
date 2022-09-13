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

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local obj1 = CS.ResManager.GetObjectByPath("AtlasClips3010/success");
		if obj1 ~= nil then
			local imageTrans = self.transform:Find("NewInfoBox/EchelonList/Echelon/EchelonItem/Img_GreatSuccess"):GetComponent(typeof(CS.UnityEngine.UI.Image));
			imageTrans.sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
		end	
		local txtTrans = self.transform:Find("NewInfoBox/EchelonList/Echelon/Img_OnSally/Tex_OnSally"):GetComponent(typeof(CS.ExText));
		txtTrans.text = CS.Data.GetLang(40414);
	end
end
util.hotfix_ex(CS.CommonOperationSettlementController,'SetLeaderPic',_SetLeaderPic)
--util.hotfix_ex(CS.CommonOperationSettlementController,'Awake',Awake)
