local util = require 'xlua.util'
xlua.private_accessible(CS.AVGPicController)

local yinshen = false;
local UpdatePic = function(self,picInfo)
	local code = picInfo.picName;
	local txt = Split(code,"#");
	local material = nil;
	local currentyinshen = false;
	for j=1,#txt do
		local mtxt = txt[j];
		if j == 1 then
			picInfo.picName = mtxt;
		elseif j == 2 then
			if mtxt == "隐身" then
				currentyinshen = true;
				local shareMat = CS.ResManager.GetObjectByPath("Material/PicCloaking"..txt[1],".mat");
				if shareMat == nil then
					shareMat = CS.ResManager.GetObjectByPath("Material/PicCloaking",".mat");
				end
				material = CS.UnityEngine.Object.Instantiate(shareMat);
			end
		end
	end
	if yinshen and not currentyinshen then
		self.picId = "";
		self.picName = "";
	end
	yinshen = currentyinshen;
	self:UpdatePic(picInfo);
	if material ~= nil then
		self.imageSelf.material = material;
	end
	picInfo.picName = code;
end
function Split(szFullString, szSeparator)
	local nFindStartIndex = 1
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
util.hotfix_ex(CS.AVGPicController,'UpdatePic',UpdatePic)

