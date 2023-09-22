local util = require 'xlua.util'
xlua.private_accessible(CS.DormFurnitureController)
xlua.private_accessible(CS.DormFurniturePieceController)

local InitVehicle_New = function(self,...)
    self:InitVehicle(...)

    local dormOrderBody = -257
    local resetOrderBody = self.arrPieceController[0]:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder;--8

    for i = 0, self.arrPieceController.Length - 1 do 
        local resetOrder = self.arrPieceController[i]:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder;
        self.arrPieceController[i]:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = resetOrder - resetOrderBody + dormOrderBody;
    end    
end

local InitVehiclePiece_New = function(self)
    self.spine = self:GetComponent(typeof(CS.SkeletonAnimation))
    self:StopAnim();
    self.spineMeshRenderer = self:GetComponent(typeof(CS.UnityEngine.MeshRenderer))
end


util.hotfix_ex(CS.DormFurnitureController,'InitVehicle',InitVehicle_New)
util.hotfix_ex(CS.DormFurniturePieceController,'InitVehicle',InitVehiclePiece_New)



