local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialMissionSelectController)

local check = false;
local Init = function(self,showMissions,currentMissionInfo)
	local RollingText = self.conentRect:GetChild(0):Find("RollingText/Tex_Mission");
	if RollingText ~= nil then
		self:Init(showMissions,currentMissionInfo);
		check = true;
	else
		while self.conentRect.childCount>1 do
		 	CS.UnityEngine.GameObject.DestroyImmediate(self.conentRect:GetChild(1).gameObject);
		end
		self.conentRect:GetChild(0).gameObject:SetActive(false);
		self.textList:Clear();
		while self.conentRect.childCount < showMissions.Count+1 do
			local child = CS.UnityEngine.GameObject.Instantiate(self.conentRect:GetChild(0).gameObject).transform;
			child:SetParent(self.conentRect, false);
			child:SetAsLastSibling();
			child.gameObject:SetActive(true);
		end
		for i=0,showMissions.Count-1 do
			local child = self.conentRect:GetChild(i+1);
			child.gameObject.name = showMissions[i].id;
			local txt = child.transform:Find("Tex_Title"):GetComponent(typeof(CS.ExText));
			txt.text = showMissions[i].name;
			self.textList:Add(child);
		end
		self.itemNum = showMissions.Count;
		if self.itemNum%2 == 0 then
			self.conentLimit = (self.itemHeight + 5)/2;
		else
			self.conentLimit = 0;
		end
		--self.conentRect.anchoredPosition = CS.UnityEngine.Vector2(self.conentRect.anchoredPosition.x, self.conentLimit);
		self.itemHeight = 65 + self.conentSpacing;
		local order = showMissions:IndexOf(currentMissionInfo);
		self.offsetDown = -116;
		self.itemHeight_min = self.offsetDown;
		self.posy = self.itemHeight_min + order * self.itemHeight;
		self.conentRect.anchoredPosition = CS.UnityEngine.Vector2(self.conentRect.anchoredPosition.x, self.posy);
		--self.textList:Insert(0, self.conentRect:GetChild(0));
		--self.checkpos = true;
	end
end


local ItemList = function(self)
	if check then
		self:ItemList();
	end
end

local CheckCurrentPos = function(self)
	self:CheckCurrentPos();
	self.speed = 0;
end
util.hotfix_ex(CS.SpecialMissionSelectController,'Init',Init)
util.hotfix_ex(CS.SpecialMissionSelectController,'ItemList',ItemList)
--util.hotfix_ex(CS.SpecialMissionSelectController,'CheckCurrentPos',CheckCurrentPos)
