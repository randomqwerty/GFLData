local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterGainEffectUIController)
local _ShowConstructionDetails= function(self,theaterConstructionInfo)
	self:ShowConstructionDetails(theaterConstructionInfo);
	local level=theaterConstructionInfo.lv;
	if level>0 then

		local curEffectInfo = CS.GameData.listTheaterEffectInfo:GetDataById(theaterConstructionInfo.effect_id);
     
		if curEffectInfo.type == 2 then
			local gun_num=0;
    		local san_num=0;
			for i=1,level,1 do
				local info=CS.GameData.listTheaterConstructionInfo:GetDataById(theaterConstructionInfo.group_id*100+i);
				if info ~=nil then
					local effect=CS.GameData.listTheaterEffectInfo:GetDataById(info.effect_id);
					gun_num=gun_num+effect.spare_gun_num;	
					san_num=san_num+effect.spare_sangvis_cost; 
				end 
			end 
			self.mTextConstructionEffectGunDes.text = CS.System.String.Format(CS.Data.GetLang(210221),gun_num);
			self.mTextConstructionEffectSangvisDes.text = CS.System.String.Format(CS.Data.GetLang(210222),san_num);

			local nextInfo = theaterConstructionInfo:GetNextLevelConstructionInfo();
			if nextInfo ~=nil then
				local gun_num_next=0;
    			local san_num_next=0;
    			local level_next=level+1;
				for i=1,level_next,1 do
					local info_next=CS.GameData.listTheaterConstructionInfo:GetDataById(theaterConstructionInfo.group_id*100+i);
					if info_next ~=nil then
						local effect_next=CS.GameData.listTheaterEffectInfo:GetDataById(info_next.effect_id);
						gun_num_next=gun_num_next+effect_next.spare_gun_num;	
						san_num_next=san_num_next+effect_next.spare_sangvis_cost; 
					end 
				end
				self.mTextNextLevelGunEffect.text = CS.System.String.Format(CS.Data.GetLang(210221), gun_num_next);
                self.mTextNextLevelSangvisEffect.text = CS.System.String.Format(CS.Data.GetLang(210222), san_num_next);
			end
		end	
		
	end 
end
util.hotfix_ex(CS.TheaterGainEffectUIController,'ShowConstructionDetails',_ShowConstructionDetails)



