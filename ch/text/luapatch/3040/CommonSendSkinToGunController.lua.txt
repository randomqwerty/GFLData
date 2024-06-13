local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSendSkinToGunController)
xlua.private_accessible(CS.RequestSendGiftToNpc)

local mOnRequestGiveNPCGift = function(self,request)
	if self.npc.id < -1  then
		getFurnitureId = 0;
		self.isNew = request.isNewSkin;
        self.mNpcSkinRepeat = request.mChangeSkinRepeat;
        self:DoPerformance();
	else
		self:OnRequestGiveNPCGift(request);
	end
	
end

util.hotfix_ex(CS.CommonSendSkinToGunController,'OnRequestGiveNPCGift',mOnRequestGiveNPCGift)
