local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionBase)

local Va11EventOpen = function()
	if CS.OPSConfig.ContainCampaigns:Contains(-32) then
		local stamp = CS.GameData.GetCurrentTimeStamp();
		if stamp >= CS.OPSConfig.startTime and stamp < CS.OPSConfig.endTime then
			return true;
		end
		stamp = nil;
	end
	return false;
end

local CheckPointCost = function(self)
	if not Va11EventOpen() then
		self:CheckPointCost();
		return;
	end	
	local iter = self.currentMissionInfo.PointCose:GetEnumerator()     
	while iter:MoveNext() do                      
		local item = iter.Current.Key;
		local num = iter.Current.Value;
		local realNum = CS.OPSPanelController.Instance.item_use[item].itemRealNum;
		if realNum == 0 or realNum < num then
			CS.CommonController.ConfirmBox(CS.Data.GetLang(230011),function()
					CS.CommonController.GotoScene("Dorm", 20004)
				end)
			return;
		end                    
	end	
	CS.OPSPanelController.Instance:ShowUnclockMessageBox(self);
end


util.hotfix_ex(CS.OPSPanelMissionBase,'CheckPointCost',CheckPointCost)
