local util = require 'xlua.util'
xlua.private_accessible(CS.MallGoodController)

function getSecondDecimal(value)
    -- 处理浮点误差：先乘以100，四舍五入到整数
    local temp = value * 100
    local roundedTemp = math.floor(temp + 0.5)  -- 四舍五入
    
    -- 提取个位数（即原小数点后第二位）
    local secondDigit = roundedTemp % 10
    
    return secondDigit
end
local DoBuy = function(self)
	if CS.ApplicationConfigData.PlatformChannelId == "pc" then
		if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
			-- self.good.pointPrice=19.99
			-- local secondDigit = getSecondDecimal(self.good.pointPrice)
			-- print("secondDigit:"..secondDigit)
			-- if secondDigit == 9 then
   --  			self.good.pointPrice=self.good.pointPrice+0.0000001
   --  		else
   --  			self.good.pointPrice=self.good.pointPrice+0.0000001

   --  			print("弥补误差："..self.good.pointPrice)
			-- end
			if self.good.rmbId == '51324' or self.good.rmbId == '51325' or self.good.rmbId == '51326' or self.good.rmbId == '51327' then
				self.good.pointPrice=19.9900001
			end
			print("弥补误差："..self.good.pointPrice)
		end
	end	
	self:DoBuy();
end
if CS.ApplicationConfigData.PlatformChannelId == "pc" then
	util.hotfix_ex(CS.MallGoodController,'DoBuy',DoBuy)
end