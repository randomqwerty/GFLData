local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchEquipmentCalibrationController)
xlua.private_accessible(CS.ResearchFairyCalibrationController)
xlua.private_accessible(CS.FactoryResourceController)
local StartEquip = function(self)
	self:Start();
	local rate = CS.ResManager.GetObjectByPath("Prefabs/Btn_Probability");
	local rateObj = CS.UnityEngine.GameObject.Instantiate(rate);
	local parent = self.transform:Find("Left");
	rateObj.transform:SetParent(parent, false);
	rateObj.transform.localPosition=CS.UnityEngine.Vector3(-482,226,0);
	local btnRate = rateObj:GetComponent(typeof(CS.ExButton));
	btnRate:AddOnClick(function()
			CS.CommonController.ShowRuleBox(CS.Data.GetLang(100348), CS.CommonController.MainCanvas.transform);
	end);
end
local StartFairy = function(self)
	self:Start();
	local rate = CS.ResManager.GetObjectByPath("Prefabs/Btn_Probability");
	local rateObj = CS.UnityEngine.GameObject.Instantiate(rate);
	local parent = self.transform:Find("Left");
	rateObj.transform:SetParent(parent, false);
	rateObj.transform.localPosition=CS.UnityEngine.Vector3(-482,226,0);
	local btnRate = rateObj:GetComponent(typeof(CS.ExButton));
	btnRate:AddOnClick(function()
			CS.CommonController.ShowRuleBox(CS.Data.GetLang(100349), CS.CommonController.MainCanvas.transform);
		end);
end
local StartFactory = function(self)
	self:Start();
	local url = CS.Data.GetString("kr_probability_web_v2");
	local urls = Split(url,",");
	local web = CS.ResManager.GetObjectByPath("Prefabs/Btn_ProbabilityWeb");
	local webObj = CS.UnityEngine.GameObject.Instantiate(web);
	local parent = self.transform:Find("Background");
	webObj.transform:SetParent(parent, false);
	webObj.transform.localPosition=CS.UnityEngine.Vector3(-671,47.5,0);
	local btnWeb = webObj:GetComponent(typeof(CS.ExButton));
	btnWeb:AddOnClick(function()
		local type = CS.FactoryResourceController.type;
		if type == CS.DevelopType.Gun then
			CS.OPSWebWindows.Show(urls[1]);
		elseif type == CS.DevelopType.SpecialGun or type == CS.DevelopType.SpecialEqiupment then
			CS.OPSWebWindows.Show(urls[2]);	
		elseif type == CS.DevelopType.Equipment then
			CS.OPSWebWindows.Show(urls[3]);
		elseif type == CS.DevelopType.SpecialFairy then
			CS.OPSWebWindows.Show(urls[4]);	
		end
	end);
end

function Split(szFullString, szSeparator)
	local nFindStartIndex = 1
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
	util.hotfix_ex(CS.ResearchEquipmentCalibrationController,'Start',StartEquip)
	util.hotfix_ex(CS.ResearchFairyCalibrationController,'Start',StartFairy)
	util.hotfix_ex(CS.FactoryResourceController,'Start',StartFactory)
end