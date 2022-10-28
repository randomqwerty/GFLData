local util = require 'xlua.util'
xlua.private_accessible(CS.DormController)
xlua.private_accessible(CS.MyMonoBehaviour)
xlua.private_accessible(CS.DormSquadBarracksController)
local myDoLoadOpen = function(self)
	local newRoomPos = self:GetCurrentRoomPosition();
	local xDiff = newRoomPos.x - self.roomPosition.x;
	local yDiff = newRoomPos.y - self.roomPosition.y;
	if(CS.ResCenter.instance.lastSceneName == "MotherBase" and self.roomPosition.x == 0 and self.roomPosition.y == 0 ) then
		self.loadingDirection = CS.DormController.DormLoadingDirection.Fade;
	elseif (xDiff == 0 and yDiff == 0 and self.currentMode == CS.DormMode.Establish) then
				if (self.currentRoom == CS.EstablishRoom.Barracks) then
					if(CS.DormSquadBarracksController.instance.isPageDown ) then
						self.loadingDirection =  CS.DormController.DormLoadingDirection.Down;
					else
						self.loadingDirection =  CS.DormController.DormLoadingDirection.Up
					end
				else
					self.loadingDirection = CS.DormController.DormLoadingDirection.Fade;
				end
	elseif (xDiff == 0) then	
		if 	yDiff > 0 then
			self.loadingDirection =CS.DormController.DormLoadingDirection.Down;
		else
			self.loadingDirection =CS.DormController.DormLoadingDirection.Up;
		end		
	else	
		if 	xDiff > 0 then
			self.loadingDirection =CS.DormController.DormLoadingDirection.Right;
		else
			self.loadingDirection =CS.DormController.DormLoadingDirection.Left;
		end		
	end
	if self.loadingDirection ~= CS.DormController.DormLoadingDirection.Down and self.loadingDirection ~= CS.DormController.DormLoadingDirection.Up then
		self:DoLoadOpen()
	else
		self.roomPosition = newRoomPos;
		if(CS.CommonLoadController.allow == false) then
			CS.CommonController.InvokeAfterSteadyFrameRate(CS.CommonLoadController.CloseLoad, self);
		end
		if self.gobjRTImage ~= nil then
			if(self.loadingDirection == CS.DormController.DormLoadingDirection.Down) then
				self.gobjRTImage.gameObject:GetComponent(typeof(CS.UnityEngine.RectTransform)):DOAnchorPosY(CS.MyMonoBehaviour.ScreenHeight, 0.7):Play();
				self.dormCamera:TweenToOriginVertical(true);
			elseif(self.loadingDirection == CS.DormController.DormLoadingDirection.Up) then
				self.gobjRTImage.gameObject:GetComponent(typeof(CS.UnityEngine.RectTransform)):DOAnchorPosY(-CS.MyMonoBehaviour.ScreenHeight, 0.7):Play();
				self.dormCamera:TweenToOriginVertical(false);
			end
			self.loadingDirection = CS.DormController.DormLoadingDirection.Fade;
		end
	end 
end
util.hotfix_ex(CS.DormController,'DoLoadOpen',myDoLoadOpen)