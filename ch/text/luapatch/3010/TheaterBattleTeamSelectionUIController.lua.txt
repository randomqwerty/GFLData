local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterBattleTeamSelectionUIController)

local _CreateSquadList = function(self)
	for i=0,self.listTeamSquadUIItem.Count-1 do
		CS.UnityEngine.Object.Destroy(self.listTeamSquadUIItem[i].gameObject)
	end
	self.listTeamSquadUIItem:Clear();
	self:CreateSquadList();
	
end

local Start = function(self)
	self:Start();
	local txtoff = self.transform:Find("Left/Holder/TheaterFormationTile/Panel/ChangeCaptain/Off/Tex_Information");
	local txton = self.transform:Find("Left/Holder/TheaterFormationTile/Panel/ChangeCaptain/On/Tex_Information");
	if txtoff ~= nil then
		txtoff:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(210300);
	end
	if txton ~= nil then
		txton:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(210300);
	end
end

util.hotfix_ex(CS.TheaterBattleTeamSelectionUIController,'CreateSquadList',_CreateSquadList)
util.hotfix_ex(CS.TheaterBattleTeamSelectionUIController,'Start',Start)