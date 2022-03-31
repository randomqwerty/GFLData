local util = require 'xlua.util'
xlua.private_accessible(CS.HomeAdjutantController)

function is_include(value, tb)
	for k, v in ipairs(tb) do
		if v == value then
			return true
		end
	end
	return false
end

local UpdateHomeAdjutant_New = function(self,...)
	self:UpdateHomeAdjutant(...); 

	local gunList = {97,20097,115,149, 168}
	local bgmList ={[97]="GF_Room_Rocktheme",[20097]="GF_Room_Rocktheme", [115]="BGM_21Christmas_DeathMetal", [149]="m_avg_tension", [168]="GF_room_violin_loop"}

	local newBgm = nil

	if self.adjutantInfo2 ~= nil and self.adjutantInfo2.gunInfo ~= nil and is_include(self.adjutantInfo2.gunInfo.id, gunList) then
		newBgm = bgmList[self.adjutantInfo2.gunInfo.id]
		--CS.NDebug.LogError(self.adjutantInfo2.gunInfo.id, "," ,newBgm)
	end

	if self.adjutantInfo ~= nil and self.adjutantInfo.gunInfo ~= nil and is_include(self.adjutantInfo.gunInfo.id, gunList) then
		newBgm = bgmList[self.adjutantInfo.gunInfo.id]
		--CS.NDebug.LogError(self.adjutantInfo.gunInfo.id, ",",newBgm)
	end

	if newBgm ~= nil then
		CS.CommonAudioController.PlayBGM(newBgm);
	else
		if CS.CommonAudioController.CurrentBGM ~= "BGM_Home" then
			CS.CommonAudioController.PlayBGM(CS.AudioBGM.BGM_Home);
			--CS.NDebug.LogError("BGM_Home")
		end
	end
end

util.hotfix_ex(CS.HomeAdjutantController,'UpdateHomeAdjutant',UpdateHomeAdjutant_New)




