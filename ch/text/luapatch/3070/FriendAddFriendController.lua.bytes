local util = require 'xlua.util'
xlua.private_accessible(CS.FriendAddFriendController)

local OnClickSearchID = function(self)
	local uid = tonumber(self.inputField.text)
	print('uid', uid)
	if uid == nil then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(200093));
		return
	end
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		-- 多服模式
		local createConnection = xlua.get_generic_method(CS.ConnectionController, 'CreateConnection');
		local createRequest = createConnection(CS.RequestSearchAllFriendZone);
		createRequest(CS.RequestSearchAllFriendZone(uid), function(req)
			CS.GameData.listSearchFriend:RemoveAll(function(f)
				return f.uid == CS.GameData.userInfo.userId and f.zoneid == CS.GameData.userInfo.zoneId
			end)
			self:RequestSearchAllFriendZoneHandle()
		end)
	else
		-- 单服模式
		if uid == CS.GameData.userInfo.userId then
            CS.CommonController.LightMessageTips(CS.Data.GetLang(110016));
			return
		end
		CS.FriendUserCardController.ShowUserCard(uid)
	end
end
xlua.hotfix(CS.FriendAddFriendController,'OnClickSearchID',OnClickSearchID)
