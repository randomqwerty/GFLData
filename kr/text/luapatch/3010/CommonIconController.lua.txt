local util = require 'xlua.util'
xlua.private_accessible(CS.CommonIconController)
local CreateIcon = function(imageIcon,package,num,desc,width)
	CS.CommonIconController.CreateIcon(imageIcon,package,num,desc,width);
	if package ~= nil then
		if package.listItemPackage.Count > 0 then
			local itemInfo = package.listItemPackage[0].info;
			if itemInfo ~= nil and itemInfo.type == 5 then
				local fc = CS.GameData.listCosmeticMall:GetDataById(itemInfo.itemId - 1000);
				if fc ~= nil then
					if fc.type == CS.CosmeticType.headPic then
						CS.CommonController.LoadImageAvatarWithSequenceFrame(imageIcon, fc.id);
					end
					if fc.type == CS.CosmeticType.headFrame then
						CS.CommonController.LoadImageHeadFrameWithSequenceFrame(imageIcon, fc.id);
					end
				end
			end
		end
	end
end
util.hotfix_ex(CS.CommonIconController,'CreateIcon',CreateIcon)