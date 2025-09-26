local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisChipDevelopUIController)

local CreateItems = function(self)
	local gobj = CS.ResManager.GetObjectByPath("UGUIPrefabs/Sangvis/UI_SangvisChipItem");
	for i=0,CS.GameData.listSangvisChipInfos.Count-1 do
		local chipInfo = CS.GameData.listSangvisChipInfos:GetDataByIndex(i);
		if chipInfo.id < 4000 then
			if self.dictChipPos:ContainsKey(chipInfo.id) then
				local gobjTemp = CS.UnityEngine.Object.Instantiate(gobj, self.chipHolder);
				local develop = gobjTemp:AddComponent(typeof(CS.SangvisChipDevelopItem));
				develop:InitWithChipAndPos(chipInfo,self.dictChipPos[chipInfo.id]);
			end
		end
	end
	
end

util.hotfix_ex(CS.SangvisChipDevelopUIController,'CreateItems',CreateItems)
