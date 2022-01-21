local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionGroup)

local transReset = function(self)
	return self.uiHolder:GetUIElement("ScoreNode/Img_ResetBG",typeof(CS.UnityEngine.RectTransform));
end

local ShowReast = function(self)
	if self.holder.nextMissionSpotOrders.Count>0 then		
		if self.holder.nextMissionSpotOrders[0].CurrentMissionId ~= 0 then
			return true;
		end					
	end
	return false;
end
local RefreshUI = function(self)
	self:RefreshUI();
	if self.lastmissioninfo == nil then
		return;
	end
	if CS.OPSPanelController.Instance.campaionId == -51 then
		local bg = self.transform:Find("BackGround/Score_Unlocked/Img_MissionInfo");
		if bg ~= nil then
			local holder = bg:GetComponent(typeof(CS.UGUISpriteHolder));
			local image = bg:GetComponent(typeof(CS.ExImage));
			if self.lastmissioninfo.id == 11003 then
				holder:SetImageSprite(5, image);
			elseif self.lastmissioninfo.id == 11004 then
				holder:SetImageSprite(6, image);
			elseif self.lastmissioninfo.id == 11005 then
				holder:SetImageSprite(1, image);
			elseif self.lastmissioninfo.id == 11006 then
				holder:SetImageSprite(2, image);
			elseif self.lastmissioninfo.id == 11007 then
				holder:SetImageSprite(3, image);
			elseif self.lastmissioninfo.id == 11008 then
				holder:SetImageSprite(4, image);
			elseif self.lastmissioninfo.id == 11009 then
				holder:SetImageSprite(0, image);
			elseif self.lastmissioninfo.id == 11010 then
				holder:SetImageSprite(4, image);
			end
		end
	end
end
util.hotfix_ex(CS.OPSPanelMissionGroup,'get_transReset',transReset)
util.hotfix_ex(CS.OPSPanelMissionGroup,'ShowReast',ShowReast)
util.hotfix_ex(CS.OPSPanelMissionGroup,'RefreshUI',RefreshUI)