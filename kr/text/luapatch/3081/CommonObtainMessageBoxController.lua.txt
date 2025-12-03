local util = require 'xlua.util'
xlua.private_accessible(CS.CommonObtainMessageBoxController)

local mInit = function(self,obtain)
	if obtain ~= nil and obtain.obtainInfo.id==3 and obtain.listMission ~= nil and  obtain.listMission.Count == 0 then
		
		local list_missions = CS.System.Collections.Generic.List(CS.System.Int32)();
		local count = CS.GameData.listMissionInfo.Count;
		for i=0,count-1 do
			local info = CS.GameData.listMissionInfo:GetDataByIndex(i)
			 
			if info~=nil and info.campaign>=0 then
				local autoMissionInfo = info.autoMissionInfo;
				if autoMissionInfo~=nil then
					if obtain.obtainType==1 then
						local gunPool = autoMissionInfo.gunPool
						if gunPool~=nil then
							for j=0,gunPool.Count-1 do
								local gun_info = gunPool[j];
								if gun_info~=nil and gun_info.id == obtain.gunId then
									list_missions:Add(info.id)
									break
								end
							end
						end
					end
					if obtain.obtainType==2 then
						local equipPool = autoMissionInfo.equipPool
						if equipPool~=nil then
							for j=0,equipPool.Count-1 do
								local equip_info = equipPool[j];
								if equip_info~=nil and equip_info.id == obtain.equipId then
									list_missions:Add(info.id)
									break
								end
							end
						end
					end
					-- if obtain.obtainType==4 then
					-- 	local componentPool = autoMissionInfo.componentPool
					-- 	if componentPool~=nil then
					-- 		for j=0,componentPool.Count-1 do
					-- 			local com_info = componentPool[j];
					-- 			if com_info~=nil and com_info.id == obtain.componentId then
					-- 				list_missions:Add(info.id)
					-- 				break
					-- 			end
					-- 		end
					-- 	end
					-- end
					
				end
			end
		end
		local m_count = list_missions.Count;
			
		--print("m_count:"..m_count)
		for i=0,m_count-1 do
			 	local mission_info_id = list_missions[i];

			 	local itemUI = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("UGUIPrefabs/GunState/Resource/ObtainDescription"), self.transParent, false);
				local itemCS= itemUI.transform:GetComponent(typeof(CS.ObtainDetailItemCtrl));

				local unlock= CS.GameData.listMission:ContainsKey(mission_info_id);
				--print("mission_info_id:"..mission_info_id)

				itemCS:Init(CS.GameData.listMissionInfo:GetDataById(mission_info_id),unlock);
		end
	else
		self:Init(obtain)
	end
end
util.hotfix_ex(CS.CommonObtainMessageBoxController,'Init',mInit)