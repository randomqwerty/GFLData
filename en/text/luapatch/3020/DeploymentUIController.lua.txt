local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)
xlua.private_accessible(CS.DeploymentController)

local ShowRougeUI = function(self,skills)
	if self.showRougeUI then
		return;
	end
	CS.DeploymentPlanModeController.CancelPlan();
	if self.rougeUI == nil or  self.rougeUI:isNull() then
		self.rougeUI = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2023RougeSpring_BuffSelector"), CS.DeploymentUIController.Instance.transform, false);
	end
	CS.CommonAudioController.PlayUI("UI_23Spring_Card_Show");
	self.showRougeUI = true;
	self.rougeUI.gameObject:SetActive(true);
	local parent = self.rougeUI.transform:Find("MainFrame/CardList/CardLayout");
	while parent.childCount < skills.Count do
		local child = CS.UnityEngine.Object.Instantiate(parent:GetChild(0).gameObject);
		child.transform:SetParent(parent,false);
	end
	for i=0,parent.childCount-1 do
		local child = parent:GetChild(i);
		if i<skills.Count then
			child.gameObject:SetActive(true);
			local txtName = child:Find("Name/Tex_Name"):GetComponent(typeof(CS.ExText));
			txtName.text = skills[i].skill.name;
			local imageIcon = child:Find("Img_Icon"):GetComponent(typeof(CS.ExImage));
			imageIcon.sprite = CS.CommonController.LoadPngCreateSprite("Pics/Icons/Enemy/"..skills[i].uicfg.iconCode);
			local txtDec = child:Find("Description/Tex_Description"):GetComponent(typeof(CS.ExText));
			txtDec.text = skills[i].skill.description;
			local btnBg = child:Find("Img_Bg"):GetComponent(typeof(CS.ExButton));
			child:Find("OnSelect").gameObject:SetActive(false);
			child:Find("TouchArea").gameObject:SetActive(false);
			btnBg.onClick:RemoveAllListeners();
			btnBg:AddOnClick(function()
				for j=0,parent.childCount-1 do
					parent:GetChild(j):Find("OnSelect").gameObject:SetActive(false);
				end
				child:Find("OnSelect").gameObject:SetActive(true);	
				child:Find("TouchArea").gameObject:SetActive(true);
				CS.CommonAudioController.PlayUI("UI_23Spring_Card_Select");
			end)
			local btnSelect = child:Find("TouchArea"):GetComponent(typeof(CS.ExButton));
			btnSelect.onClick:RemoveAllListeners();
			btnSelect:AddOnClick(function()
					skills[i]:RequestGameCastSkill(true);
					self:CloseRougeUI();
					CS.CommonAudioController.PlayUI("UI_23Spring_Card_Get");
				end)
		else
			child.gameObject:SetActive(false);
		end
	end
end

util.hotfix_ex(CS.DeploymentUIController,'ShowRougeUI',ShowRougeUI)



