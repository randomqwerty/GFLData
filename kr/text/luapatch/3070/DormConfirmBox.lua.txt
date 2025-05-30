local util = require 'xlua.util'
xlua.private_accessible(CS.DormConfirmBox)
local confirmBox;
local InitBox = function(self,_msg,_handler,_showGive)
	confirmBox = self;
	self:InitBox(_msg,_handler,_showGive)
	if _showGive then
		local trigger = self.giveNumInputField.gameObject:AddComponent(typeof(CS.UnityEngine.EventSystems.EventTrigger));
		local entry = CS.UnityEngine.EventSystems.EventTrigger.Entry();
		entry.eventID = CS.UnityEngine.EventSystems.EventTriggerType.Select;
		entry.callback:AddListener(function(data)
				self.giveNumInputField.text = tostring(self.mNum);
		end)
		trigger.triggers:Add(entry);
		self.giveNumInputField.onValueChanged:AddListener(function(value)
				CheckInputField(value);
		end);
	end
end

function CheckInputField(value)
	local num = 1;
	if tonumber(value) ~= nil then
		num = tonumber(value);
		if num > confirmBox.mMaxValue then
			num = confirmBox.mMaxValue;
		end
		if num < 1 then
			num = 1;
		end
	else
		return;
	end
	confirmBox.mNum = num;
	confirmBox.mValue = num;
	confirmBox.giveNumInputField.text = tostring(num);
	local callback = confirmBox.mNumChangeDelegate;
	callback(num);
end

util.hotfix_ex(CS.DormConfirmBox,'InitBox',InitBox)



