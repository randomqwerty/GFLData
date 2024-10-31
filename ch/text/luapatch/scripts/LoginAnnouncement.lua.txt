local util = require 'xlua.util'
local model = require("AnnouncementModel")
local cache_key = "login_announcement"
local isAgree = false
local scrollBar = nil
local allRead = false
local OnClickSubmit = function()
	-- print('OnClickSubmit', isAgree)
	if isAgree then
		CS.UnityEngine.PlayerPrefs.SetInt(cache_key, model.version)
		CS.UnityEngine.Object.Destroy(self.gameObject)
	end
end

local OnClickAgree = function()
	-- print('OnClickAgree')
	if allRead then
		isAgree = not isAgree
		goChecked:SetActive(isAgree)
	else
		CS.CommonController.LightMessageTips(CS.Data.GetLang(100333))
	end
end

local OnScrollBarValueChanged = function(val)
	if not allRead and val <= 0.01 then
		allRead = true
	end
end

Awake = function()
	allRead = false
	isAgree = false
	goSubmit:GetComponent(typeof(CS.ExButton)):AddOnClick(OnClickSubmit)
	goToggle:GetComponent(typeof(CS.ExButton)):AddOnClick(OnClickAgree)
	scrollBar = goScrollRect:GetComponent(typeof(CS.UnityEngine.UI.ScrollRect)).verticalScrollbar

	model:Init()
	local cacheVersion = CS.UnityEngine.PlayerPrefs.GetInt(cache_key, 0)
	if cacheVersion >= model.version then
		allread = true
		isAgree = true
	end
end

Start = function()
	if not CS.System.String.IsNullOrEmpty(model.path) then
		local txt = CS.ResManager.GetObjectByPath(model.path, ".txt");
		if txt ~= nil then
			goText:GetComponent(typeof(CS.ExText)).text = txt.text
		end
	end
	scrollBar.onValueChanged:AddListener(OnScrollBarValueChanged)
	goChecked:SetActive(isAgree)
end