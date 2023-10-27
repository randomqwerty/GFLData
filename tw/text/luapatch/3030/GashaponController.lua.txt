local util = require 'xlua.util'
xlua.private_accessible(CS.GashaponController)

local _CheckSkinHaveGun = function(self,gashaPrize)
	local showNoGunTip = false;
	if gashaPrize.isSkin and gashaPrize.giftInfo ~= nil then
		local _skinInfo = CS.GameData.listSkinInfo:GetDataById(gashaPrize.giftInfo.skin);
		if _skinInfo ~= nil then
			local tt = CS.GameData.listGun:Exists(
					(
						function(g) return g.info.id == _skinInfo.fitGun or (g.info.isMindupdate and _skinInfo.fitGun == g.info.gunInfoOtherMod.id); 
						end)
				);
			showNoGunTip = tt == false;
		end
	end
	return showNoGunTip;
end


util.hotfix_ex(CS.GashaponController,'CheckSkinHaveGun',_CheckSkinHaveGun)