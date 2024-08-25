local HttpService = game:GetService("HttpService")

local apiUrl = "https://example.com/api"  -- Replace with actual API URL
local apiKey = "your_api_key_here"  -- Replace with actual API key

local function makeRequest(endpoint, method, data)
    local url = apiUrl .. endpoint
    local headers = {
        ["Authorization"] = "Bearer " .. apiKey,
        ["Content-Type"] = "application/json"
    }
    
    local requestData = {
        Url = url,
        Method = method,
        Headers = headers,
        Body = HttpService:JSONEncode(data)
    }
    
    local success, response = pcall(function()
        return HttpService:RequestAsync(requestData)
    end)
    
    if success then
        return HttpService:JSONDecode(response.Body)
    else
        warn("Request failed: " .. response)
        return nil
    end
end

-- Example usage
local status = makeRequest("/status", "GET", {})
print(status)
