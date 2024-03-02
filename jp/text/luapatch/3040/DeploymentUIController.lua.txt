local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

local LoadItemData = function(self)
	self:LoadItemData();
	if self.itemObj ~= nil and not self.itemObj:isNull() then
		local rectTrans = self.itemObj:GetComponent(typeof(CS.UnityEngine.RectTransform));
		rectTrans.anchorMin = CS.UnityEngine.Vector2.one;
		rectTrans.anchorMax = CS.UnityEngine.Vector2.one;
		if self:canShowFightBuffUI() then
			rectTrans.anchoredPosition = CS.UnityEngine.Vector2(270,-330);
		else
			rectTrans.anchoredPosition = CS.UnityEngine.Vector2(270,-70);
		end
	end
end
local ItemObjMoveLeft = function(self)
	if self.itemObj ~= nil and not self.itemObj:isNull() then
		local rectTrans = self.itemObj:GetComponent(typeof(CS.UnityEngine.RectTransform));
		rectTrans:DOAnchorPosX(70,0.5):SetEase(CS.DG.Tweening.Ease.OutBack);
	end
end
local ItemObjMoveReast = function(self)
	if self.itemObj ~= nil and not self.itemObj:isNull() then
		local rectTrans = self.itemObj:GetComponent(typeof(CS.UnityEngine.RectTransform));
		rectTrans:DOAnchorPosX(270,0.5):SetEase(CS.DG.Tweening.Ease.OutBack);
	end
end

local CheckSpotsType = function(missionwintypeid,type,checknot,showTarget,medal,checkWin)
	local typenum = CS.Mathf.Abs(CS.System.Convert.ToInt32(type));
	local logicResult = true;
	if CS.GameData.missionAction ~= nil then
		for i = 0,CS.GameData.listSpotAction.Count-1  do
			local spotAction = CS.GameData.listSpotAction[i];
			local spottypenum = CS.Mathf.Abs(CS.System.Convert.ToInt32(spotAction.currentSpotType));
			if spottypenum == typenum then
				local result = spotAction.belong == CS.Belong.friendly;
				if checknot then
					result = spotAction.belong ~= CS.Belong.friendly;
				end
				if showTarget then
					spotAction.spot:ShowWinTarget(missionwintypeid, checknot,medal, checkWin);
				end
				logicResult = logicResult and result;
			end
		end
	else
		for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
			local spot = CS.DeploymentBackgroundController.Instance.listSpot[i];
			local spottypenum = CS.Mathf.Abs(CS.System.Convert.ToInt32(spot.spotInfo.type));
			if spottypenum == typenum then
				local result = spot.spotInfo.belong == CS.Belong.friendly;
				if checknot then
					result = spot.spotInfo.belong ~= CS.Belong.friendly;
				end
				if showTarget then
					spot:ShowWinTarget(missionwintypeid, checknot,medal, checkWin);
				end
				logicResult = logicResult and result;
			end
		end		
	end
	return logicResult;
end
util.hotfix_ex(CS.DeploymentUIController,'LoadItemData',LoadItemData)
util.hotfix_ex(CS.DeploymentUIController,'ItemObjMoveLeft',ItemObjMoveLeft)
util.hotfix_ex(CS.DeploymentUIController,'ItemObjMoveReast',ItemObjMoveReast)
util.hotfix_ex(CS.DeploymentUIController,'CheckSpotsType',CheckSpotsType)
