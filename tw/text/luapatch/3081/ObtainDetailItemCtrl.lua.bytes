local util = require 'xlua.util'
xlua.private_accessible(CS.ObtainDetailItemCtrl)


local mInit = function(self,info,unlock)
	self:Init(info,unlock)
	if unlock==false then
		local btn=self.objLock:AddComponent(typeof(CS.ExButton));
		btn:AddOnClick(function()
					OnClickUnlock();
				end);
	end
	if info.campaign==14 then
		self.textNum.text = "A-"..info.sub
	end
end
function OnClickUnlock()--点击重置按钮
	CS.CommonController.LightMessageTips(CS.Data.GetLang(33065));
end
local mGotoJump = function(self)
	local unlock= CS.GameData.listMission:ContainsKey(self.missionInfo.id);
	if unlock==false then
		print("未解锁");
	else
		self:GotoJump()
	end
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw 
	or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea 
	or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
util.hotfix_ex(CS.ObtainDetailItemCtrl,'Init',mInit)
end
--util.hotfix_ex(CS.ObtainDetailItemCtrl,'SetClick',mSetClick)
--util.hotfix_ex(CS.ObtainDetailItemCtrl,'GotoJump',mGotoJump)