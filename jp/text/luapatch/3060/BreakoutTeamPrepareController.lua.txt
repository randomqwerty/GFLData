local util = require 'xlua.util'
xlua.private_accessible(CS.BreakoutTeamPrepareController)
xlua.private_accessible(CS.BreakoutIntelligenceBoxController)

local InitData = function(self)
	self:InitData()
	UpdateIntelligenceRedpoint(self)	
end

UpdateIntelligenceRedpoint = function(inst)
	local objIntelligence = inst.transform:Find("Main/Btn_Intelligence/Img_New").gameObject
	objIntelligence:SetActive(false);

    listSavedUnlockToSave = CS.System.Collections.Generic["List`1[System.Int32]"]()
    local listSavedUnlock = CS.System.Collections.Generic["List`1[System.Int32]"]()
    local saveConfigs = CS.UnityEngine.PlayerPrefs.GetString("localBreakoutUnlockIntelligence1", "");
    local vecSaveGuns = Split(saveConfigs, ",")
    
    for i=1, #vecSaveGuns do
    	if vecSaveGuns[i] ~= "" then
			local itemId = tonumber(vecSaveGuns[i]) 
			listSavedUnlock:Add(itemId)	
		end
	end

    for i=0, CS.GF.Tarkov.GameDataCache.I.listPhaseInfo.Count - 1 do
    	local dropItem = CS.GF.Tarkov.GameDataCache.I.listPhaseInfo[i]
    	if dropItem.mission == CS.GF.Tarkov.GameDataCache.I.playerData.missionId and CS.System.String.IsNullOrEmpty(dropItem.item_drop) == false then
       		local vecItems = Split(dropItem.item_drop, ",")
       		for j=1, #vecItems do
    			if vecItems[j] ~= "" then
    				local vecConfigs = Split(vecItems[j], "-")
    				local itemType = tonumber(vecConfigs[1])
    				if itemType == 2 then
    					local itemId = tonumber(Split(vecConfigs[2], ":")[1])
    					local unlock = CS.GameData.GetItem(itemId) > 0;
    					if unlock then
    						listSavedUnlockToSave:Add(itemId)
    					end

                    	if unlock and listSavedUnlock:Contains(itemId) == false then
                            objIntelligence:SetActive(true)
                    	end
    				end
				end
			end
       	end
    end
end

local Show = function(self)
	self:Show()

	local toSave = ""
	if listSavedUnlockToSave ~= nil then
		for i = 0, listSavedUnlockToSave.Count -1 do
			toSave = toSave ..listSavedUnlockToSave[i]
			if i ~= listSavedUnlockToSave.Count - 1 then        
            	toSave = toSave .. ","
        	end 
		end
	end
	CS.UnityEngine.PlayerPrefs.SetString("localBreakoutUnlockIntelligence1", toSave);
	UpdateIntelligenceRedpoint(CS.BreakoutTeamPrepareController.Instance)
end

local OnServiceStartAVGEnd = function(self)
	self:PlayBGM()
	self:OnServiceStartAVGEnd()
end

local OnBattleResultAVGEnd = function(self)
	self:PlayBGM()
	self:OnBattleResultAVGEnd()
end

util.hotfix_ex(CS.BreakoutTeamPrepareController,'InitData',InitData)
util.hotfix_ex(CS.BreakoutIntelligenceBoxController,'Show',Show)
util.hotfix_ex(CS.BreakoutTeamPrepareController,'OnServiceStartAVGEnd',OnServiceStartAVGEnd)
util.hotfix_ex(CS.BreakoutTeamPrepareController,'OnBattleResultAVGEnd',OnBattleResultAVGEnd)




