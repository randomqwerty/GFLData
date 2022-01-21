local util = require 'xlua.util'
xlua.private_accessible(CS.CommonStorageFullConfirmBoxController)

local InitUI = function(self)
	self:InitUI();
	self.transform:Find("Frame/Selection/Expansion/Confirm/Tex_Confirm"):GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(1754);
	self.transform:Find("Frame/Selection/Recycle/Confirm/Tex_Confirm"):GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(1755);
	self.transform:Find("Frame/Selection/Strengthen/Confirm/Tex_Confirm"):GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(1755);
	local canvas = self.gameObject:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = 31;
	
end
util.hotfix_ex(CS.CommonStorageFullConfirmBoxController,'InitUI',InitUI)

