local util = require 'xlua.util'
--[[
public enum TaskStatus
{
	Inactive = 0,
	Failure = 1,
	Success = 2,
	Running = 3
}
]]--
taskStatus = 2

OnAwake = function()
	--print("TestAction OnAwake", testId, testMsg, testFP)
end

OnStart = function()
	
	xlua.private_accessible(CS.GF.Tarkov.BattleManager)
	local list = CS.GF.Tarkov.RootSystem.instance.BattleManager._listUnitDataMultiLane
	local count = list.Count
	-- print("TestAction OnStart1", count)
	for i=count-1,0,-1 do
		if list[i].isDead then
			list:RemoveAt(i)
		end
	end
	list = nil
	-- print("TestAction OnStart2", list.Count)
end

OnReset = function()
	--print("TestAction OnReset", testId, testMsg, testFP)
end