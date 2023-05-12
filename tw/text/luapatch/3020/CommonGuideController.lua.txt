local util = require 'xlua.util'
xlua.private_accessible(CS.CommonGuideController)
xlua.private_accessible(CS.DailyExploreDifficultySelection)
local findTagCount = 0;
local myInvokeStartAction = function(self, arrObject)
    local name = string.format("%s", arrObject[0]);
	if(name == "Card1") then
		findTagCount = findTagCount + 1;
		if (findTagCount == 10) then
			CS.CommonGuideController.instance:SetGuideStatus(true, CS.GuideType.dailyStep2);
			CS.DailyExploreData.GetInstance().CheckDay = -1;
			CS.CommonController.GotoScene("DailyGame", 0, 0, nil, "", false, "", true);
		else
			self:InvokeStartAction(arrObject);
		end
	else
		findTagCount = 0;
		self:InvokeStartAction(arrObject);
	end
end
local myCheckGuide = function(self)
	if (CS.CommonGuideController.Instance:CheckGuide(CS.GuideType.dailyStep3) and CS.CommonGuideController.Instance:CheckGuide(CS.GuideType.isFirstClickResetBtnCommitAgain) == false) then
		CS.CommonGuideController.TriggerCheckGuideEvent(CS.GuideType.isFirstClickResetBtnCommitAgain);
		local cv = CS.GriffinEntryMessageBoxController.Instance:GetComponent(typeof(CS.UnityEngine.Canvas));
		cv.sortingLayerName = "UI";
		cv.sortingLayerID = 5;
		cv.sortingOrder = 101;
		CS.GriffinEntryMessageBoxController.Instance.gameObject.layer = 5;
		local msgBoxObj = CS.UnityEngine.GameObject.Find("MessageBoxCamera");
		if (msgBoxObj ~= nil) then
			cv.worldCamera = msgBoxObj:GetComponent(CS.UnityEngine.Camera);
		end
	end
end
util.hotfix_ex(CS.GuideManagerController,'InvokeStartAction',myInvokeStartAction)
util.hotfix_ex(CS.DailyExploreDifficultySelection,'CheckGuide',myCheckGuide)