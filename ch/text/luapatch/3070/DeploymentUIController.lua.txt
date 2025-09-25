local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)


local RefreshItemUI = function(self)
	self:RefreshItemUI();
	if self.itemShowObj == nil or self.itemShowObj:isNull() then
		return;
	end
	local name = self.itemShowObj.name;
	if self:Is1ItemObj(name) or self:IsItemsObj(name) then
		return;
	end
	local ButtonTrans = self.itemShowObj.transform:Find("TipsButton");
	if ButtonTrans == nil then
		return;
	end
	local button = ButtonTrans:GetComponent(typeof(CS.ExButton));
	local url = ButtonTrans:Find("URL"):GetComponent(typeof(CS.ExText)).text;
	button.onClick:RemoveAllListeners();
	button:AddOnClick(function()
		CS.OPSWebWindows.Show(url);
	end)
end

util.hotfix_ex(CS.DeploymentUIController,'RefreshItemUI',RefreshItemUI)
