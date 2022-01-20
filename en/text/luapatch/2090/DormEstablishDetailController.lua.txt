local util = require 'xlua.util'
xlua.private_accessible(CS.DormEstablishDetailController)
local QuickBuildByItemId = function(self,quickItemType)
	if self.establish ~= nil then
		local remainTime = CS.UnityEngine.Mathf.Max(self.establish.produceEndTime - CS.GameData.GetCurrentTimeStamp(), 0);
		local costItem = CS.Data.GetQuickAccelerateWriteInfo(remainTime);
		if quickItemType - 1 < costItem.Count then
			local count = costItem[quickItemType - 1].Value;
			local costItemId = costItem[quickItemType - 1].Key;
			local itemName = CS.GameData.listItemInfo:GetDataById(costItem[quickItemType - 1].Key).name;
			local reportName = "";
			if self.establish.isSpReport then
				reportName = CS.Data.GetLang(190156);
			else
				reportName = CS.Data.GetLang(190155);
			end
			local title = tostring(CS.System.String.Format(CS.Data.GetLang(31935),tostring(count),itemName,reportName));
			CS.CommonController.ConfirmBox(title,function()
				self:RequestBuildEnd(quickItemType);
			end)
		end
	end
end

util.hotfix_ex(CS.DormEstablishDetailController,'QuickBuildByItemId',QuickBuildByItemId)
