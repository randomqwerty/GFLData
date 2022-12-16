local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessMapInfoItemCtrl)

local Start = function(self)
	self:Start();
	local txt = self.transform:Find("Img_MapTypeIcon/Img_Use/Tex_Use"):GetComponent(typeof(CS.ExText));
	txt.resizeTextForBestFit = true;
end
util.hotfix_ex(CS.GF.FlightChess.FlightChessMapInfoItemCtrl,'Start',Start)