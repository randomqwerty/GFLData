local util = require 'xlua.util'
xlua.private_accessible(CS.RankingListUIController)

local Awake = function(self)
	self:Awake();
	local canvasTitle = self.transform:Find("Title"):GetComponent(typeof(CS.UnityEngine.Canvas));
	canvasTitle.sortingOrder = 20;
	local canvasTop = self.transform:Find("Top"):GetComponent(typeof(CS.UnityEngine.Canvas));
	canvasTop.sortingOrder = 20;
	local canvasPlayer = self.transform:Find("Main/PlayerRankItem").gameObject:AddComponent(typeof(CS.UnityEngine.Canvas));
	canvasPlayer.overrideSorting = true;
	canvasPlayer.sortingOrder = 20;
end

util.hotfix_ex(CS.RankingListUIController,'Awake',Awake)

