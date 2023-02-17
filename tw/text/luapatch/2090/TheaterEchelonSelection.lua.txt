local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterEchelonSelection)

local OnSelectFairy = function(self,fairy)
	self:OnListReturn();
    if self.curEditSlot ~= nil and self.curEditSlot.dataType == CS.TheaterFormationRectItem.DataType.Fairy and self.fairyListIsAlter then
    if fairy == nil then
        CS.TheaterTeamData.instance:RemoveAlterFairy(self.curEditSlot.cellId);
    else
        CS.TheaterTeamData.instance:AddAlterFairy(self.curEditSlot.cellId, fairy);
    end
    CS.TheaterTeamData.instance:ArrangeAlterFairy();
    self:RefreshExtraUI();
    self:RefreshBossScore();
    else
        if CS.UISimulatorFormation.isExist then
            CS.FormationFairyLabelController.Instance:TeamFairy(fairy);
            CS. UISimulatorFormation.Instance.goFormation:SetActive(true);
        else
            CS.TheaterTeamData.instance:SetFairy(fairy);
            self:RefreshTeamList();
        end
    end

    self.curEditSlot = nil;
end
local	InitUI=function(self)
	self:InitUI();
	local	txtUI=self.transform:Find("Right/TheaterEchelonSelectionEnemyInfo/Top_Filter/Btn_Normal/UI_Text");
	local	txt=txtUI:GetComponent(typeof(CS.ExText));
	txt.text=CS.Data.GetLang(210105);
	local	txtUI1=self.transform:Find("Right/TheaterEchelonSelectionEnemyInfo/Top_Filter/Btn_ACE/Title/UI_Text");
	local	txt1=txtUI1:GetComponent(typeof(CS.ExText));
	txt1.text=CS.Data.GetLang(210104);
end
util.hotfix_ex(CS.TheaterEchelonSelection,'OnSelectFairy',OnSelectFairy)
util.hotfix_ex(CS.TheaterEchelonSelection,'InitUI',InitUI)