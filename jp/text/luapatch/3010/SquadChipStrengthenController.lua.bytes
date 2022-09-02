local util = require 'xlua.util'
xlua.private_accessible(CS.SquadChipStrengthenController)

local OnClickSelectAuto = function(self)
	if CS.SquadChipListController.Instance.currentChip.level >= CS.Data.SquadChipStrengthenLevelMax() then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(190209));
		return;
	end
	self.isSelecting = true;
	CS.SquadChipListController.Instance:ClearFilterExceptColor();
	local listNewFood = {};
	--避免lua排序
	local listNewFood2Star = {};
	local listNewFood3Star = {};
	local listNewFood4Star = {};
	for i=0, CS.GameData.listSquadChip.Count - 1 do
		if self:AutoSelectFoodFilter(CS.GameData.listSquadChip[i]) and CS.SquadChipListController.Instance:ChipListFilter(CS.GameData.listSquadChip[i]) then
			if CS.GameData.listSquadChip[i].chipInfo.rank == 2 then
				table.insert(listNewFood2Star,CS.GameData.listSquadChip[i]);
			elseif CS.GameData.listSquadChip[i].chipInfo.rank == 3 then
				table.insert(listNewFood3Star,CS.GameData.listSquadChip[i]);
			elseif CS.GameData.listSquadChip[i].chipInfo.rank == 4 then
				table.insert(listNewFood4Star,CS.GameData.listSquadChip[i]);
			end
			
		end
	end
	
	for k, v in pairs(listNewFood2Star) do
		table.insert(listNewFood,v);
	end
	for k, v in pairs(listNewFood3Star) do
		table.insert(listNewFood,v);
	end
	for k, v in pairs(listNewFood4Star) do
		table.insert(listNewFood,v);
	end
	
	local tempChip;
	self.expGet = 0;
	local sameColorRatio = CS.Data.GetInt("squad_chip_same_color_bonus") / 100;
	self.listChipFood:Clear();

	
	for key, value in pairs(listNewFood) do
		
		tempChip = value;
		if self.listChipFood:Contains(tempChip) == false then
			self.listChipFood:Add(tempChip);
			local _sameColorRatio = 1;
			if self.fakeChip.colorId == tempChip.colorId then
				_sameColorRatio = sameColorRatio;
			end
			self.expGet = self.expGet + tempChip:GetFeedExp(_sameColorRatio);
			self.fakeChip.exp = CS.SquadChipListController.Instance.currentChip.exp + self.expGet;
			self.fakeChip:UpdateData();
			if self.fakeChip.level >= CS.Data.SquadChipStrengthenLevelMax() then
				CS.CommonController.LightMessageTips(CS.Data.GetLang(190209));
				break;
			end
			
		end
	end
	self:UpdateExpData();
	CS.SquadChipListController.Instance:InitDefaultSortType(CS.SquadChipListController.UIState.Strengthen_Select);
	self:UpdateUI(true);
end

util.hotfix_ex(CS.SquadChipStrengthenController,'OnClickSelectAuto',OnClickSelectAuto)

