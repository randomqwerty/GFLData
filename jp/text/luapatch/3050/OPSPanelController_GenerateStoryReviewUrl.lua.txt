local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.UniWebView)
xlua.private_accessible(CS.ShowUrlMessage)
local GenerateStoryReviewUrl = function(self)
	local url = self:GenerateStoryReviewUrl()
	if not CS.System.String.IsNullOrEmpty(url) then
		return url..'&channel=game'
	end
	return url
end

local CreateWebViewInst = function()
	CS.ShowUrlMessage.CreateWebViewInst();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		CS.UniWebView.SetJavaScriptEnabled(true);
	end
end
local CloseWindows = function()
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		if CS.ShowUrlMessage._webView ~= nil then
			CS.ShowUrlMessage._webView:Stop();
			CS.UniWebView.ClearCookies();
		end
	end
	CS.ShowUrlMessage.CloseWindows();
end
util.hotfix_ex(CS.OPSPanelController,'GenerateStoryReviewUrl',GenerateStoryReviewUrl)
util.hotfix_ex(CS.ShowUrlMessage,'CreateWebViewInst',CreateWebViewInst)
util.hotfix_ex(CS.ShowUrlMessage,'CloseWindows',CloseWindows)