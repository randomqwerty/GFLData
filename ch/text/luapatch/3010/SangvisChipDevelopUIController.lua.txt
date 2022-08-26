local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisChipDevelopUIController)
xlua.private_accessible(CS.ResManager)

local GetObjectByPath = function(path,type,callbackIfDownloaded,showlog)
	local index = string.find(path,".prefab");
	if index ~= nil then
		local path1 = string.gsub(path,".prefab","");
		CS.ResManager.GetObjectByPath(path1,type,callbackIfDownloaded,showlog);
		return;
	end
	CS.ResManager.GetObjectByPath(path,type,callbackIfDownloaded,showlog);
end

local Start = function(self)
	util.hotfix_ex(CS.ResManager,'GetObjectByPath',GetObjectByPath)
	self:Start();
end
util.hotfix_ex(CS.SangvisChipDevelopUIController,'Start',Start)

