local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterFormationRectItem)

theaterRect = nil;
local OpenGunState = function()
	--[[local theaterRect = nil;

	--射线检测ui
	local eventSystem = CS.UnityEngine.EventSystems.EventSystem.current;
	local pointerEventData = CS.UnityEngine.EventSystems.PointerEventData(eventSystem);
	pointerEventData.position = CS.UnityEngine.Vector2(CS.UnityEngine.Input.mousePosition.x,CS.UnityEngine.Input.mousePosition.y);
	local uiRaycastResult = CS.System.Collections.Generic.List(CS.UnityEngine.EventSystems.RaycastResult)();
	eventSystem:RaycastAll(pointerEventData, uiRaycastResult);
	for i=0,uiRaycastResult.Count-1 do
		theaterRect = uiRaycastResult[i].gameObject:GetComponent(typeof(CS.TheaterFormationRectItem));
		if(theaterRect ~= nil) then
			break;
		end
	end--]]

	if theaterRect ~= nil then
	theaterRect.isDraging = false;
	if theaterRect.isSangvis or theaterRect.isNull or theaterRect.isNPC ~= 0 or theaterRect.isLock then
		return;
	end
	theaterRect:ResetDrag();
	CS.GunStateController.Open("UGUIPrefabs/GunState/New/GunState");
	CS.GunStateController.Instance:InitData(CS.LoadLevel.Formation, theaterRect.gun);
	CS.GunStateController.Instance:HideCombineStrengthTrainButton(true);
	CS.TheaterEchelonSelection.Instance.topUIObj:SetActive(true);
    CS.TheaterEchelonSelection.Instance.topUIObj.transform:SetAsLastSibling();
end
	uiRaycastResult = nil;
end

local OpenSangvisGunGunState = function()
	local theaterRect = nil;

	--射线检测ui
	local eventSystem = CS.UnityEngine.EventSystems.EventSystem.current;
	local pointerEventData = CS.UnityEngine.EventSystems.PointerEventData(eventSystem);
	pointerEventData.position = CS.UnityEngine.Vector2(CS.UnityEngine.Input.mousePosition.x,CS.UnityEngine.Input.mousePosition.y);
	local uiRaycastResult = CS.System.Collections.Generic.List(CS.UnityEngine.EventSystems.RaycastResult)();
	eventSystem:RaycastAll(pointerEventData, uiRaycastResult);
	for i=0,uiRaycastResult.Count-1 do
		theaterRect = uiRaycastResult[i].gameObject:GetComponent(typeof(CS.TheaterFormationRectItem));
		if(theaterRect ~= nil) then
			break;
		end
	end

	if theaterRect ~= nil then
	theaterRect.isDraging = false;
	if theaterRect.isSangvis == false or theaterRect.isNull or theaterRect.isNPC ~= 0 or theaterRect.isLock then
		return;
	end
	theaterRect:ResetDrag();
	CS.SangvisGunStateController.OpenWithSangvisGun(CS.LoadLevel.Formation, theaterRect.sangvis, nil);
end
	uiRaycastResult = nil;
end

local InitAsGun = function(self,...)
	if(self.isNPC == 0 and CS.TheaterEchelonSelection.Instance ~= nil)  then
		self.btnSelf:SetCharacterListLongPress(OpenGunState);
    else
		self.btnSelf:SetCharacterListLongPress(nil,false);
	end
	self:InitAsGun(...);
end

local InitAsSangvis = function(self,...)
	if(self.isNPC == 0 and CS.TheaterEchelonSelection.Instance ~= nil)  then
		self.btnSelf:SetCharacterListLongPress(OpenSangvisGunGunState);
    else
		self.btnSelf:SetCharacterListLongPress(nil,false);
	end
	self:InitAsSangvis(...);
end

local ResetUI = function(self)
	self.btnSelf:SetCharacterListLongPress(nil,false);
	self:ResetUI();
end

local InitUIElements = function(self)
	self:InitUIElements();
	CS.EventTriggerListener.Get(self.gameObject).onEnter = 
	function()
	    theaterRect = self;
	end
end

util.hotfix_ex(CS.TheaterFormationRectItem,'InitAsGun',InitAsGun)
util.hotfix_ex(CS.TheaterFormationRectItem,'InitAsSangvis',InitAsSangvis)
util.hotfix_ex(CS.TheaterFormationRectItem,'ResetUI',ResetUI)
util.hotfix_ex(CS.TheaterFormationRectItem,'InitUIElements',InitUIElements)


