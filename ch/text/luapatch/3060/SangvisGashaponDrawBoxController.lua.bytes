local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGashaponDrawBoxController)

local InitUIElements = function(self)
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		return;
	end
	local bgObj = CS.ResManager.GetObjectByPath("Prefabs/Btn_Probability");
	local bg = CS.UnityEngine.GameObject.Instantiate(bgObj);
	local parent = self.transform:Find("Frame");
	bg.transform:SetParent(parent, false);
	bg.transform.localPosition = CS.UnityEngine.Vector3(-50,-330,0);
	local btn = bg.transform:GetComponent(typeof(CS.ExButton));
	local text = CS.Data.GetLang(100335).."\n";
	local allnum = 0;
	local alltype2 = 0;
	local iter = self.currentGasha.sangvisCantureGashaRewardDic:GetEnumerator(); 
	while iter:MoveNext() do 
		local reward = iter.Current.Value;
		allnum = allnum + reward.currentCount;
		local type = reward.sangvisCaptureGashaRewardInfo.reward_type;
		if type == 2 or type == 4 or type == 6 then
			alltype2 = alltype2 +1;
		end
	end
	local index = 1;
	local iter1 = self.currentGasha.sangvisCantureGashaRewardDic:GetEnumerator(); 
	while iter1:MoveNext() do 
		local reward = iter1.Current.Value;
		local type = reward.sangvisCaptureGashaRewardInfo.reward_type;
		local sangvisid = reward.sangvisCaptureGashaRewardInfo.sangvis_id;
		CS.NDebug.Log("id",reward.sangvisCaptureGashaRewardInfo.id);
		if type == 1 or type == 3 or type == 5 then
			local txt = CS.Data.GetLang(100336);
			local name = CS.GameData.listSangvisGunInfo:GetDataById(tonumber(sangvisid)).name;
			local num = tostring(reward.currentCount);
			local all = tostring(reward.maxCount);
			local percentage = (num/allnum)*100;
			local perent = string.format("%.2f",percentage);
			local showtext = CS.System.String.Format(txt, name,num,all,perent);
			CS.NDebug.Log(type,showtext);
			text = text..showtext.."\n";
		else
			local txt = CS.Data.GetLang(100337);
			local txt1 = CS.Data.GetLang(100338);
			local star = tostring(math.ceil(4 - type/2));
			local indexText = tostring(index);
			index = index+1;
			if alltype2 == 1 then
				indexText = "";
			end
			local num = tostring(reward.currentCount);
			local all = tostring(reward.maxCount);
			local percentage = (num/allnum)*100;
			local perent = string.format("%.2f",percentage);
			local showtext = CS.System.String.Format(txt, star,indexText,num,all,perent);
			local ids = Split(sangvisid,",");
			local names = "";
			for j=1,#ids do
				local name = CS.GameData.listSangvisGunInfo:GetDataById(tonumber(ids[j])).name;
				if j~=1 then
					names = names.."、"..name;
				else
					names = names..name;
				end
			end			
			local showtext1 = CS.System.String.Format(txt1, star,indexText,names);
			CS.NDebug.Log(type,showtext);
			--CS.NDebug.Log(type,showtext1);
			text = text..showtext.."\n";	
			text = text..showtext1.."\n";		
		end 
	end	
	
	btn:AddOnClick(function ()
		CS.CommonRuleBoxController.OpenInMessageBox(text, nil);
	end)
	local webObj = CS.ResManager.GetObjectByPath("Prefabs/Btn_ProbabilityWeb");
	local web = CS.UnityEngine.GameObject.Instantiate(webObj);
	web.transform:SetParent(parent, false);
	web.transform.localPosition = CS.UnityEngine.Vector3(90,-330,0);
	local webbtn = web.transform:GetComponent(typeof(CS.ExButton));	
	webbtn:AddOnClick(function ()
			local url = CS.Data.GetString("kr_probability_web");
			CS.OPSWebWindows.Show(url);
		end)
end

function Split(szFullString, szSeparator)
	if(szFullString == nil) then
		return nil
	end
	local nFindStartIndex = 0
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end

util.hotfix_ex(CS.SangvisGashaponDrawBoxController,'InitUIElements',InitUIElements)




