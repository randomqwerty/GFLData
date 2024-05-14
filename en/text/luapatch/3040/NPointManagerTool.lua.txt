local util = require 'xlua.util'
xlua.private_accessible(CS.NPointManagerTool)

local InitId = function(self,idArr,isRotation)
	if self.objList.Count == 0 then
		self:Start();
	end
	if self.nPointManagerToolBG.objList.Count == 0 then
		self.nPointManagerToolBG:Start();
	end
	self:InitId(idArr,isRotation);
end

local RotationToIndex = function(self,index)
	if not self.gameObject.activeInHierarchy then
		return;
	end
	self:RotationToIndex(index);
end
util.hotfix_ex(CS.NPointManagerTool,'InitId',InitId)
util.hotfix_ex(CS.NPointManagerTool,'RotationToIndex',RotationToIndex)