local util = require 'xlua.util'
xlua.private_accessible(CS.PicControlEffect)

local ShowOriginal = function(self)
	local image = self.transform:GetComponent(typeof(CS.UnityEngine.UI.Image));
	if image ~= nil then
		self.mat = CS.UnityEngine.Object.Instantiate(image.material);
		image.material = self.mat;
		--CS.NDebug.Log("ShowOriginal赋值",self.mat,image.material);
	end
	self:ShowOriginal();
	if self.currentEffect == CS.PicControlEffect.Effect.Tongxun then
		self.mat.shader = CS.ResManager.GetObjectByPath("Shader/UGUIAVGCommunicationBox",".shader");
	end	
end
local DoVibrate = function(self)
	local image = self.transform:GetComponent(typeof(CS.UnityEngine.UI.Image));
	if image ~= nil then
		self.mat = CS.UnityEngine.Object.Instantiate(image.material);
		image.material = self.mat;
		--CS.NDebug.Log("DoVibrate赋值",self.mat,image.material);
	end
	self:DoVibrate();
end
local ShowMessageEffect = function(self,time)
	local image = self.transform:GetComponent(typeof(CS.UnityEngine.UI.Image));
	if image ~= nil then
		self.mat = CS.UnityEngine.Object.Instantiate(image.material);
		image.material = self.mat;
		--CS.NDebug.Log("ShowMessageEffect赋值",self.mat,image.material);
	end
	self:ShowMessageEffect(time);
	self.mat.shader = CS.ResManager.GetObjectByPath("Shader/UGUIAVGCommunicationBox",".shader");
end
util.hotfix_ex(CS.PicControlEffect,'ShowOriginal',ShowOriginal)
util.hotfix_ex(CS.PicControlEffect,'DoVibrate',DoVibrate)
util.hotfix_ex(CS.PicControlEffect,'ShowMessageEffect',ShowMessageEffect)

