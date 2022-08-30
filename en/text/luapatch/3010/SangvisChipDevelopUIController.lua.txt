local _, LuaDebuggee = pcall(require, 'LuaDebuggee')
if LuaDebuggee and LuaDebuggee.StartDebug then
	LuaDebuggee.StartDebug('127.0.0.1', 9826)
else
	print('Please read the FAQ.pdf')
end
local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisChipDevelopUIController)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.SangvisChipDevelopMapData)
local myLoadMapConfig = function(self,level)
	local path = "ProfilesConfig/SangvisChipMap/MapData";
	self.saveLevel = level;
	if (level > 5) then
		path = string.Format("ProfilesConfig/SangvisChipMap/MapData_{0}", level);
	end
	local gobj = CS.ResManager.GetObjectByPath(path);
	self:CopyRectTransform(gobj.transform, self.dragRect);
	local transTemp1;
	local transTemp2;
	for i=0 , gobj.transform.childCount - 1 do
		transTemp1 = gobj.transform:GetChild(i);
		transTemp2 = self.dragRect:GetChild(i);
		self:CopyRectTransform(transTemp1, transTemp2);
		for j = 0, transTemp1.childCount - 1 do
			self:CopyRectTransform(transTemp1:GetChild(j), transTemp2:GetChild(j));
		end					
	end
	self.dictChipPos:Clear();
	local mapData = gobj:GetComponent(typeof(CS.SangvisChipDevelopMapData));
	for i = 0, mapData.listPosData.Count - 1 do
		local pos = mapData.listPosData[i];
		self.dictChipPos[pos.id] = pos;
	end				
	self.standardRectScale = self.dragRect.localScale.x;
	self.arrStandardTypeTextScale[0] = self.rectTransformTypeMissionTitle.localScale.x;
	self.arrStandardTypeTextScale[1] = self.rectTransformTypeSpecialTitle.localScale.x;
	self.arrStandardTypeTextScale[2] = self.rectTransformTypeHaloTitle.localScale.x;
end
util.hotfix_ex(CS.SangvisChipDevelopUIController,'LoadMapConfig',myLoadMapConfig)

