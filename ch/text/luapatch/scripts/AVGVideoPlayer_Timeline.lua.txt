local util = require 'xlua.util'
local endBG = 0;
local OnVideoPlayEnd = function()
	CS.AVGController.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = true;
end

Start = function()
	print('play video');
	if self.transform.childCount > 0 then
		local videoCode = self.transform:GetChild(0).name;
		CS.CommonVideoPlayer.PlayVideo(CS.CommonVideoPlayer.GetFilePathVideo(videoCode),OnVideoPlayEnd,false,true,false,false,"",false,true);
		CS.AVGController.Instance.gameObject:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled = false;
	end
	
end