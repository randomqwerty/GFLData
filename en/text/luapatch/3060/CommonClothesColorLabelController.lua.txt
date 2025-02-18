local util = require 'xlua.util'
xlua.private_accessible(CS.CommonClothesColorLabelController)
function OnClickWeb() 
	local url = CS.Data.GetString("kr_probability_web")
	CS.UnityEngine.Application.OpenURL(url);
end

function OnClickRate() 
	CS.CommonController.ShowRuleBox(CS.Data.GetLang(250071), CS.CommonController.MainCanvas.transform);
end
local mInitUIElements = function(self)
	
	 
	--self.btnColorranRandomProbability.transform.localPosition=CS.UnityEngine.Vector3(self.btnColorranRandom.transform.localPosition.x+18,self.btnColorranRandom.transform.localPosition.y-150,0);
	
	local web = CS.ResManager.GetObjectByPath("Prefabs/Btn_ProbabilityWeb");
    local webObj = CS.UnityEngine.GameObject.Instantiate(web);
    webObj.transform:SetParent(self.transform, false);
    webObj.transform.localPosition=CS.UnityEngine.Vector3(1193,110,0);
    local btnWeb = webObj:GetComponent(typeof(CS.ExButton));
	btnWeb:AddOnClick(OnClickWeb);

	local rate = CS.ResManager.GetObjectByPath("Prefabs/Btn_Probability");
    local rateObj = CS.UnityEngine.GameObject.Instantiate(rate);
    rateObj.transform:SetParent(self.transform, false);
    rateObj.transform.localPosition=CS.UnityEngine.Vector3(1058,110,0);

    local btnRate = rateObj:GetComponent(typeof(CS.ExButton));
	btnRate:AddOnClick(OnClickRate);

	self:InitUIElements();
end
local mSwitchColorrantButtons = function(self,isOn)
	self:SwitchColorrantButtons(isOn)

	local btnWeb=self.transform:Find("Btn_ProbabilityWeb(Clone)");
	local btnRate=self.transform:Find("Btn_Probability(Clone)");
	if btnWeb~=nil then
		btnWeb.gameObject:SetActive(isOn)
	end
	if btnRate~=nil then
		btnRate.gameObject:SetActive(isOn)
	end
end

if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then		
util.hotfix_ex(CS.CommonClothesColorLabelController,'InitUIElements',mInitUIElements)
util.hotfix_ex(CS.CommonClothesColorLabelController,'SwitchColorrantButtons',mSwitchColorrantButtons)
end


