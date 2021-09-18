local util = require 'xlua.util'
xlua.private_accessible(CS.CommonLive2DController)

local SetScenePos_New = function(self)
	local selfPath = CS.Data.GetLive2DPath(self.transform);
	--CS.NDebug.LogError("SetScenePos_New"..selfPath)
	local index = string.find(selfPath,"WeddingPlay");
	if index ~= nil then
		--print("index"..index)
		for i=0,self.currModel.live2dPosDataList.Count-1 do
			if self.currModel.live2dPosDataList[i].sceneName == "Home" and self.currModel.live2dPosDataList[i].path == "Live2DCanvas/btnPicHolder" then
				self.transform:GetComponent(typeof(CS.UnityEngine.RectTransform)).anchoredPosition = CS.UnityEngine.Vector2(self.currModel.live2dPosDataList[i].anchoredPos.x,self.currModel.live2dPosDataList[i].anchoredPos.y)
				self.currModel.transform.localScale = self.currModel.live2dPosDataList[i].scale
				return
			end
		end		
	else
		self:SetScenePos()
	end	
end

local PlayDragEndMotion_New = function(self, motionName)
	if not CS.System.String.IsNullOrEmpty(motionName) then
		local motionData = self:GetMotionDataByName(motionName, "10000")
		local res = self:PlayMotions(motionData, 3)

		if res ~= -1 then
			local n = self:getRandomNumber(0, motionData.voiceList.Length)
			self:TryPlayExpression(motionData, n)
			self:TryPlayVoice(motionData, n)
		end
	end
end

util.hotfix_ex(CS.CommonLive2DController,'SetScenePos',SetScenePos_New)
util.hotfix_ex(CS.CommonLive2DController,'PlayDragEndMotion',PlayDragEndMotion_New)



