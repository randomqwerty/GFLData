local util = require 'xlua.util'
xlua.private_accessible(CS.OPSTowerMissionConfig)

local CheckScrollIndexPos = function(self,index,play,delay)
	local posy = self.baseHeight - self.itemHeight * index;
	local offset = self.opsTowerMissions[index].offset;
	posy = posy-offset.y;
	if play then
		self.scrollect.content:DOKill();
		self.scrollect.content:DOAnchorPosY(posy, self.durationTime):SetDelay(delay):SetEase(CS.DG.Tweening.Ease.OutQuad);
	else
		self.scrollect.content.anchoredPosition = CS.UnityEngine.Vector2(0,posy);
	end
end
util.hotfix_ex(CS.OPSTowerMissionConfig,'CheckScrollIndexPos',CheckScrollIndexPos)
