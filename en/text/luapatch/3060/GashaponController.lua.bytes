local util = require 'xlua.util'
xlua.private_accessible(CS.GashaponController)
xlua.private_accessible(CS.RequestGashaData)
 
local dicGashaRate=CS.System.Collections.Generic.Dictionary(CS.System.Int32,CS.System.String)();
local dicGashaRateComplete=CS.System.Collections.Generic.List(CS.System.Int32)();
local mOpenConfirmBox = function(self)
	print(self.gashaPoolId.."号奖池")
	local content = ""
	if dicGashaRate:ContainsKey(self.gashaPoolId) then
		content = dicGashaRate[self.gashaPoolId];
	else
		content = CS.Data.GetLang(170003);
		CS.CommonController.ShowRuleBox(content, CS.CommonController.MainCanvas.transform);
		return;
	end
	if dicGashaRateComplete:Contains(self.gashaPoolId) == false then

		print(self.gashaPoolId.."号奖池 需要重新替换content")
		local mRewardPool = CS.GashaponRewardPool();
		mRewardPool:Init(self.gashaPoolId)

		local skinList = mRewardPool:GetSkinList();
		if skinList~=nil and skinList.Count >0 then
			local skin_count = skinList.Count;
			  
			for i=0,skin_count-1 do
				local item = skinList[i]
				local key = "|"..item.id.."|"
				content=content:gsub(key, item.name);	 
			end
			skinList=nil;
		end
		local furGroupCount = mRewardPool:GetFurnitureListCount();
		for i=0,furGroupCount-1 do
			local listInfo=mRewardPool:GetFurnitureList(i)
			if listInfo~=nil and listInfo.Count >0 then
				for i=0,listInfo.Count-1 do
					local item = listInfo[i]
					local key = "@"..item.id.."@"
					content=content:gsub(key, item.name);	 
				end
				listInfo=nil;
			end
		end
		local giftList = mRewardPool:GetGiftList();
		if giftList~=nil and giftList.Count >0 then
			local gift_count = giftList.Count;
			  
			for i=0,gift_count-1 do
				local item = giftList[i]
				local key = "|"..item.id.."|"
				content=content:gsub(key, item.name);	 
			end
			giftList=nil;
		end
		mRewardPool=nil;	
		dicGashaRate[self.gashaPoolId]=content;
		dicGashaRateComplete:Add(self.gashaPoolId);
	end 
	--self.ConfirmBoxText.text = content;
	--print(content)
	if self.gashaPoolId==1 then
		local boxObj=CS.ResManager.GetObjectByPath("UGUIPrefabs/Common/CommonRuleBox")
		local box = CS.UnityEngine.GameObject.Instantiate(boxObj);
		box.transform:SetParent(CS.CommonController.MainCanvas.transform, false);
		local textOld=box.transform:Find("contents/content");
        textOld.gameObject:SetActive(false); 


        local Text_KRObj = CS.ResManager.GetObjectByPath("Prefabs/ProbabilityText_KR");
        local Text_KR = CS.UnityEngine.GameObject.Instantiate(Text_KRObj);
        Text_KR.transform:SetParent(textOld.transform.parent,false);


        local scroll = textOld.transform.parent:GetComponent(typeof(CS.UnityEngine.UI.ScrollRect))
        scroll.content=Text_KR.transform;

        local textBaseObj=Text_KR.transform:Find("Text_Content");
        local textObj2 = CS.UnityEngine.GameObject.Instantiate(textBaseObj);
        textObj2.transform:SetParent(textBaseObj.transform.parent,false);

        local text1 = textBaseObj:GetComponent(typeof(CS.ExText))
        local text2 = textObj2:GetComponent(typeof(CS.ExText))

        local len=#content;
        local midIndex = math.floor(len / 2);
        local firstPart = string.sub(content, 1, midIndex)
        local secondPart = string.sub(content, midIndex + 1)
        local delta = string.find(secondPart, "%%")
        if delta then
        	midIndex=midIndex+delta
        	firstPart= string.sub(content, 1, midIndex)
        	secondPart = string.sub(content, midIndex + 2)
        end
        text1.text = firstPart;
        text2.text = secondPart;
        --Text_KR.transform.localPosition = CS.UnityEngine.Vector3(Text_KR.transform.localPosition.x,-60000,0);
	else
		CS.CommonController.ShowRuleBox(content, CS.CommonController.MainCanvas.transform);
	end
        content=nil
end
local mSuccessJsonHandleData = function(self,jsonData)
	self:SuccessJsonHandleData(jsonData);
	if dicGashaRate==nil then
		dicGashaRate=CS.System.Collections.Generic.Dictionary(CS.System.Int32,CS.System.String)();
	end
	if dicGashaRate.Count >0 then
		dicGashaRate:Clear();
	end
	if dicGashaRateComplete==nil then
		dicGashaRateComplete=CS.System.Collections.Generic.List(CS.System.Int32)();
	end
	if dicGashaRateComplete.Count >0 then
		dicGashaRateComplete:Clear();
	end
	if jsonData:Contains("reward_weight_list") then
		local data = jsonData:GetValue("reward_weight_list");
		local gasha_len = CS.GameData.listGashaInfo.Count-1;
		--print("gasha_len:"..gasha_len)
		for i=0,gasha_len do
			local id = CS.GameData.listGashaInfo[i].id
			local key = id.."";
			dicGashaRate:Add(id,data:GetValue(key).String);
		end
	end
	--print("dicGashaRate:"..dicGashaRate.Count)
end

local mInitGashaponView = function(self)
	self:InitGashaponView();
	local web = CS.ResManager.GetObjectByPath("Prefabs/Btn_ProbabilityWeb");
    local webObj = CS.UnityEngine.GameObject.Instantiate(web);
    webObj.transform:SetParent(self.mFloatPointHolder.transform.parent, false);
    webObj.transform.localPosition=CS.UnityEngine.Vector3(870,-220,0);
    local btnWeb = webObj:GetComponent(typeof(CS.ExButton));
	btnWeb:AddOnClick(OnClickWeb);
end
function OnClickWeb() 
	local url = CS.Data.GetString("kr_probability_web")
	CS.UnityEngine.Application.OpenURL(url);
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then

util.hotfix_ex(CS.GashaponController,'OpenConfirmBox',mOpenConfirmBox) 
util.hotfix_ex(CS.GashaponController,'InitGashaponView',mInitGashaponView) 
util.hotfix_ex(CS.RequestGashaData,'SuccessJsonHandleData',mSuccessJsonHandleData)

end

