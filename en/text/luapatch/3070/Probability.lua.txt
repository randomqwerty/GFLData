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
	local web = CS.ResManager.GetObjectByPath("Prefabs/Btn_ProbabilityWeb");
	local webObj = CS.UnityEngine.GameObject.Instantiate(web);
	local parent = self.transform:Find("Background");
	webObj.transform:SetParent(parent, false);
	webObj.transform.localPosition=CS.UnityEngine.Vector3(-671,47.5,0);
	local btnWeb = webObj:GetComponent(typeof(CS.ExButton));
	btnWeb:AddOnClick(function()
		local url = CS.Data.GetString("kr_probability_web")
		CS.OPSWebWindows.Show(url);
	end);
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
	util.hotfix_ex(CS.ResearchEquipmentCalibrationController,'Start',StartEquip)
	util.hotfix_ex(CS.ResearchFairyCalibrationController,'Start',StartFairy)
	util.hotfix_ex(CS.FactoryResourceController,'Start',StartFactory)
end