local util = require 'xlua.util'
xlua.private_accessible(CS.RewardBoxController)

local mInitDrawIcons = function(self)
	if self.drawList~=nil and self.drawList.Count>0 then
		local index = self.drawList.Count-1
		for i=0,index do
			local package = self.drawList[i];
			local builders = package:GetMailRewardBuilders();
			for j=0,builders.Count-1 do
				local temp = CS.UnityEngine.Object.Instantiate(self.ItemPrefab)
				temp.transform:SetParent(self.listHolder, false);

				local iconholder = temp.transform:Find("IconHolder");
				local nameText = temp.transform:Find("Tex_ItemName"):GetComponent(typeof(CS.ExText));

				nameText.text = builders[j]:Build(iconholder).strTitle;
				temp:SetActive(true);
			end 
		end
	else
		self:InitDrawIcons();
	end
end
util.hotfix_ex(CS.RewardBoxController,'InitDrawIcons',mInitDrawIcons)

