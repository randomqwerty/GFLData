local util = require 'xlua.util'
xlua.private_accessible(CS.OPSWebWindows)

local Show = function(url)
	if CS.OPSWebWindows.Instance == nil or CS.OPSWebWindows.Instance:isNull() then
		local web = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/BattleWebWindow"));
		CS.OPSWebWindows.Instance = web:AddComponent(typeof(CS.OPSWebWindows));
	end
	CS.OPSWebWindows.Instance:OpenAnnouncement(url);
end

local OpenAnnouncement = function(self,url)
	self:OpenAnnouncement(url);
	self.transform:Find("ImageBlock").gameObject:AddComponent(typeof(CS.ImageBufferBlurRefraction));
	local btn = self.transform:Find("ShowArea").gameObject:AddComponent(typeof(CS.ExButton));
	btn:AddOnClick(function()
		self:CloseAnnouncement();
	end);
end

util.hotfix_ex(CS.OPSWebWindows,'Show',Show)
util.hotfix_ex(CS.OPSWebWindows,'OpenAnnouncement',OpenAnnouncement)

