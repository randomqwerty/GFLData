local util = require 'xlua.util'
xlua.private_accessible(CS.DormGiveDressPerformanceController)


local SetPic = function(self,useSkin)
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
		local normalPic = nil;
		local skinid = 0;
		if useSkin then
			skinid = self.skinInfo.id;
		end
		if not CS.DormGiveDressPerformanceController.isNPC then
			local path = CS.CommonController.GetBigPicPath(self.gunInfo, skinid);
			normalPic = CS.ResManager.GetObjectByPath(path):GetComponent(typeof(CS.CommonPicController));
		else
			local path = CS.CommonController.GetBigPicPathByCode(self.npcInfo.code, skinid);
			normalPic = CS.ResManager.GetObjectByPath(path):GetComponent(typeof(CS.CommonPicController));
		end
		self.spritePic.sprite = normalPic.arrPic[0];
		self.materialPic:SetTexture("_AlphaTex", normalPic.arrAlphaPic[0]);
		local pixelPerUnit = self.spritePic.sprite.pixelsPerUnit;
		local texsize = self.spritePic.sprite.texture.width;
		local finalScale =1;
		local finalX = 0;
		local finalY = 0;
		local topPos = 6 +  (CS.MyMonoBehaviour.ScreenHeight - 1152) / (texsize * 0.5);
		local posData = normalPic:GetCurrentPosData("Dorm", "GiveNewDress");
		if posData == nil then
			finalScale = normalPic.transform.localScale.x / 1.5;
			finalScale = finalScale*1024 / texsize;
			local size = texsize * finalScale / pixelPerUnit;
			finalX = (187 + normalPic.transform.localPosition.x) * self.spritePic.transform.parent.localScale.x * finalScale / pixelPerUnit;
			finalY = topPos - size / 2 + normalPic.transform.localPosition.y * self.spritePic.transform.parent.localScale.x * finalScale / pixelPerUnit;
		else
			CS.NDebug.LogBlue(normalPic.gameObject.name,"找到posData", posData.scale, "sizeDelta", posData.sizeDelta, "pos", posData.pos);
			finalScale = posData.scale.x / 1.5;
			finalScale = finalScale*posData.sizeDelta.x / texsize;
			local size = texsize * finalScale / pixelPerUnit;
			finalX = (187 + posData.pos.x) * self.spritePic.transform.parent.localScale.x * finalScale / pixelPerUnit;
			finalY = topPos - size / 2 + posData.pos.y * self.spritePic.transform.parent.localScale.x * finalScale / pixelPerUnit;
		end
		self.spritePic.transform.localScale = CS.UnityEngine.Vector3(finalScale,finalScale,1);
		self.spritePic.transform.localPosition = CS.UnityEngine.Vector3(finalX,finalY,0);
	else
		self:SetPic(useSkin);
	end
end

util.hotfix_ex(CS.DormGiveDressPerformanceController,'SetPic',SetPic)