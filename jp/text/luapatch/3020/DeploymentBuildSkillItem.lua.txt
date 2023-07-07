local util = require 'xlua.util'
xlua.private_accessible(CS.BuildSkillDetail)

local CheckCost = function(self)
	if self.skill.apCost>0 then
		CS.GameData.missionAction.ap = CS.GameData.missionAction.ap-self.skill.apCost;
	end
	if self.skill.itemCose.Keys.Count>0 then
		local iter = self.skill.itemCose:GetEnumerator()
		while iter:MoveNext() do
			local itemid = iter.Current.Key;
			local costnum = iter.Current.Value;
			local totalnum = CS.GameData.GetItem(itemid);
			local resnum = totalnum - costnum;
			if resnum<0 then
				CS.GameData.SetItem(itemid, 0);
			else
				CS.GameData.SetItem(itemid, resnum);
			end
		end
	end
end
local RefreshUI = function(self)
	self:CheckItemCost();
end

local RefreshLeftUI = function(self)
	self:RefreshLeftUI();
	self.btnSkill.gameObject:SetActive(true);
	self.btnSkillCancelLeft.gameObject:SetActive(false);
end
local buildSkill = nil;
local ControlBuild = function(self)
	if self.buildSkill.skill.id == 610001 then
		buildSkill = self.buildSkill;
		ShowRougeSummerUI();
		return;
	end
	self:ControlBuild();
end
local RougeSummerObj = nil; 
local selectItems = nil;
Item1id = 9041;
Item2id = 9042;
function item1Selectnnum()
	local num=0;
	if selectItems.Count == 1 then
		local item1 = selectItems[0];
		if item1 == Item1id then
			num = 1;
		end
	elseif selectItems.Count == 2 then
		local item1 = selectItems[0];
		local item2 = selectItems[1];
		if item1 == Item1id then
			num = num + 1;
		end
		if item2 == Item1id then
			num = num + 1;
		end
	end
	return num;
end
function item2Selectnnum()
	local num=0;
	if selectItems.Count == 1 then
		local item1 = selectItems[0];
		if item1 == Item2id then
			num = 1;
		end
	elseif selectItems.Count == 2 then
		local item1 = selectItems[0];
		local item2 = selectItems[1];
		if item1 == Item2id then
			num = num + 1;
		end
		if item2 == Item2id then
			num = num + 1;
		end
	end
	return num;
end
function ShowRougeSummerUI()
	if selectItems == nil then
		selectItems = CS.System.Collections.Generic.List(CS.System.Int32)();
	end
	if RougeSummerObj == nil or RougeSummerObj:isNull() then
		selectItems:Clear();		
		RougeSummerObj = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityRes/2023RougeSummer_BuffMixer"));
		local btnItem1 = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_1/TouchArea");
		btnItem1:GetComponent(typeof(CS.ExButton)):AddOnClick(function()
			if selectItems.Count>1 then
				return;
			end
			local itemnum = CS.GameData.GetItem(Item1id);
			itemnum = itemnum - item1Selectnnum();	
			if itemnum == 0 then
				return;	
			end
			selectItems:Add(Item1id);
			ShowRougeSummerUI();
		end);
		local btnItem2 = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_2/TouchArea");
		btnItem2:GetComponent(typeof(CS.ExButton)):AddOnClick(function()
			if selectItems.Count>1 then
				return;
			end
			local itemnum = CS.GameData.GetItem(Item2id);
			itemnum = itemnum - item2Selectnnum();
			if itemnum == 0 then
				return;
			end
			selectItems:Add(Item2id);
			ShowRougeSummerUI();
		end);
		local mixParent = RougeSummerObj.transform:Find("MainFrame/Mixer/Img_Container/ItemLayout");
		mixParent:Find("Item1_L"):GetComponent(typeof(CS.ExButton)):AddOnClick(function()
				selectItems:Remove(Item1id);
				ShowRougeSummerUI();	
			end);
		mixParent:Find("Item1_R"):GetComponent(typeof(CS.ExButton)):AddOnClick(function()
				selectItems:Remove(Item1id);
				ShowRougeSummerUI();
			end);
		mixParent:Find("Item2_L"):GetComponent(typeof(CS.ExButton)):AddOnClick(function()
				selectItems:Remove(Item2id);
				ShowRougeSummerUI();
			end);
		mixParent:Find("Item2_R"):GetComponent(typeof(CS.ExButton)):AddOnClick(function()
				selectItems:Remove(Item2id);
				ShowRougeSummerUI();
			end);
		local btnskill = RougeSummerObj.transform:Find("MainFrame/Btn_Confirm");
		btnskill:GetComponent(typeof(CS.ExButton)):AddOnClick(function()
				CastSkill();
			end);
		local bg = RougeSummerObj.transform:Find("MainFrame/Img_Bg");
		bg.gameObject:AddComponent(typeof(CS.ExButton)):AddOnClick(function()
				CS.UnityEngine.Object.Destroy(RougeSummerObj);
			end);
		local btnInfo = RougeSummerObj.transform:Find("MainFrame/Output/Img_Info");
		local url = btnInfo:Find("URL"):GetComponent(typeof(CS.ExText)).text;
		btnInfo.gameObject:GetComponent(typeof(CS.ExButton)):AddOnClick(function()
				CS.OPSWebWindows.Show(url);
			end);
		local item1Info = CS.GameData.listItemInfo:GetDataById(Item1id);
		local item2Info = CS.GameData.listItemInfo:GetDataById(Item2id);
		local txtNameItem1 = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_1/Img_NameBg/Tex_Name");
		txtNameItem1:GetComponent(typeof(CS.ExText)).text = item1Info.name;
		local txtNameItem2 = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_2/Img_NameBg/Tex_Name");
		txtNameItem2:GetComponent(typeof(CS.ExText)).text = item2Info.name;
		local imageItem1 = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_1/Img_IconBg/Img_Icon");
		imageItem1:GetComponent(typeof(CS.ExImage)).sprite = CS.CommonController.LoadPngCreateSprite(item1Info.codePath);
		local imageItem2 = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_2/Img_IconBg/Img_Icon");
		imageItem2:GetComponent(typeof(CS.ExImage)).sprite = CS.CommonController.LoadPngCreateSprite(item2Info.codePath);
	end
	local item1num = CS.GameData.GetItem(Item1id);
	local item2num = CS.GameData.GetItem(Item2id);
	item1num = item1num - item1Selectnnum();
	item2num = item2num - item2Selectnnum();
	RougeSummerObj:SetActive(true);
	local item1Parent = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_1/Container/ItemLayout");
	local item2Parent = RougeSummerObj.transform:Find("MainFrame/CardList/ItemCard_2/Container/ItemLayout");
	for i=0,item1num-1 do
		if item1Parent.childCount<=i then
			local child = CS.UnityEngine.Object.Instantiate(item1Parent:GetChild(0).gameObject);
			child.transform:SetParent(item1Parent,false);
		end		
	end
	for i=0,item2num-1 do
		if item2Parent.childCount<=i then
			local child = CS.UnityEngine.Object.Instantiate(item2Parent:GetChild(0).gameObject);
			child.transform:SetParent(item2Parent,false);
		end
	end
	for i=0,item1Parent.childCount-1 do
		local child= item1Parent:GetChild(i);
		local show = i < item1num;
		child.gameObject:SetActive(show);
	end
	for i=0,item2Parent.childCount-1 do
		local child= item2Parent:GetChild(i);
		local show = i < item2num;
		child.gameObject:SetActive(show);
	end
	local mix = RougeSummerObj.transform:Find("MainFrame/Mixer/Img_Container/ItemLayout");
	local Item1L = mix:Find("Item1_L");
	local Item1R = mix:Find("Item1_R");
	local Item2L = mix:Find("Item2_L");
	local Item2R = mix:Find("Item2_R");
	Item1L.gameObject:SetActive(false);
	Item1R.gameObject:SetActive(false);
	Item2L.gameObject:SetActive(false);
	Item2R.gameObject:SetActive(false);
	if selectItems.Count == 1 then
		local item1 = selectItems[0];
		if item1 == Item1id then
			Item1L.gameObject:SetActive(true);
		elseif item1 == Item2id then
			Item2L.gameObject:SetActive(true);
		end
	elseif selectItems.Count == 2 then
		local item1 = selectItems[0];
		local item2 = selectItems[1];
		if item1 == Item1id then
			Item1L.gameObject:SetActive(true);
		elseif item1 == Item2id then
			Item2L.gameObject:SetActive(true);
		end
		if item2 == Item1id then
			Item1R.gameObject:SetActive(true);
		elseif item2 == Item2id then
			Item2R.gameObject:SetActive(true);
		end
	end
	local missionskillid = 0;
	if selectItems.Count == 1 then
		local item1 = selectItems[0];
		if item1 == Item1id then
			missionskillid = 610011;
		elseif item1 == Item2id then
			missionskillid = 610012;
		end
	elseif selectItems.Count == 2 then
		local item1 = selectItems[0];
		local item2 = selectItems[1];
		if item1 == Item1id then
			if item2 == Item1id then
				missionskillid = 610013;
			elseif item2 == Item2id then
				missionskillid = 610015;
			end
		elseif item1 == Item2id then
			if item2 == Item1id then
				missionskillid = 610015;
			elseif item2 == Item2id then
				missionskillid = 610014;
			end
		end
	end
	local txtName = RougeSummerObj.transform:Find("MainFrame/Output/Tex_Name"):GetComponent(typeof(CS.ExText));
	local txtdec = RougeSummerObj.transform:Find("MainFrame/Output/Tex_Desc"):GetComponent(typeof(CS.ExText));
	local image = RougeSummerObj.transform:Find("MainFrame/Mixer/Img_Product"):GetComponent(typeof(CS.ExImage));
	if missionskillid == 0 then
		txtName.text = "";
		txtdec.text = "";
		image.gameObject:SetActive(false);
	else
		local skill = CS.GameData.listMissionSkillCfg:GetDataById(missionskillid);
		txtName.text = skill.name;
		txtdec.text = skill.description;
		image.gameObject:SetActive(false);
		image.sprite = CS.CommonController.LoadPngCreateSprite("Pics/Icons/Skill/Deployment/"..skill.code);
	end
	local dj = RougeSummerObj.transform:Find("MainFrame/Mixer/JBQ_jbt_dj/JBQ_jbt_djdh/JBQ_jbt_dj");
	dj.gameObject:SetActive(true);
end
local playanim = false;
function CastSkill()
	if selectItems.Count == 0 then
		return;
	end
	if playanim then
		return;
	end
	playanim = true;
	local missionskillid = 0;
	if selectItems.Count == 1 then
		local item1 = selectItems[0];
		if item1 == Item1id then
			missionskillid = 610011;
		elseif item1 == Item2id then
			missionskillid = 610012;
		end
	elseif selectItems.Count == 2 then
		local item1 = selectItems[0];
		local item2 = selectItems[1];
		if item1 == Item1id then
			if item2 == Item1id then
				missionskillid = 610013;
			elseif item2 == Item2id then
				missionskillid = 610015;
			end		
		elseif item1 == Item2id then
			if item2 == Item1id then
				missionskillid = 610015;
			elseif item2 == Item2id then
				missionskillid = 610014;
			end
		end
	end
	buildSkill.skill = CS.GameData.listMissionSkillCfg:GetDataById(missionskillid);
	buildSkill.otherskills:Clear();
	PlayAnim(true);
	CS.CommonController.Invoke(function()
			buildSkill:RequestCastSkill();
		end,5,CS.DeploymentController.Instance);
end
function PlayAnim(play)
	local image = RougeSummerObj.transform:Find("MainFrame/Mixer/Img_Product"):GetComponent(typeof(CS.ExImage));
	local dj = RougeSummerObj.transform:Find("MainFrame/Mixer/JBQ_jbt_dj/JBQ_jbt_djdh/JBQ_jbt_dj");
	local djplay = RougeSummerObj.transform:Find("MainFrame/Mixer/JBQ_jbt_dj/JBQ_jbt");
	local fix = RougeSummerObj.transform:Find("MainFrame/Mixer/Img_Container/JBQ_fx");
	local guo = RougeSummerObj.transform:Find("MainFrame/Mixer/Img_Container/JBQ_guo");
	if play then
		image.gameObject:SetActive(true);
		dj.gameObject:SetActive(false);
		djplay.gameObject:SetActive(true);
		guo.gameObject:SetActive(true);
		fix.gameObject:SetActive(true);
	else
		image.gameObject:SetActive(false);
		dj.gameObject:SetActive(true);
		djplay.gameObject:SetActive(false);
		guo.gameObject:SetActive(false);
		fix.gameObject:SetActive(false);
	end
end
local RequestControlBuild = function(self,data)
	CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
	self:RequestControlBuild(data);
	if RougeSummerObj ~= nil and not RougeSummerObj:isNull() then
		selectItems:Clear();
		PlayAnim(false);
		ShowRougeSummerUI();
		playanim = false;
	end
end

local RequestBuffControlBuild = function(self,data)
	CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
	self:RequestBuffControlBuild(data);
end
util.hotfix_ex(CS.BuildSkillDetail,'RequestControlBuild',RequestControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'RequestBuffControlBuild',RequestBuffControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'CheckCost',CheckCost)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshUI',RefreshUI)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'ControlBuild',ControlBuild)