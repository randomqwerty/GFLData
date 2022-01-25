local util = require 'xlua.util'
xlua.private_accessible(CS.OneClickBuyPackage)

local myOneClickBuyPackage = function(self, ...)
	--print('myOneClickBuyPackage1');
	local length = select('#', ...);
    if length == 5 then		
		local goodType = select(1, ...);
		local id = select(2, ...);

		if(CS.System.Convert.ToInt32(goodType) == 1 and id == 7 and self.mallGoodRight == nil and self.mallGoodLeft ~=  nil) then
			--print('myOneClickBuyPackage2');
			self.costLeftContract = self.mallGoodLeft.gemPrice
		end
	end
end

util.hotfix_ex(CS.OneClickBuyPackage, '.ctor', myOneClickBuyPackage)



