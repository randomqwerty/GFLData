local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionActivityBar)

local Init = function(self,config)
	self:Init(config);
	local image = self.transform:Find("MissionShow"):GetComponent(typeof(CS.ExImage));
	local holder = self.transform:Find("MissionShow"):GetComponent(typeof(CS.UGUISpriteHolder));
	if image~=nil and holder~= nil then
		if config.campaignId == -61 then
			image.sprite = holder.listSprite[1];
		end
	end
end

util.hotfix_ex(CS.MissionSelectionActivityBar,'Init',Init)

