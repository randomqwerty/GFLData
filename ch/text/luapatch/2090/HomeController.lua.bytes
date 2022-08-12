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
	CheckOPSTime(self);
	local parent = self.btnTheater.transform.parent;
	local rectTrans = parent:GetComponent(typeof(CS.UnityEngine.RectTransform));
	rectTrans.sizeDelta = CS.UnityEngine.Vector2(930,160);
end

local _OnClickHomeAVG = function(self)	
	if self.adjutantController.adjutantInfo2 == nil then
		--CS.NDebug.LogError("_OnClickHomeAVG")
        self.adjutantController:UpdateAdjutant(self.adjutantController.adjutantInfo);
    end

	self:OnClickHomeAVG();
end

opsShowTime = 0;
opsEnterTime = 0;
opsDispearTime = 0;
function CheckOPSTime(self)
	local temp = CS.Data.GetString("2022_bikini_time");
	if CS.System.String.IsNullOrEmpty(temp) then
		return;
	end
	local times =Split(temp,",");	
	opsShowTime = tonumber(times[1]);
	opsEnterTime = tonumber(times[2]);
	opsDispearTime = tonumber(times[3]);
	print("opsShowTime"..opsShowTime);
	print("opsEnterTime"..opsEnterTime);
	print("opsDispearTime"..opsDispearTime);
	local stamp = CS.GameData.GetCurrentTimeStamp();
	if stamp>opsShowTime and stamp<opsDispearTime then
		local parent = self.btnTheater.transform.parent;
		local obj = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Prefabs/2022BikiniResultEntrance"), parent, false);
		local unclock = obj.transform:Find("Img_Unlocked");
		unclock.gameObject:SetActive(stamp>opsEnterTime);
		local clock = obj.transform:Find("Img_Locked");
		clock.gameObject:SetActive(stamp<opsEnterTime);
		local btn = obj:GetComponent(typeof(CS.ExButton));
		btn:AddOnClick(function()
				EnterOPS();
			end)
	end
end

function EnterOPS()
	if opsEnterTime<CS.GameData.GetCurrentTimeStamp() then
		CS.OPSConfig.Instance:GoToScene(-52);
	else
		local dateTime = CS.GameData.UnixToDateTime(opsEnterTime);
		local time = tostring(dateTime.Month).."/"..tostring(dateTime.Day);
		local txt = tostring(CS.System.String.Format(CS.Data.GetLang(60348),time));
		CS.CommonController.LightMessageTips(txt);		
	end
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
util.hotfix_ex(CS.HomeController,'CheckNewShop',_CheckNewShop)
util.hotfix_ex(CS.HomeController,'OnClickEvent_btn',_OnClickEvent_btn)
util.hotfix_ex(CS.HomeController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.HomeController,'OnClickHomeAVG',_OnClickHomeAVG)




