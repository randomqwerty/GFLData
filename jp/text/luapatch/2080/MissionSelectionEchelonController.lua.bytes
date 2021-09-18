local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionEchelonController)

local ShowTeamInfo = function(self,Id)
	if self.selectionType == 1 then
		for i = 1, CS.GameData.userInfo.maxTeam do
			--用影响格字段判断是否是人形梯队
			if CS.GameData.dictTeam[i].CostRes == nil then
				print(CS.GameData.dictTeam[i].CostRes);
				--梯队中是否所有人形都是可出战状态
				local allAvailable = true;
				if CS.GameData.dictTeam[i].listGun.Count == 0 then
					allAvailable = false;
				else
					for j = 0, CS.GameData.dictTeam[i].listGun.Count-1 do
						if CS.GameData.dictTeam[i].listGun[j].life <= 0 or CS.GameData.dictTeam[i].listGun[j].status ~= CS.GunStatus.normal then
							allAvailable = false;
							break;
						end
					end
				end
				--如果该梯队能用，则走原逻辑。否则继续循环
				if allAvailable then
					self:ShowTeamInfo(Id);
					return;
				end
			end
		end
		--循环走完到这里说明没有梯队可用，弹提示
		CS.CommonController.LightMessageTips(CS.Data.GetLang(100046));
	else
		self:ShowTeamInfo(Id);
	end
end

util.hotfix_ex(CS.MissionSelectionEchelonController,'ShowTeamInfo',ShowTeamInfo)