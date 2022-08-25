local _, LuaDebuggee = pcall(require, 'LuaDebuggee')
if LuaDebuggee and LuaDebuggee.StartDebug then
	LuaDebuggee.StartDebug('127.0.0.1', 9826)
else
	print('Please read the FAQ.pdf')
end
local util = require 'xlua.util'
xlua.private_accessible(CS.StoreRoomController)
xlua.private_accessible(CS.CommonSangvisCharacterListController)
xlua.private_accessible(CS.CommonAudioController)

local myOpenSangvisBox = function(self,isOn)
	if isOn == true then
		self.sangvisButton.image.sprite = self.arrSangvisToggleSprites[1];
	else
		self.sangvisButton.image.sprite = self.arrSangvisToggleSprites[0];
	end
    if isOn == true then
		self:CloseOtherList(2);
		if CS.CommonSangvisCharacterListController.Instance ~= nil and needRefreshSangvisList == false  then
			CS.CommonSangvisCharacterListController.Instance.gameObject:SetActive(true);
			self.needRefreshSangvisList = false;
		else
			local listTrans = self.transform:Find("SangvisCharacterList(Clone)");
			if (listTrans ~= nil) then
				listTrans:GetComponent(typeof(CS.CommonSangvisCharacterListController)):RefreshList();
			else
				CS.CommonSangvisCharacterListController.CreateStorageList();
			end
			self.needRefreshSangvisList = false;
		end
		self.cancelBtn.gameObject:SetActive(false);
		self.returnHomeButton.gameObject:SetActive(true);
		CS.CommonAudioController.PlayUI(CS.AudioUI.UI_default);
	else
		self:OpenSangvisBox(isOn)
    end
end
util.hotfix_ex(CS.StoreRoomController,'OpenSangvisBox',myOpenSangvisBox)