local this = {}

this.Init = function(self)
	-- print("AnnouncementModel Init", self.inited)
	if not self.inited then
		local regionType = "cn"

		if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw then
			regionType = "tw"
		elseif CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
			regionType = "kr"
		elseif CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
			regionType = "jp"
		elseif CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
			regionType = "us"
		end

		self.open = false
		local txt = CS.ResManager.GetObjectByPath("ProfilesConfig/AnnounceConfig", ".txt");
		local json = nil
		if txt ~= nil then
			json = CS.LitJson.JsonMapper.ToObject(txt.text)
		end
		
		if json ~= nil and json:Contains(regionType) then
			local jsonRegion = json:GetValue(regionType)
			self.open = jsonRegion:GetValue("open").Int ~= 0
			if self.open then
				self.version = jsonRegion:GetValue("version").Int
				self.path = jsonRegion:GetValue("path").String
			end
		end

		print("AnnouncementModel Init", self.inited, self.open, self.version, self.path)
		self.inited = true
	end
end

this.Reset = function(self)
	self.inited = false
end

return this