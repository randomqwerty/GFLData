local util = require 'xlua.util'
xlua.private_accessible(CS.AVGPicController)

local UpdatePic = function(self,picInfo)
	self:UpdatePic(picInfo);
	if self.gameLoadPic ~= nil then
		local order = tonumber(picInfo.picId);
		if self.gameLoadPic.transform.childCount > order then
			local child = self.gameLoadPic.transform:GetChild(order);
			if child ~= nil then
				local obj = CS.UnityEngine.GameObject.Instantiate(child.gameObject);
				obj.transform:SetParent(self.transform, false);
			end
		end
	end
end

util.hotfix_ex(CS.AVGPicController,'UpdatePic',UpdatePic)



