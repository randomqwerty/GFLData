local util = require 'xlua.util'
xlua.private_accessible(CS.CommonVideoPlayer)
local endBG = 0;
local OnVideoPlayEnd = function()
	if CS.AVGController.inst~=nil and not CS.AVGController.inst:isNull() then
		CS.AVGController.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = true;
	end
end

Start = function()
	print('play video2');
	if self.transform.childCount > 0 then
		local videoCode = self.transform:GetChild(0).name;
		local avgcanvas = CS.AVGController.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.Canvas));
		CS.CommonVideoPlayer.PlayVideo(CS.CommonVideoPlayer.GetFilePathVideo(videoCode),OnVideoPlayEnd,false,true,false,false,"",false,false);
		local vodeocanvas = CS.CommonVideoPlayer.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.Canvas));
		vodeocanvas.sortingLayerName = avgcanvas.sortingLayerName;
		vodeocanvas.sortingOrder = avgcanvas.sortingOrder+1;
		CS.AVGController.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = false;
		if CS.CommonSidebarController.exists then
			CS.CommonController.Invoke(function()
				CS.CommonVideoPlayer.Instance.canvasScaler.referenceResolution = CS.UnityEngine.Vector2(CS.Utility.rr * 2048, 1536);
			end,0.5,self);
		end
	end
	
end