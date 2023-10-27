local util = require 'xlua.util'
xlua.private_accessible(CS.DormExplorationFormationController)
xlua.private_accessible(CS.DormController)
 
local mOnClickClose = function(self)
    print("mOnClickClose")
    self:Close(); 
    --CS.DormExploreRoomController.instance.onEndExplore = nil;
    --CS.DormExploreRoomController.instance.onStartExplore = nil;
    CS.ExploreData.SaveSettings(nil);
end
local mRefreshAllUI = function(self) 
    if CS.DormExplorationFormationController.Instance ~=nil and CS.DormExplorationFormationController.Instance.gameObject~=nil then
        print("mRefreshAllUI 1")
        self:RefreshAllUI(); 
    else
        print("mRefreshAllUI delegate")
    end
end
local mClose = function(self) 
    if CS.DormExplorationFormationController.Instance==nil then
        print("mClose instance nil")
    else
        print("mClose")
        self:Close();
        CS.DormExplorationFormationController.Instance=nil;
    end 
end
local mResumeDorm = function(self) 
    if CS.DormExplorationFormationController.Instance~=nil and CS.DormExplorationFormationController.Instance.gameObject~=nil and CS.DormExplorationFormationController.Instance.gameObject.activeSelf then
        print("not ResumeDorm")
    else
        print("ResumeDorm")
        self:ResumeDorm();
    end 
end
local mPauseDorm = function(self) 
    if CS.DormExplorationFormationController.Instance~=nil and CS.DormExplorationFormationController.Instance.gameObject~=nil and CS.DormExplorationFormationController.Instance.gameObject.activeSelf then
        print("not PauseDorm")
    else
        print("PauseDorm")
        self:PauseDorm();
    end 
end
util.hotfix_ex(CS.DormExplorationFormationController,'OnClickClose',mOnClickClose)
util.hotfix_ex(CS.DormExplorationFormationController,'RefreshAllUI',mRefreshAllUI)
util.hotfix_ex(CS.DormExplorationFormationController,'Close',mClose)
util.hotfix_ex(CS.DormController,'ResumeDorm',mResumeDorm)
util.hotfix_ex(CS.DormController,'PauseDorm',mPauseDorm)