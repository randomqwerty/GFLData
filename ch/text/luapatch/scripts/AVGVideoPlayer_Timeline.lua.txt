local util = require 'xlua.util'
local endBG = 0;
local OnVideoPlayEnd = function()
	CS.AVGController.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = true;
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
	end
	
end