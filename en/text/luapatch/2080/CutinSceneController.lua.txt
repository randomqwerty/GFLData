local util = require 'xlua.util'
xlua.private_accessible(CS.CutinSceneController)
local gunTable = {"obelisk"}
local OffsetDataTableX = {-2,0.5,0,1.6}
local OffsetDataTableY = {1.3,-0.2,0,1.3}
local ScaleTableX = {0.85,1,1,0.5}
local ScaleTableY = {0.85,1,1,0.5}
local CreatePerformanceSquad = function(self,summonerData,offsetIndex)
	self:CreatePerformanceSquad(summonerData,offsetIndex)
	if CS.CutinController.Instance.splitCount == 2 then
		for i=1,#gunTable do
			if self.character.gun:GetCode() == gunTable[i] and offsetIndex == 0 then
				self.character.transform.localPosition = CS.UnityEngine.Vector3(0.67,-1.97,1.95)
				self.character.transform.localScale = CS.UnityEngine.Vector3(0.85,0.85,0.85)
				break
			end
			if self.character.gun:GetCode() == gunTable[i] and offsetIndex == 1 then
				self.character.transform.localPosition = CS.UnityEngine.Vector3(0.63,-2.41,3.15)
				self.character.transform.localScale = CS.UnityEngine.Vector3(0.85,0.85,0.85)
				break
			end
		end
	end

	
end

util.hotfix_ex(CS.CutinSceneController,'CreatePerformanceSquad',CreatePerformanceSquad)