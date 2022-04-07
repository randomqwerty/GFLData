local util = require 'xlua.util'
xlua.private_accessible(CS.ItemPackage)


local _NewItem = function(self, ...)
	local length = select('#', ...);
    if length == 2 then
        if self.info ~= nil and self.amount==0 and self.info.type == 12then
           self.amount=1;  
        end 
    end
end

util.hotfix_ex(CS.ItemPackage,'.ctor',_NewItem)