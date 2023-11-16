local util = require 'xlua.util'
xlua.private_accessible(CS.HomeAdjutantController)
--xlua.private_accessible(CS.Live2D.Cubism.Rendering.Masking.CubismMaskController)
xlua.private_accessible(CS.GunStateController)
xlua.private_accessible(CS.WeddingPlay)

local GetLive2dMaskController = function(picController)
	if picController ~= nil then
    	local live2d = picController.transform:GetComponent(typeof(CS.CommonLive2DController))
    	if live2d ~= nil then   
    		local maskController = live2d.currModel.model:GetComponent(typeof(CS.Live2D.Cubism.Rendering.Masking.CubismMaskController))
    		return maskController
    	end
    end

    return nil
end

local MaskTextureRemove = function(picController)
	local maskController = GetLive2dMaskController(picController)
	if maskController ~= nil and maskController.MaskTexture ~= nil then
		maskController.MaskTexture:RemoveSource(maskController);
		CS.NDebug.LogError("----------------------------------------------- MaskTextureRemove")
	end
end

local MaskTextureAdd = function(picController)
	local maskController = GetLive2dMaskController(picController)
	if maskController ~= nil and maskController.MaskTexture ~= nil then
		maskController.MaskTexture:AddSource(maskController);
		CS.NDebug.LogError("----------------------------------------------- MaskTextureAdd")
	end
end

local AdjutantMaskTextureRemove = function(btnPicHolder)
	if btnPicHolder ~= nil then   	
    	local live2d = btnPicHolder.transform:GetComponentInChildren(typeof(CS.CommonLive2DController))
    	if live2d ~= nil then   
    		local maskController = live2d.currModel.model:GetComponent(typeof(CS.Live2D.Cubism.Rendering.Masking.CubismMaskController))
    		if maskController ~= nil and maskController.MaskTexture ~= nil then
    			maskController.MaskTexture:RemoveSource(maskController);
    			CS.NDebug.LogError("----------------------------------------------- AdjutantMaskTextureRemove")
    		end
    	end
    end	
end

local UpdateAdjutant_New = function(self, ...)
    self.btnPicHolder.transform:DestroyChildren();
    self.btnPicHolder2.transform:DestroyChildren();
	AdjutantMaskTextureRemove(self.btnPicHolder)   
	self:UpdateAdjutant(...)
end

local OnEnable_New = function(self)
	MaskTextureAdd(self.picController)
	self:OnEnable()
end

local OnDisable_New = function(self)
	MaskTextureRemove(self.picController)
	self:OnDisable()
end

local ChangeActive_New = function(self, inactives, b)
	if b then
		MaskTextureRemove(self.mCommonLive2DController)
	end
	self:ChangeActive(inactives, b)
end

util.hotfix_ex(CS.HomeAdjutantController,'UpdateAdjutant',UpdateAdjutant_New)
util.hotfix_ex(CS.GunStateController,'OnEnable',OnEnable_New)
util.hotfix_ex(CS.GunStateController,'OnDisable',OnDisable_New)
util.hotfix_ex(CS.WeddingPlay,'ChangeActive',ChangeActive_New)


