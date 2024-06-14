local util = require 'xlua.util'
xlua.private_accessible(CS.QuestsController)
xlua.private_accessible(CS.DailyWeekQuestCtrl)
xlua.private_accessible(CS.CareerQuestUnitController) 

local ShowUI = function(self)
	self:ShowUI();
	if CS.DailyWeekQuestCtrl.Instance~=nil and CS.DailyWeekQuestCtrl.Instance.hasLoadPic then
		if CS.DailyWeekQuestCtrl.Instance.kalinaParent.childCount == 0 then
			CS.DailyWeekQuestCtrl.Instance.hasLoadPic = false;
			CS.DailyWeekQuestCtrl.Instance:InitKalina();
			CS.DailyWeekQuestCtrl.Instance:LoadRewardBox();
		end 
	end
end
local mAwake = function(self) 
	self:Awake();
	
	local old_btn = self.transform:Find("MainController/SideBar/CommonToggleGroupControlller/ResearchQuests");
	if old_btn~=nil then
		old_btn.gameObject:SetActive(false);
	end
	local old_career = self.transform:Find("CareerQuest");
	if old_career~=nil then
		CS.UnityEngine.Object.DestroyImmediate(old_career.gameObject);
		local parent = self.transform;
		local obj = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("AtlasClips3040/CareerQuestJP"), parent, false);
		obj.name="CareerQuest";
		obj:SetActive(false);
		print("replace CareerQuest")
	end
end
local mCheckNewCareerQuestVersion = function(self) 

end
local mHideNewCareerQuestTip = function(self) 
	if CS.GameData.userRecord:CheckCareerTaskVersion()==true then
        CS.GameData.userRecord:SetCareerTaskVersion_HasClick();
    end
end
util.hotfix_ex(CS.QuestsController,'ShowUI',ShowUI)
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
	util.hotfix_ex(CS.CareerQuestUnitController,'Awake',mAwake)
	util.hotfix_ex(CS.QuestsController,'CheckNewCareerQuestVersion',mCheckNewCareerQuestVersion)
	util.hotfix_ex(CS.QuestsController,'HideNewCareerQuestTip',mHideNewCareerQuestTip)
end