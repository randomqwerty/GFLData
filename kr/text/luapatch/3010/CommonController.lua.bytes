local util = require 'xlua.util'
xlua.private_accessible(CS.CommonController)
--修正特效匹配头像框
local LoadImageHeadFrameWithSequenceFrame = function(image,cosmeticId)
	CS.CommonController.LoadImageHeadFrameWithSequenceFrame(image,cosmeticId);
	if image == nil then
		return;
	end
	local Frame = image.transform:Find("Frame");
	if Frame.childCount > 0 then
		local effect = Frame:GetChild(0);
		local rect = image.transform:GetComponent(typeof(CS.UnityEngine.RectTransform));
		if rect ~= nil then
			local size = rect.sizeDelta.x*1.0/210;
			effect.localScale = CS.UnityEngine.Vector3(size,size,1);
		end
	end
end
local myPlayAudio = function(button)
	if button == "Cutin" then
		print("hook")
	else
		print("orgin")
		CS.CommonController.PlayAudio(button);
	end
end
util.hotfix_ex(CS.CommonController,'LoadImageHeadFrameWithSequenceFrame',LoadImageHeadFrameWithSequenceFrame)
util.hotfix_ex(CS.CommonController,'PlayAudio',myPlayAudio)



