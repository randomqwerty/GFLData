local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCharacterRecord) 

--local record={}
local _InitList = function(self,recordList)

	if self.recordControllerList==nil then
		self.recordControllerList= CS.System.Collections.Generic.List(CS.TeamRecordItem) 
	end 
	self:InitList(recordList);
end

local _InitUIElements = function(self)
	local record={}
	if self.recordControllerList~=nil then
		for i=0,self.recordControllerList.Count-1 do
			if self.recordControllerList[i]~=nil then
				table.insert(record,self.recordControllerList[i]);
			end 
		end
		self:InitUIElements();
		for i=1,#record do
			self.recordControllerList:Add(record[i]);
		end
	else
		self:InitUIElements();
	end 
end
util.hotfix_ex(CS.CommonCharacterRecord,'InitList',_InitList)
util.hotfix_ex(CS.CommonCharacterRecord,'InitUIElements',_InitUIElements)


