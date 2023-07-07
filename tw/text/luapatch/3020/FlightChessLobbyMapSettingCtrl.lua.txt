local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessLobbyMapSettingCtrl)
local _InitRightMapList = function(self,mission)
    self:InitRightMapList(mission);
    local key= "chess_mission_"..mission.id;
    local cache_num = self:GetSaveIndex(mission); 
	if self.curMapIndex == cache_num then
        CS.Data.DelKeyFromPlayerPref(key);
        CS.UnityEngine.PlayerPrefs.SetInt(key,self.curMapIndex);
        local num2 = CS.UnityEngine.PlayerPrefs.GetInt(key);
    end 
end
util.hotfix_ex(CS.GF.FlightChess.FlightChessLobbyMapSettingCtrl,'InitRightMapList',_InitRightMapList)