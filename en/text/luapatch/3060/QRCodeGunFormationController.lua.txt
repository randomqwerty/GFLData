local util = require 'xlua.util'
xlua.private_accessible(CS.QRCodeGunFormationController)
local mRequestChangeToGunTeam = function(self)
	local isRepeated =false
	local currTeamID = CS.FormationController.Instance.currentSelectedTeam;
	local len =  self.scanGunResult.vecGuns.Length-1
	for i=0,len do
		if isRepeated == false then
			local newGun = self.scanGunResult.vecGuns[i];
			if newGun ~= nil and self.scanGunResult.vecGunState[i] == CS.QRCodeStateType.Available and newGun.teamId ~= 0 and newGun.teamId ~= 101 then

				local oldLocation = i +1
				local oldGun =nil;
				if CS.GameData.dictTeam[currTeamID].dictLocation:ContainsKey(oldLocation) then
					oldGun = CS.GameData.dictTeam[currTeamID].dictLocation[oldLocation];
				end
				if oldGun~=nil then
					local new_teamId = newGun.teamId;
	                local new_location = newGun.location;
	                local newlen = CS.GameData.dictTeam[new_teamId].listGun.Count-1
	                for j=0,newlen do
	                	if isRepeated == false then
		                	local tempGun = CS.GameData.dictTeam[new_teamId].listGun[j]
		                	if tempGun~=nil and tempGun._location ~= new_location then
		                		if tempGun.info == oldGun.info and tempGun ~= oldGun then
		                			isRepeated=true
		                		elseif tempGun.info.gunInfoOtherMod == oldGun.info then
		                			isRepeated=true
		                		elseif oldGun.info.gunInfoOtherMod == tempGun.info then
		                			isRepeated=true
		                		end	
		                	end
	                	end
	                end
				end
			end
		end
	end 
	if isRepeated then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(100048)); 
		return;
	else
		self:RequestChangeToGunTeam();
	end
end
util.hotfix_ex(CS.QRCodeGunFormationController,'RequestChangeToGunTeam',mRequestChangeToGunTeam)

