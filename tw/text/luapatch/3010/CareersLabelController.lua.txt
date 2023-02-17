local util = require 'xlua.util'
xlua.private_accessible(CS.CareersLabelController)
xlua.private_accessible(CS.CareerQuestController)
local myInit = function(self,questitem)
    self:Init(questitem)
	if (CS.CareerQuestController.Instance.lockedObj.activeSelf) then
		self.lockedMask:SetActive(true);
		self.lockedMaskBG:SetActive(false);
		self.lockedMaskTex:SetActive(false);
	end
	if (self.lockedMask.activeSelf) then
		self.btnReceive.gameObject:SetActive(false);
		self.btnMission.gameObject:SetActive(false);
		self.mBtnGoNow.gameObject:SetActive(false);
		self.quickJumpObj:SetActive(true);
		self.receivedQuickObj:SetActive(false);
		self.receivedMissionObj:SetActive(false);
		self.inProgressObj:SetActive(false);
		self.btnMoreMaskObj:SetActive(true);
		self.placeHolderObj:SetActive(false);
		self.texProgressObj:SetActive(false);
	else
		self.btnMoreMaskObj:SetActive(false);
		self.placeHolderObj:SetActive(true);
	end
	self.imgMissionBGObj:SetActive(self.questItem.questInfo.IsAccomplished == false);
end
util.hotfix_ex(CS.CareersLabelController,'Init',myInit)