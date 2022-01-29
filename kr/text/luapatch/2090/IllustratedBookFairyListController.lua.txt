local util = require 'xlua.util'
xlua.private_accessible(CS.IllustratedBookFairyListController)
xlua.private_accessible(CS.IllustratedBookController)
local _InitUIElements = function(self)
    self:InitUIElements();
    if self.listFakeFairy.Count>3 then

    	local index=self.listFakeFairy.Count-1; 
    	local fairy_m=self.listFakeFairy[index];
    	if fairy_m.info.id == 90004 then
    		print("remove 90004")
    		self.listFakeFairy:RemoveAt(index);
    	end


    	index=self.listFakeFairy.Count-1; 
    	local fairy_n=self.listFakeFairy[index];
    	if fairy_n.info.id == 90003 then
    		print("remove 90003")
    		self.listFakeFairy:RemoveAt(index);
    	end
    	fairy_m=nil;
    	fairy_n=nil;
    end
end
local _SetRightTop = function(self,title,acquired,amount)
    if self._illustratedBookFairyListController ~= nil then
        if self._illustratedBookFairyListController.gameObject.activeSelf then
            self:SetRightTop(title,acquired,amount-2);
        else
            self:SetRightTop(title,acquired,amount);
        end
    else
        self:SetRightTop(title,acquired,amount);
    end

end

util.hotfix_ex(CS.IllustratedBookFairyListController,'InitUIElements',_InitUIElements)
util.hotfix_ex(CS.IllustratedBookController,'SetRightTop',_SetRightTop)