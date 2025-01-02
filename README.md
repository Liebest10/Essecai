```
local scriptCode = [[
local mathService = game:GetService("MathRandom")
local BASE_CHANCE = 10
local LUCK_BONUS = 50

local function calculateLuck()
    local finalChance = BASE_CHANCE + LUCK_BONUS
    local randomNumber = mathService:NextInteger(1, 100)
    return randomNumber <= finalChance
end

local function initLuckySystem()
    if type(BASE_CHANCE) ~= "number" or type(LUCK_BONUS) ~= "number" then
        warn("Valores inválidos para BASE_CHANCE ou LUCK_BONUS")
    end
end

initLuckySystem()

game.Players.LocalPlayer.CharacterAdded:Connect(function(character)
    character:WaitForChild("Humanoid").Died:Connect(function()
        if calculateLuck() then
            print("Você é extremamente sortudo! Recebeu um item raro!")
        else
            print("Melhor sorte na próxima!")
        end
    end)
end)
]]

loadstring(scriptCode)()
```
