local util = require 'xlua.util'
xlua.private_accessible(CS.RewardBoxController)

local ShowNormalReward = function(self,content,handler,title,subTitle,isMallReward,allowLimit);
	self:ShowNormalReward(content,handler,title,subTitle,isMallReward,allowLimit);
	local show = false;
	local num1 = CS.GameData.GetItem(9021);
	local num2 = CS.GameData.GetItem(9022);
	local num3 = CS.GameData.GetItem(9023);
	local num4 = CS.GameData.GetItem(9024);
	local num5 = CS.GameData.GetItem(9025);
	local num1Add = 0;
	local num2Add = 0;
	local num3Add = 0;
	local num4Add = 0;
	local num5Add = 0;	
	for i=0,content.listItemPackage.Count -1 do
		local package = content.listItemPackage[i];
		if package.info.id == 9021 then
			show = true;
			num1Add = package.amount;
			num1 = num1-num1Add;
		elseif  package.info.id == 9022 then
			show = true;
			num2Add = package.amount;
			num2 = num2-num2Add;
		elseif  package.info.id == 9023 then
			show = true;
			num3Add = package.amount;
			num3 = num3-num3Add;
		elseif  package.info.id == 9024 then
			show = true;
			num4Add = package.amount;
			num4 = num4-num4Add;
		elseif  package.info.id == 9025 then
			show = true;
			num5Add = package.amount;
			num5 = num5-num5Add;
		end
	end
	if show then
		local map = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/ZLSR_AbilityUp"), self.transform, false);
		local Ability1 = map.transform:Find("Frame/Ability1");
		local Ability2 = map.transform:Find("Frame/Ability2");
		local Ability3 = map.transform:Find("Frame/Ability3");
		local Ability4 = map.transform:Find("Frame/Ability4");
		local Ability5 = map.transform:Find("Frame/Ability5");
		if (num1+num1Add)>99 then
			Ability1:Find("Text_Num").gameObject:SetActive(false);
			Ability1:Find("Img_Max").gameObject:SetActive(true);
		else		
			local text = Ability1:Find("Text_Num"):GetComponent(typeof(CS.ExText));
			local check = Ability1:Find("AbilityUp");
			if num1Add > 0 then
				check.gameObject:SetActive(true);
				text.text = tostring(num1).."<color=#00BDD6FF>+"..tostring(num1Add).."</color>";
			else
				check.gameObject:SetActive(false);
				text.text = tostring(num1);
			end			
		end
		if (num2+num2Add)>99 then
			Ability2:Find("Text_Num").gameObject:SetActive(false);
			Ability2:Find("Img_Max").gameObject:SetActive(true);
		else		
			local text = Ability2:Find("Text_Num"):GetComponent(typeof(CS.ExText));
			local check = Ability2:Find("AbilityUp");
			if num2Add > 0 then
				check.gameObject:SetActive(true);
				text.text = tostring(num2).."<color=#00BDD6FF>+"..tostring(num2Add).."</color>";
			else
				check.gameObject:SetActive(false);
				text.text = tostring(num2);
			end			
		end
		if (num3+num3Add)>99 then
			Ability3:Find("Text_Num").gameObject:SetActive(false);
			Ability3:Find("Img_Max").gameObject:SetActive(true);
		else		
			local text = Ability3:Find("Text_Num"):GetComponent(typeof(CS.ExText));
			local check = Ability3:Find("AbilityUp");
			if num3Add > 0 then
				check.gameObject:SetActive(true);
				text.text = tostring(num3).."<color=#00BDD6FF>+"..tostring(num3Add).."</color>";
			else
				check.gameObject:SetActive(false);
				text.text = tostring(num3);
			end			
		end
		if (num4+num4Add)>99 then
			Ability4:Find("Text_Num").gameObject:SetActive(false);
			Ability4:Find("Img_Max").gameObject:SetActive(true);
		else		
			local text = Ability4:Find("Text_Num"):GetComponent(typeof(CS.ExText));
			local check = Ability4:Find("AbilityUp");
			if num4Add > 0 then
				check.gameObject:SetActive(true);
				text.text = tostring(num4).."<color=#00BDD6FF>+"..tostring(num4Add).."</color>";
			else
				check.gameObject:SetActive(false);
				text.text = tostring(num4);
			end			
		end
		if (num5+num5Add)>99 then
			Ability5:Find("Text_Num").gameObject:SetActive(false);
			Ability5:Find("Img_Max").gameObject:SetActive(true);
		else		
			local text = Ability5:Find("Text_Num"):GetComponent(typeof(CS.ExText));
			local check = Ability5:Find("AbilityUp");
			if num5Add > 0 then
				check.gameObject:SetActive(true);
				text.text = tostring(num5).."<color=#00BDD6FF>+"..tostring(num5Add).."</color>";
			else
				check.gameObject:SetActive(false);
				text.text = tostring(num5);
			end			
		end
	end
end

util.hotfix_ex(CS.RewardBoxController,'ShowNormalReward',ShowNormalReward)
