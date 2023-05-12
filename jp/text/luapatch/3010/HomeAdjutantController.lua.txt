local util = require 'xlua.util'
xlua.private_accessible(CS.HomeAdjutantController)

local UpdateAdjutantGroup = function(self,left,right)
	while self.btnPicHolder.transform.childCount > 0 do
		local child = self.btnPicHolder.transform:GetChild(0);
		child:SetParent(nil,false);
		CS.UnityEngine.Object.Destroy(child.gameObject);
	end
	while self.btnPicHolder2.transform.childCount > 0 do
		local child = self.btnPicHolder2.transform:GetChild(0);
		child:SetParent(nil,false);
		CS.UnityEngine.Object.Destroy(child.gameObject);
	end
	self:UpdateAdjutantGroup(left,right);
end
local UpdateAdjutant = function(self,adjutantInfo)
	while self.btnPicHolder.transform.childCount > 0 do
		local child = self.btnPicHolder.transform:GetChild(0);
		child:SetParent(nil,false);
		CS.UnityEngine.Object.Destroy(child.gameObject);
	end
	while self.btnPicHolder2.transform.childCount > 0 do
		local child = self.btnPicHolder2.transform:GetChild(0);
		child:SetParent(nil,false);
		CS.UnityEngine.Object.Destroy(child.gameObject);
	end
	self:UpdateAdjutant(adjutantInfo);
end

util.hotfix_ex(CS.HomeAdjutantController,'UpdateAdjutantGroup',UpdateAdjutantGroup)
util.hotfix_ex(CS.HomeAdjutantController,'UpdateAdjutant',UpdateAdjutant)