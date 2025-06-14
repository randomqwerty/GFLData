local util = require 'xlua.util'
xlua.private_accessible(CS.CommonLive2DController)
xlua.private_accessible(CS.MallKalinaFavorController)

local SetScenePosNew = function(self)
	self:SetScenePosNew();
	self.pos = self.gameObject:GetComponent(typeof(CS.UnityEngine.RectTransform)).anchoredPosition;
end

local getMotionsData = function(self,type)
	if self.mTypeToLive2DMotionDataDic:ContainsKey(type) then
		return self:getMotionsData(type);
	end
	CS.NDebug.LogError("当前缺少动作(默认待机101)",type);
	return self:getMotionsData("101");
end

local LoadNPCPic = function(self)
	self:LoadNPCPic();
	self.mLive2DMotionListLevelUp:Clear();
	self.mLive2DMotionListLevelHit:Clear();
end

local PlayLive2DCustomVoice = function(self,type)
	self:PlayLive2DCustomVoice(type);
	if self.textDialogue.text == "" then
		self:ShowDialog(false);
	end
end
util.hotfix_ex(CS.CommonLive2DController,'SetScenePosNew',SetScenePosNew)
util.hotfix_ex(CS.CommonLive2DController,'getMotionsData',getMotionsData)
util.hotfix_ex(CS.MallKalinaFavorController,'LoadNPCPic',LoadNPCPic)
util.hotfix_ex(CS.MallKalinaFavorController,'PlayLive2DCustomVoice',PlayLive2DCustomVoice)