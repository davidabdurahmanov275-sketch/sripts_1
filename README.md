-- 🔇 Полная блокировка сообщений в чат
pcall(function()

    -- блок FireServer (обычные сообщения)
    local mt = getrawmetatable(game)
    setreadonly(mt,false)

    local old = mt.__namecall
    mt.__namecall = newcclosure(function(self,...)
        local method = getnamecallmethod()

        if method == "FireServer" and tostring(self) == "SayMessageRequest" then
            return nil
        end

        if method == "SetCore" then
            local args = {...}
            if args[1] == "ChatMakeSystemMessage" then
                return nil
            end
        end

        return old(self,...)
    end)

    setreadonly(mt,true)

end)

-- 🚀 запуск твоего скрипта
loadstring(game:HttpGet("https://raw.githubusercontent.com/sladostrastnik/TokraScript/main/Loader.luau"))()
