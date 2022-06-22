local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)

xlua.private_accessible(CS.ExButton)
local _CheckNewShop = function(self)
	self:CheckNewShop(); 
	if CS.GameData.userInfo.DaysAfterSeven <= CS.Data.GetInt("seven_attendance_duration")then
		local key=CS.GameData.userInfo.userId.."";
		local tt=CS.Data.GetPlayerPrefString(key,"TimeLimitEvent");
		local now= CS.Data.serverTomorrowZero.."";
		
		if tt~= now then 
			self.btnEvent.badge:ShowMallBade(CS.UnityEngine.Vector2(20,20)); 
		else
			self.btnEvent.badge:CloseBadge(); 
		end
	end
end
local _OnClickEvent_btn = function(self)
	self:OnClickEvent_btn();
	
	if CS.GameData.userInfo.DaysAfterSeven <= CS.Data.GetInt("seven_attendance_duration") then
		local key=CS.GameData.userInfo.userId.."";
		local tt=CS.Data.GetPlayerPrefString(key,"TimeLimitEvent");
		local now= CS.Data.serverTomorrowZero.."";
		if tt~= now then 
			CS.Data.SetPlayerPrefString(key,"TimeLimitEvent",now);
			self.btnEvent.badge:CloseBadge();  
		end
	end
end

local InitUIElements= function(self)
	self:InitUIElements();
	local obj1 = CS.ResManager.GetObjectByPath("AtlasClips2090/活动_战区小按钮");
	if obj1 ~= nil then
		print("载入图片");
		self.btnTheater:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
	end
end

local _OnClickHomeAVG = function(self)	
	if self.adjutantController.adjutantInfo2 == nil then
		--CS.NDebug.LogError("_OnClickHomeAVG")
        self.adjutantController:UpdateAdjutant(self.adjutantController.adjutantInfo);
    end

	self:OnClickHomeAVG();
end
util.hotfix_ex(CS.HomeController,'CheckNewShop',_CheckNewShop)
util.hotfix_ex(CS.HomeController,'OnClickEvent_btn',_OnClickEvent_btn)
util.hotfix_ex(CS.HomeController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.HomeController,'OnClickHomeAVG',_OnClickHomeAVG)




