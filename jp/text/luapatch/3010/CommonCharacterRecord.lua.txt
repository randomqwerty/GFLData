local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCharacterRecord) 

local _InitList = function(self,recordList)

	if self.recordControllerList==nil then
		self.recordControllerList= CS.System.Collections.Generic.List(CS.TeamRecord) 
	end 
	self:InitList(recordList);
end
local record={}
local _InitUIElements = function(self)

	if self.recordControllerList~=nil then
		for i=0,self.recordControllerList.Count-1 do
			table.insert(record,self.recordControllerList[i]);
		end
		self:InitUIElements();
		for i=1,#record do
			self.recordControllerList.Add(record[i]);
		end
	else
		self:InitUIElements();
	end 
end
util.hotfix_ex(CS.CommonCharacterRecord,'InitList',_InitList)
util.hotfix_ex(CS.CommonCharacterRecord,'InitUIElements',_InitUIElements)


