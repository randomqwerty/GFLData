local util = require 'xlua.util'
xlua.private_accessible(CS.FlightChessLobbyGashaController)
xlua.private_accessible(CS.GF.FlightChess.FlightChessLobbyMainController)
xlua.private_accessible(CS.CommanderUniform)
xlua.private_accessible(CS.Package)
local _GetPackage = function(self,source, extra, forceShowPerformance, playAnimNow,isMailReward)
	--print("_GetPackage 2"); 
	self:GetPackage(source,extra,forceShowPerformance,playAnimNow,isMailReward);
	if self.id == 94411 or self.id == 94412 or self.id == 94420 then
		--print("_GetPackage"); 
		--print(self.id); 

		if self.listUniform.Count>0 then
			local len=self.listUniform.Count;
			for i=0,len-1 do
				local u_id = self.listUniform[i];
				if CS.GameData.listCommanderUniform:ContainsKey(u_id)==false then
					local uniform = CS.CommanderUniform(u_id,"");
					uniform.getTime = CS.GameData.GetCurrentTimeStamp();

					CS.GameData.listCommanderUniform:Add(uniform,-1);
				end
			end
		end
	end
end
local ShowGashaEffect_New = function(self, gold)
	self:ShowGashaEffect(gold)
	CS.GF.FlightChess.FlightChessLobbyMainController.Instance:RefreshUI()
end

local _InitUIElements = function(self)
	util.hotfix_ex(CS.Package,'GetPackage',_GetPackage)
	self:InitUIElements()
end
local _CloseWindow = function(self)
	xlua.hotfix(CS.Package,'GetPackage',nil)
	self:CloseWindow()
end

util.hotfix_ex(CS.FlightChessLobbyGashaController,'ShowGashaEffect',ShowGashaEffect_New)
util.hotfix_ex(CS.FlightChessLobbyGashaController,'InitUIElements',_InitUIElements)
util.hotfix_ex(CS.FlightChessLobbyGashaController,'CloseWindow',_CloseWindow)
 
