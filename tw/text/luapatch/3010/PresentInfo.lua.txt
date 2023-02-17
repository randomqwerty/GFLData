local util = require 'xlua.util'
xlua.private_accessible(CS.PresentInfo)
local FormatTimeStamp = function(timeStamp)
	local restSecond = timeStamp;
	local restDays = restSecond / 86400;
	local restHours = (restSecond % 86400) / 3600;
	local restMinutes = (restSecond % 3600) / 60;
	
	if restMinutes < 1 then
		restMinutes = 1;
	end
	return CS.System.String.Format("{0}" .. CS.Data.GetLang(1122) .. 
		"{1}" .. CS.Data.GetLang(1121) .. "{2}" .. CS.Data.GetLang(1120), 
		math.floor(restDays), math.floor(restHours),math.floor(restMinutes));
end


local GetrestTime = function(self)
	local rest = self.restTimeInt;
	if rest == -1 or rest == -2 then
		return "";
	end
	return FormatTimeStamp(rest);
end

util.hotfix_ex(CS.PresentInfo,'get_restTime',GetrestTime)