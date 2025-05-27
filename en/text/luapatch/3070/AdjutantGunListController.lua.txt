local util = require 'xlua.util'
xlua.private_accessible(CS.AdjutantGunListController)

local mInitUIElements = function(self)
	if self.btnCollect ==nil then
		self.btnFliter:AddOnClick(function()
			self:OnClickFilter();
		end)
		self.btnFliterAll:AddOnClick(function()
			self:OnClickFilterButton(0)
		end)
        self.btnFliterHandGun:AddOnClick(function()
			self:OnClickFilterButton(1)
		end)
        self.btnFliterSubmachinegun:AddOnClick(function()
			self:OnClickFilterButton(2)
		end)
        self.btnFliterSniperRifle:AddOnClick(function()
			self:OnClickFilterButton(3)
		end)
        self.btnFliterAssaultRifle:AddOnClick(function()
			self:OnClickFilterButton(4)
		end)
        self.btnFliterMachinegun:AddOnClick(function()
			self:OnClickFilterButton(5)
		end)
        self.btnFliterShotgun:AddOnClick(function()
			self:OnClickFilterButton(6)
		end)
        self.btnFilterReset:AddOnClick(function()
			self:OnClickRest();
		end)
        self.btnFilterConfirm:AddOnClick(function()
			self:OnClickSure(true);
		end)

		self.btnSort:AddOnClick(function()
			self:OnClickSort();
		end)
        self.btnSortSkin:AddOnClick(function()
			self:OnClickSortBotton(1);
		end)
        self.btnSortID:AddOnClick(function()
			self:OnClickSortBotton(2);
		end)


        self.toggleByCharacter.onValueChanged:AddListener(function(isOn)
			self:OnToggleValueChanged(isOn);
		end)
        self.toggleByCharacter.isOn = false;
        self.goSortHolder:SetActive(false);

        self.goFliter:SetActive(false);
        self.goFairyFliterNew:SetActive(false);
        self.txCurrentFilter.gameObject:SetActive(true);
        self.oldFilterAll:SetActive(false);

	else
		self:InitUIElements();
	end	
end

util.hotfix_ex(CS.AdjutantGunListController,'InitUIElements',mInitUIElements)
