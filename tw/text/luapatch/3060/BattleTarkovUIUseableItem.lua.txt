local util = require 'xlua.util'
xlua.private_accessible(CS.BattleTarkovUIUseableItem)
xlua.private_accessible(CS.GF.Tarkov.TarkovDragItem)


local IsDragVaild = function(self)
	local dragingRect = self.dragingRect
	local rectSelf = CS.UnityEngine.Rect(dragingRect.position.x + dragingRect.sizeDelta.x * dragingRect.lossyScale.x, dragingRect.position.y + dragingRect.sizeDelta.y * dragingRect.lossyScale.y, dragingRect.sizeDelta.x * dragingRect.lossyScale.x * 1.5, dragingRect.sizeDelta.y * dragingRect.lossyScale.y * 0.2)

	local other = self.transform.parent.parent.parent:Find("Img_CancelArea"):GetComponent(typeof(CS.UnityEngine.RectTransform))
	local rectOther = CS.UnityEngine.Rect(other.position.x + other.sizeDelta.x * other.lossyScale.x, other.position.y + other.sizeDelta.y * other.lossyScale.y * 0.8, other.sizeDelta.x * other.lossyScale.x, -other.sizeDelta.y * other.lossyScale.y * 5)
	if rectOther:Overlaps(rectSelf,true) then
		return false
	end
	return true
end
local TryUseItem = function(self)
	if not self.isCD and self.useableCount > 0 then
		self._uiManager:UseItem(self.itemid,CS.TarkovBattleWrapper.WorldPosToTarkovPos(self.currentDragPos.x),self.currentDragLane)
	end
end
util.hotfix_ex(CS.BattleTarkovUIUseableItem,'IsDragVaild',IsDragVaild)
util.hotfix_ex(CS.BattleTarkovUIUseableItem,'TryUseItem',TryUseItem)

