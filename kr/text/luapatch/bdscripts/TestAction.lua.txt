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
	print("TestAction OnAwake", testId, testMsg, testFP)
end

OnStart = function()
	local test1 = testFP:AsFloat() + 1
	print("TestAction OnStart", testId, testMsg, test1)
end

OnReset = function()
	print("TestAction OnReset", testId, testMsg, testFP)
end