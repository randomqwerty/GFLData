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
util.hotfix_ex(CS.HomeController,'CheckNewShop',_CheckNewShop)
util.hotfix_ex(CS.HomeController,'OnClickEvent_btn',_OnClickEvent_btn)



