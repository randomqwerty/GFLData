local util = require 'xlua.util'
xlua.private_accessible(CS.HomeUserInfoNewController)
xlua.private_accessible(CS.FriendPersonalCardController)
xlua.private_accessible(CS.DormUIController)
xlua.private_accessible(CS.FriendListLabelController)

local myOnClickChangeName = function(self)
	local time = CS.GameData.GetCurrentTimeStamp();
	if(time >= 1665633600 and time <= 1666843200) then
		CS.CommonController.LightMessageTips("该功能暂未开放");
	else
		self:OnClickChangeName()
	end
end
local myChangeIntro = function(self)
	local time = CS.GameData.GetCurrentTimeStamp();
	if(time >= 1665633600 and time <= 1666843200) then
		CS.CommonController.LightMessageTips("该功能暂未开放");
	else
		self:ChangeIntro()
	end
end
local myOnClickRename = function(self)
	local time = CS.GameData.GetCurrentTimeStamp();
	if(time >= 1665633600 and time <= 1666843200) then
		CS.CommonController.LightMessageTips("该功能暂未开放");
	else
		self:OnClickRename()
	end
end
local myOnClickLeaveMessage = function(self)
	local time = CS.GameData.GetCurrentTimeStamp();
	if(time >= 1665633600 and time <= 1666843200) then
		CS.CommonController.LightMessageTips("该功能暂未开放");
	else
		self:OnClickLeaveMessage()
	end
end
local myOnClickShowMessage = function(self)
	local time = CS.GameData.GetCurrentTimeStamp();
	if(time >= 1665633600 and time <= 1666843200) then
		CS.CommonController.LightMessageTips("该功能暂未开放");
	else
		self:OnClickShowMessage()
	end
end
util.hotfix_ex(CS.HomeUserInfoNewController,'OnClickChangeName',myOnClickChangeName)
util.hotfix_ex(CS.FriendPersonalCardController,'ChangeIntro',myChangeIntro)
util.hotfix_ex(CS.DormUIController,'OnClickRename',myOnClickRename)
util.hotfix_ex(CS.DormUIController,'OnClickLeaveMessage',myOnClickLeaveMessage)
util.hotfix_ex(CS.FriendListLabelController,'OnClickShowMessage',myOnClickShowMessage)