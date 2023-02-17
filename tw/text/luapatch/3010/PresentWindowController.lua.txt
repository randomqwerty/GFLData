local util = require 'xlua.util'
xlua.private_accessible(CS.PresentWindowController)
xlua.private_accessible(CS.Data)
xlua.private_accessible(CS.CommonController)
local idLangMap={};
local myStart = function(self)
	self:Start();
	if CS.System.String.IsNullOrEmpty(CS.Data.GetString("present_info")) then

	else
		local assemblyMemberArray = Split(CS.Data.GetString("present_info"),';')
		for i = 1, #assemblyMemberArray do
			local kv = Split(assemblyMemberArray[i], ':');
			local id = CS.System.Convert.ToInt32(kv[1]);
			local langId = CS.System.Convert.ToInt32(kv[2]);
			idLangMap[id] = langId;
		end
	end
	
end
local myShowPresentTip = function(self)
    local content;
	if (self.presentInfo.presentType == CS.PresentInfo.PresentType.Optional) then
		content = CS.Data.GetLang(53033);
	elseif	self.presentInfo.presentType == CS.PresentInfo.PresentType.Random then
		content = CS.Data.GetLang(53034);
	elseif	self.presentInfo.presentType == CS.PresentInfo.PresentType.Static then
		content = CS.Data.GetLang(53035);
	elseif	self.presentInfo.presentType == CS.PresentInfo.PresentType.Multiple then
		content = CS.Data.GetLang(53036);
	else 
		content = "";	
	end
	if(is_include(self.presentInfo.item_id, idLangMap)) then
		content = CS.Data.GetLang(idLangMap[self.presentInfo.item_id]);
	end
	CS.CommonController.ShowRuleBox(content,CS.CommonController.MainCanvas.transform);
end
function is_include(value, t)
	for k,v in pairs(t) do
		if  k == value then
			return true;
		end
	end
	return false;
end

local ShowSkinPreview = function(self,skinInfo)
	if skinInfo == nil then
		return;
	end
	self.objLeft:SetActive(false);
	self.objRight:SetActive(false);
	self.objPackageBg:SetActive(false);
	local gunInfo = CS.GameData.listGunInfo:GetDataById(skinInfo.fitGun);
	local pic = CS.CommonController.LoadBigPic(gunInfo.code, self.btnBlackBg.transform, skinInfo.id, false);
	pic:SwitchDamaged(false);
end
util.hotfix_ex(CS.PresentWindowController,'ShowPresentTip',myShowPresentTip)
util.hotfix_ex(CS.PresentWindowController,'Start',myStart)
util.hotfix_ex(CS.PresentWindowController,'ShowSkinPreview',ShowSkinPreview)