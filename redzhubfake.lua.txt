-- ts file was generated at discord.gg/25ms

local u1 = select(1, ...) or {
    JoinTeam = 'Pirates',
    Translator = true,
}

if not game.IsLoaded then
    game.Loaded:Wait()
end

local _VirtualInputManager = game:GetService('VirtualInputManager')
local _LocalizationService = game:GetService('LocalizationService')
local _CollectionService = game:GetService('CollectionService')
local _ReplicatedStorage = game:GetService('ReplicatedStorage')
local _VirtualUser = game:GetService('VirtualUser')
local _HttpService = game:GetService('HttpService')
local _RunService = game:GetService('RunService')
local _Lighting = game:GetService('Lighting')
local _Players = game:GetService('Players')
local _CoreGui = game:GetService('CoreGui')
local _CurrentCamera = workspace.CurrentCamera
local _Stepped = _RunService.Stepped
local _LocalPlayer = _Players.LocalPlayer
local _Data = _LocalPlayer:WaitForChild('Data')

_Data:WaitForChild('LastSpawnPoint')
_Data:WaitForChild('SpawnPoint')

local _Fragments = _Data:WaitForChild('Fragments')
local _Subclass = _Data:WaitForChild('Subclass')
local _FruitCap = _Data:WaitForChild('FruitCap')
local _Level = _Data:WaitForChild('Level')
local _Beli = _Data:WaitForChild('Beli')
local _Map = workspace:WaitForChild('Map')
local _NPCs = workspace:WaitForChild('NPCs')
local _Boats = workspace:WaitForChild('Boats')
local _SeaBeasts = workspace:WaitForChild('SeaBeasts')
local _Enemies = workspace:WaitForChild('Enemies')
local _Characters = workspace:WaitForChild('Characters')
local __WorldOrigin = workspace:WaitForChild('_WorldOrigin')
local _Locations = __WorldOrigin:WaitForChild('Locations')

__WorldOrigin:WaitForChild('PlayerSpawns')

local _Remotes = _ReplicatedStorage:WaitForChild('Remotes')
local _Modules = _ReplicatedStorage:WaitForChild('Modules')
local _Net = _Modules:WaitForChild('Net')
local u32 = (getgenv or getrenv or getfenv)()
local _HttpGet = game.HttpGet
local u34 = {}
local u35 = {}
local u36 = u32.rz_Functions or {}
local u37 = u32.rz_FarmFunctions or {}
local u38 = u32.rz_Settings or {
    AutoBuso = true,
    BringMobs = true,
    BringDistance = 250,
    FarmMode = 'Up',
    FarmTool = 'Melee',
    FarmDistance = 15,
    FarmPos = Vector3.new(0, 15, 0),
    SeaSkills = {},
    boatSelected = {},
    fishSelected = {},
}
local u45 = u32.rz_EnabledOptions or setmetatable({}, {
    __newindex = function(_, p39, p40)
        rawset(u35, p39, p40 or nil)
        table.clear(u37)

        local v41, v42, v43 = ipairs(u36)

        while true do
            local v44

            v43, v44 = v41(v42, v43)

            if v43 == nil then
                break
            end
            if rawget(u35, v44.Name) then
                table.insert(u37, v44)
            end
        end
    end,
    __index = u35,
})
local _PlayerGui = _LocalPlayer.PlayerGui

if not (_LocalPlayer.Team or _LocalPlayer:FindFirstChild('Main')) then
    local v47 = 0

    local function v53(p48)
        local _ChooseTeam = _PlayerGui['Main (minimal)']:WaitForChild('ChooseTeam')
        local v50 = p48:find('pirate') and 'Pirates' or 'Marines'
        local v51 = getconnections(_ChooseTeam.Container[v50].Frame.TextButton.Activated)

        for v52 = 1, #v51 do
            v51[v52].Function()
        end
    end

    while not (_LocalPlayer.Team or _LocalPlayer:FindFirstChild('Main')) do
        if tick() - v47 >= 0.5 then
            pcall(v53, string.lower(u1.JoinTeam or 'Pirates'))

            v47 = tick()
        end

        task.wait()
    end
end
if u32.redz_hub_error then
    u32.redz_hub_error:Destroy()
end

local u54 = {
    Owner = 'https://raw.githubusercontent.com/newredz/',
}

u54.Repository = u54.Owner .. 'BloxFruits/refs/heads/main/'

local function u55()
    return identifyexecutor and identifyexecutor() or 'Null'
end
local function u58(p56)
    u32.loadedFarm = nil
    u32.OnFarm = false

    local _Message = Instance.new('Message', workspace)

    _Message.Text = string.gsub(p56, u54.Owner, '')
    u32.redz_hub_error = _Message

    return error(p56, 2)
end

function __httpget(p59, _)
    local v60, v61, v62 = pairs(u54)

    while true do
        local v63

        v62, v63 = v60(v61, v62)

        if v62 == nil then
            break
        end

        local v64 = '{' .. v62 .. '}'

        if p59:find(v64) then
            p59 = p59:gsub(v64, v63)
        end
    end

    local v65, v66 = pcall(_HttpGet, game, p59)

    if v65 then
        return v66, p59
    else
        return u58((('[1] [%s] Failed to load script: %s\n{{ %s }}'):format(u55(), p59, v66)))
    end
end
function __loadstring(p67, p68, p69)
    local v70, v71 = __httpget(p67)
    local v72, v73 = loadstring(v70 .. (p68 or ''))

    if type(v72) ~= 'function' then
        return u58((('[2] [%s] sintaxe error: %s\n{{ %s }}'):format(u55(), v71, v73)))
    end

    local v74, v75

    if p69 then
        v74, v75 = pcall(v72, unpack(p69))
    else
        v74, v75 = pcall(v72)
    end
    if v74 then
        return v75
    end
    if type(v75) == 'string' then
        ('[3] [%s] Execute error: %s\n{{ %s }}'):format(u55(), v71, v75)
    end
end

u32.rz_Functions = u36
u32.rz_Settings = u38
u32.rz_EnabledOptions = u45
u32.rz_FarmFunctions = u37

local u76 = rz_connections or {}

u32.rz_connections = u76

local v77, v78, v79 = ipairs(u76)

while true do
    local v80

    v79, v80 = v77(v78, v79)

    if v79 == nil then
        break
    end

    v80:Disconnect()
end

table.clear(u76)

local u81 = nil
local u82 = nil
local u83 = nil
local u84 = {
    Marines = function()
        u82.FireRemote('SetTeam', 'Marines')
    end,
    Pirates = function()
        u82.FireRemote('SetTeam', 'Pirates')
    end,
}

local function v88(p85)
    local u86 = _CollectionService:GetTagged(p85)

    table.insert(u76, _CollectionService:GetInstanceAddedSignal(p85):Connect(function(p87)
        table.insert(u86, p87)
    end))

    return u86
end

local __ChestTagged = v88('_ChestTagged')
local _BerryBush = v88('BerryBush')
local u101 = {
    RemoveFog = function()
        if _Lighting:FindFirstChild('LightingLayers') then
            _Lighting.LightingLayers:Remove()
        end
    end,
    AllCodes = function()
        local _RepositoryUtilsCodestxt = __httpget('{Repository}Utils/Codes.txt')
        local v92 = string.gsub(_RepositoryUtilsCodestxt, '\n', ''):split(' ')

        for v93 = 1, #v92 do
            _Remotes.Redeem:InvokeServer(v92[v93])
        end
    end,
    GetTimer = function(p94)
        local v95 = math.floor(p94)
        local v96 = math.floor(p94 / 60)
        local v97 = math.floor(p94 / 60 / 60)
        local v98 = v95 - v96 * 60
        local v99 = v96 - v97 * 60

        if v99 < 10 then
            v99 = '0' .. tostring(v99) or v99
        end

        local v100 = ':'

        if v98 < 10 then
            v98 = '0' .. tostring(v98) or v98
        end

        return v99 .. v100 .. v98
    end,
}
local u102 = {Managers = {}}
local _Managers = u102.Managers
local u104 = loadstring([[

    local module = {}
    module.__index = module
    
    local TweenService = game:GetService("TweenService")
    
    local tweens = {}
    local EasingStyle = Enum.EasingStyle.Linear
    
    function module.new(obj, time, prop, value)
      local self = setmetatable({}, module)
      
      self.tween = TweenService:Create(obj, TweenInfo.new(time, EasingStyle), { [prop] = value })
      self.tween:Play()
      self.value = value
      self.object = obj
      
      if tweens[obj] then
        tweens[obj]:destroy()
      end
      
      tweens[obj] = self
      return self
    end
    
    function module:destroy()
      self.tween:Pause()
      self.tween:Destroy()
      
      tweens[self.object] = nil
      setmetatable(self, nil)
    end
    
    function module:stop(obj)
      if tweens[obj] then
        tweens[obj]:destroy()
      end
    end
    
    return module
  ]])()

function _Managers.PlayerTeleport()
    local u105 = {
        lastCF = nil,
        lastTP = 0,
        nextNum = 1,
        BypassCooldown = 0,
        GreatTree = CFrame.new(28610, 14897, 105),
        SpawnVector = Vector3.new(0, -25.2, 0),
    }
    local _Unlocked = u82.Inventory.Unlocked
    local _Sea = u82.GameData.Sea
    local _IsAlive = u82.IsAlive
    local _FireRemote = u82.FireRemote
    local u110 = ({
        {
            ['Sky Island 1'] = Vector3.new(-4652, 873, -1754),
            ['Sky Island 2'] = Vector3.new(-7895, 5547, -380),
            ['Under Water Island'] = Vector3.new(61164, 15, 1820),
            ['Under Water Island Entrace'] = Vector3.new(3865, 20, -1926),
        },
        {
            ['Flamingo Mansion'] = Vector3.new(-317, 331, 597),
            ['Flamingo Room'] = Vector3.new(2283, 15, 867),
            ['Cursed Ship'] = Vector3.new(923, 125, 32853),
            ['Zombie Island'] = Vector3.new(-6509, 83, -133),
        },
        {
            Mansion = Vector3.new(-12464, 376, -7566),
            ['Hydra Island'] = Vector3.new(5651, 1015, -350),
            ['Temple of Time'] = Vector3.new(28286, 14897, 103),
            ['Sea Castle'] = Vector3.new(-5090, 319, -3146),
            ['Great Tree'] = Vector3.new(2953, 2282, -7217),
        },
    })[_Sea]

    local function u111()
        u105.NpcDebounce = false
    end

    function u105.talkNpc(_, p112, p113, ...)
        if _LocalPlayer:DistanceFromCharacter(p112.Position) < 5 then
            if type(p113) ~= 'function' then
                _FireRemote(p113, ...)
            else
                p113()
            end
        end
    end
    function u105.hasUnlocked(_, p114)
        if _Sea == 3 and (p114 == 'Hydra Island' or p114 == 'Sea Castle' or p114 == 'Mansion') then
            return _Unlocked['Valkyrie Helm']
        end
        if _Sea == 2 then
            if p114 == 'Flamingo Mansion' or p114 == 'Flamingo Room' then
                return _Unlocked['Swan Glasses'] or _Level.Value >= 1750
            end
            if p114 == 'Zombie Island' or p114 == 'Cursed Ship' then
                return _Level.Value >= 1000
            end
        end

        return true
    end
    function u105.GetNearestPortal(p115, p116)
        local _huge = math.huge
        local v118, v119, v120 = pairs(u110)
        local v121 = nil
        local v122 = nil

        while true do
            local v123

            v120, v123 = v118(v119, v120)

            if v120 == nil then
                break
            end
            if p115:hasUnlocked(v120) then
                local _Magnitude = (p116 - v123).Magnitude

                if _Magnitude < _huge then
                    v122 = v120
                    v121 = v123
                    _huge = _Magnitude
                end
            end
        end

        return v121, v122
    end
    function u105.TeleportToGreatTree(p125)
        p125.new(p125.GreatTree, nil, true)
        p125:talkNpc(p125.GreatTree, 'RaceV4Progress', 'TeleportBack')
    end
    function u105.NPCs(p126, p127, p128)
        if _IsAlive(_LocalPlayer.Character) then
            if p126.NpcDebounce and p127[p126.nextNum] then
                u83(p127[p126.nextNum] + p126.SpawnVector)

                return nil
            end

            local _PrimaryPart = _LocalPlayer.Character.PrimaryPart

            if #p127 ~= 1 then
                if #p127 > 1 then
                    if p126.nextNum > #p127 then
                        p126.nextNum = 1
                    end

                    local v130 = p127[p126.nextNum]

                    if _PrimaryPart and (_PrimaryPart.Position - v130.Position).Magnitude < 5 then
                        p126.nextNum = p126.nextNum + 1
                        p126.NpcDebounce = true

                        task.delay(1, u111)
                    else
                        p126.new(v130, p128)
                    end
                end
            else
                p126.new(p127[1], p128)
            end
        end
    end
    function u105.new(p131, p132, p133, p134)
        local v135 = u105

        if _IsAlive(_LocalPlayer.Character) and (tick() - v135.lastTP >= 1 or p131 ~= v135.lastCF) then
            if _LocalPlayer.Character.PrimaryPart then
                if not p133 then
                    v135.lastPosition = p131.Position
                end

                v135.lastTP = tick()
                v135.lastCF = p131

                local _Humanoid = _LocalPlayer.Character.Humanoid
                local _PrimaryPart2 = _LocalPlayer.Character.PrimaryPart

                if _Humanoid.Sit then
                    _Humanoid.Sit = false

                    return
                elseif _PrimaryPart2.Anchored then
                    u104:stop(_PrimaryPart2)
                else
                    local v138 = u38.TweenSpeed or 220
                    local _Position = p131.Position
                    local _Magnitude2 = (_PrimaryPart2.Position - _Position).Magnitude

                    if _Magnitude2 < 150 and not p132 then
                        u104:stop(_PrimaryPart2)

                        _PrimaryPart2.CFrame = p131
                    end

                    local v141, v142 = v135:GetNearestPortal(_Position)
                    local v143

                    if v141 then
                        v143 = (_Position - v141).Magnitude + 300
                    else
                        v143 = v141
                    end
                    if v141 and 8 <= tick() - v135.BypassCooldown and v143 < _Magnitude2 then
                        if v142 == 'Great Tree' then
                            v135:TeleportToGreatTree()
                        else
                            u104:stop(_PrimaryPart2)
                            task.wait(0.2)

                            if (_Position - v141).Magnitude >= 50 then
                                _Position = v141 + (_Position - _PrimaryPart2.Position).Unit * 40
                            end

                            _FireRemote('requestEntrance', _Position)

                            BypassCooldown = tick()
                        end
                    elseif p132 then
                        u104.new(_PrimaryPart2, _Magnitude2 / p132, 'CFrame', p131)
                    else
                        if not p134 then
                            local _Position2 = _PrimaryPart2.Position
                            local v145 = CFrame.new(_Position2.X, _Position.Y, _Position2.Z)

                            if (_Position2 - v145.Position).Magnitude > 75 then
                                u104:stop(_PrimaryPart2)
                                task.wait(0.1)

                                _PrimaryPart2.CFrame = v145

                                task.wait(0.5)
                            end
                        end
                        if _Magnitude2 < 380 then
                            u104.new(_PrimaryPart2, _Magnitude2 / (v138 * 2), 'CFrame', p131)
                        else
                            u104.new(_PrimaryPart2, _Magnitude2 / v138, 'CFrame', p131)
                        end
                    end
                end
            else
                return nil
            end
        else
            return nil
        end
    end

    u82.Tween:GetPropertyChangedSignal('Parent'):Connect(function()
        if not u82.Tween.Parent and _IsAlive(_LocalPlayer.Character) then
            u104:stop(_LocalPlayer.Character.PrimaryPart)
        end
    end)

    u83 = u105.new

    return u105
end
function _Managers.QuestManager()
    local u146 = {
        QuestList = {},
        EnemyList = {},
        QuestPos = {},
        Crafts = {},
        Sea = u82.GameData.Sea,
        takeQuestDebounce = false,
        _Position = CFrame.new(0, 0, 2.5),
    }
    local _Quest = _LocalPlayer.PlayerGui:WaitForChild('Main').Quest
    local _Title = _Quest.Container.QuestTitle.Title
    local u149 = 'https://raw.githubusercontent.com/newredzBloxFruits/refs/heads/main/GameModules/'
    local u150 = {
        GuideModule = _ReplicatedStorage:WaitForChild('GuideModule'),
        Quests = _ReplicatedStorage:WaitForChild('Quests'),
        SkinUtil = _Modules:WaitForChild('SkinUtil'),
    }

    local function v154(p151)
        local v152, v153 = pcall(function()
            return require(u150[p151])
        end)

        if not v152 then
            warn(('falha a o carregar Module [ %s ] [ %s ]'):format(p151, v153))
        end

        return v152 and v153 and v153 or loadstring(_HttpGet(workspace, u149 .. p151 .. '.lua'))()
    end

    local _GuideModule = v154('GuideModule')
    local _Quests = v154('Quests')
    local _SkinUtil = v154('SkinUtil')
    local u158 = _SkinUtil.AuraSkins or _SkinUtil
    local _EnemyLocations = u82.EnemyLocations
    local _ = u82.EnemySpawned
    local _IsBoss = u82.IsBoss
    local u161 = {
        Colors = {
            Context = 'GetSkinsInventory',
        },
    }

    local function v169(p162)
        local v163 = next
        local _Task = p162.Task
        local v165 = nil
        local v166 = {}
        local v167 = {}

        while true do
            local v168

            v165, v168 = v163(_Task, v165)

            if v165 == nil then
                break
            end

            v167 = _EnemyLocations[v165] or {}
            _EnemyLocations[v165] = v167

            table.insert(v166, v165)
        end

        return v166, v167
    end

    task.spawn(function()
        if _GuideModule.Data.IsFakeData then
            return nil
        end

        local v170, v171, v172 = pairs(_GuideModule.Data.NPCList)

        while true do
            local v173

            v172, v173 = v170(v171, v172)

            if v172 == nil then
                break
            end

            u146.QuestPos[v173.NPCName] = CFrame.new(v173.Position)
        end

        local v177 = {
            __newindex = function(p174, p175, p176)
                u146.QuestPos[p176.NPCName] = CFrame.new(p176.Position)

                return rawset(p174, p175, p176)
            end,
        }

        setmetatable(_GuideModule.Data.NPCList, v177)
    end)
    task.spawn(u82.RunFunctions.Quests, u146, _Quests, v169)

    function u146.GetUnlockedHakiColors(p178)
        if not p178.haki_colors or tick() - p178.haki_colors.last_update >= 30 then
            p178.haki_colors = _Net['RF/FruitCustomizerRF']:InvokeServer(u161.Colors)
            p178.haki_colors.last_update = tick()
        end

        return p178.haki_colors
    end
    function u146.GetQuest(p179)
        if p179.oldLevel ~= _Level.Value or not p179.CurrentQuest then
            p179.oldLevel = _Level.Value

            local _Sea2 = p179.Sea
            local v181 = math.clamp(_Level.Value, 0, _Sea2 == 1 and 700 or (_Sea2 == 2 and 1500 or _Level.Value))
            local v182, v183, v184 = ipairs(p179.QuestList)
            local v185 = nil
            local v186 = nil
            local v187 = nil

            while true do
                local v188

                v184, v188 = v182(v183, v184)

                if v184 == nil then
                    break
                end

                local _Level2 = v188.Enemy.Level
                local v190 = v188.Enemy.Name[1]

                if _IsBoss(v190) then
                    if _Level2 <= v181 and v181 - 50 <= _Level2 then
                        v185 = v190
                    else
                        v185 = false
                    end

                    v186 = v188
                else
                    if v181 < _Level2 then
                        p179.CurrentQuest = v187
                        p179.oldBossQuest = v186
                        p179.oldBoss = v185

                        return v187
                    end

                    v187 = v188
                end
            end

            p179.CurrentQuest = v187
            p179.oldBossQuest = v186
            p179.oldBoss = v185

            return v187
        elseif p179.oldBoss and u82.Enemies.IsSpawned(p179.oldBoss) then
            return p179.oldBossQuest
        else
            return p179.CurrentQuest
        end
    end
    function u146.GetQuestPosition(p191, p192)
        if not _GuideModule.Data.IsFakeData then
            return p191.QuestPos[_GuideModule.Data.LastClosestNPC]
        end

        local v193 = _GuideModule.Data.NPCs[p192]
        local v194 = not v193 or _NPCs:FindFirstChild(v193) or _ReplicatedStorage.NPCs:FindFirstChild(v193)

        if v194 then
            v194 = v194:GetPivot()
        end

        return v194
    end
    function u146.VerifyQuest(_, p195)
        if not _Quest.Visible then
            return false
        end

        local v196 = string.gsub(_Title.Text, '-', ''):lower()

        if type(p195) == 'string' then
            return string.find(v196, string.gsub(p195, '-', ''):lower())
        end

        local v197, v198, v199 = ipairs(p195)

        while true do
            local v200

            v199, v200 = v197(v198, v199)

            if v199 == nil then
                break
            end
            if string.find(v196, string.gsub(v200, '-', ''):lower()) then
                return v200
            end
        end
    end
    function u146.StartQuest(p201, p202, p203, p204)
        if p204 and _LocalPlayer:DistanceFromCharacter(p204.Position) >= 5 then
            u83(p204 * p201._Position)

            return 'Teleporting to NPC: ' .. p202
        end
        if not p201.takeQuestDebounce then
            task.wait(0.5)
            u82.FireRemote('StartQuest', p202, p203)

            return 'Getting Quest: ' .. p202, task.wait(0.5)
        end
        if p201.Debounce and 75 > tick() - p201.Debounce and p201.InDebounceQuest == p203 .. p202 then
            return 'Quest Debounce: ' .. u101.GetTimer(75 - (tick() - p201.Debounce))
        end

        u38.RunningMethod = 'Getting Quest: ' .. p202

        task.wait(0.5)
        u82.FireRemote('StartQuest', p202, p203)

        local v205 = p203 .. p202

        p201.Debounce = tick()
        p201.InDebounceQuest = v205

        return u38.RunningMethod, task.wait(0.5)
    end
    function u146.GetAuraCraft(_, p206)
        return (u158[p206] or {}).EtcItems
    end
    function u146.GetColorsList(_)
        local v207, v208, v209 = pairs(u158)
        local v210 = {}

        while true do
            local v211

            v209, v211 = v207(v208, v209)

            if v209 == nil then
                break
            end
            if v211.EtcItems then
                table.insert(v210, v209)
            end
        end

        return v210
    end

    return u146
end
function _Managers.FarmManager()
    local u212 = {
        NPCs = {},
        CanFarm = {},
        EnemyLocation = {},
        ClickPosition = Vector2.new(),
        axisDebounce = 0,
    }
    local _IsAlive2 = u82.IsAlive
    local _EnemySpawned = u82.EnemySpawned
    local _EnemyLocations2 = u82.EnemyLocations
    local _EquipTool = u82.EquipTool
    local u217 = 0

    u212.Materials = ({
        {
            'Leather + Scrap Metal',
            'Magma Ore',
            'Fish Tail',
            'Angel Wings',
        },
        {
            'Leather + Scrap Metal',
            'Magma Ore',
            'Mystic Droplet',
            'Radiactive Material',
            'Vampire Fang',
        },
        {
            'Leather + Scrap Metal',
            'Fish Tail',
            'Gunpowder',
            'Mini Tusk',
            'Conjured Cocoa',
            'Dragon Scale',
        },
    })[u82.GameData.Sea]
    u212.Enemies = {
        Elites = {
            'Deandre',
            'Diablo',
            'Urban',
        },
        Bones = {
            'Reborn Skeleton',
            'Living Zombie',
            'Demonic Soul',
            'Posessed Mummy',
        },
        Katakuri = {
            'Head Baker',
            'Baking Staff',
            'Cake Guard',
            'Cookie Crafter',
        },
        Ectoplasm = {
            'Ship Deckhand',
            'Ship Engineer',
            'Ship Steward',
            'Ship Officer',
        },
    }
    u212.FarmModes = {
        Star = function(p218, p219)
            local v220 = p219.CFrame + p218:GetNextAxis()

            if _LocalPlayer:DistanceFromCharacter(v220.Position) >= 5 then
                u83(v220)
            end
        end,
        Orbit = function(_, p221, p222)
            local _Parent = p221.Parent
            local v224 = task.wait()
            local _RunningOption = u38.RunningOption
            local v226 = 3.5
            local v227 = 0

            while(p222 or u38.FarmMode) == 'Orbit' and u45[_RunningOption] and (p221 and _IsAlive2(_Parent)) do
                if tick() - u217 >= 1 then
                    _EquipTool()
                end

                EnableBuso()

                local _FarmDistance = u38.FarmDistance

                v227 = v227 + v226 * v224

                u83(CFrame.new(math.cos(v227) * _FarmDistance, 8, math.sin(v227) * _FarmDistance) + p221.Position)

                v224 = task.wait(u38.SmoothMode and 0.1 or 0)
            end
        end,
        Up = function(_, p229)
            local v230 = p229.CFrame + u38.FarmPos

            if _LocalPlayer:DistanceFromCharacter(v230.Position) >= 5 then
                u83(v230)
            end
        end,
    }

    local u231 = {
        ['Angel Wings'] = {
            CFrame.new(-7742, 5634, -1564),
        },
        ['Leather + Scrap Metal'] = {
            CFrame.new(-1257, 54, 4091),
            CFrame.new(-1100, 77, 1152),
            CFrame.new(-364, 116, 5692),
        },
        ['Magma Ore'] = {
            CFrame.new(-5408, 11, 8456),
            CFrame.new(-5241, 50, -4713),
        },
        ['Fish Tail'] = {
            CFrame.new(60931, 19, 1574),
            false,
            CFrame.new(-10679, 398, -8975),
        },
        ['Mystic Droplet'] = {
            false,
            CFrame.new(-3350, 282, -10527),
        },
        ['Radiactive Material'] = {
            false,
            CFrame.new(-73, 149, -112),
        },
        ['Vampire Fang'] = {
            false,
            CFrame.new(-6030, 6, -1281),
        },
        Gunpowder = {
            false,
            false,
            CFrame.new(-394, 135, 5981),
        },
        ['Mini Tusk'] = {
            false,
            false,
            CFrame.new(-13510, 584, -6986),
        },
        ['Conjured Cocoa'] = {
            false,
            false,
            CFrame.new(400, 81, -12257),
        },
        ['Dragon Scale'] = {
            false,
            false,
            CFrame.new(6689, 378, 331),
        },
    }
    local u232 = {
        ['Leather + Scrap Metal'] = {
            {
                'Pirate',
                'Brute',
                'Scrap Metal',
                'Pirate Millionaire',
            },
            {true, true, true},
        },
        ['Angel Wings'] = {
            {
                'Royal Soldier',
                'Royal Squad',
            },
            {true, false, false},
        },
        ['Magma Ore'] = {
            {
                'Military Soldier',
                'Lava Pirate',
            },
            {true, true, false},
        },
        ['Fish Tail'] = {
            {
                'Fishman Warrior',
                'Fishman Captain',
                'Fishman Raider',
            },
            {true, false, true},
        },
        ['Conjured Cocoa'] = {
            {
                'Cocoa Warrior',
                'Chocolate Bar Battler',
            },
            {false, false, true},
        },
        ['Mystic Droplet'] = {
            {
                'Water Fighter',
            },
            {false, true, false},
        },
        ['Radiactive Material'] = {
            {
                'Factory Staff',
            },
            {false, true, false},
        },
        ['Vampire Fang'] = {
            {
                'Vampire',
            },
            {false, true, false},
        },
        Gunpowder = {
            {
                'Pistol Billionaire',
            },
            {false, false, true},
        },
        ['Mini Tusk'] = {
            {
                'Mythological Pirate',
            },
            {false, false, true},
        },
        ['Dragon Scale'] = {
            {
                'Dragon Crew Archer',
            },
            {false, false, true},
        },
    }

    function u212.ToolDebounce()
        u217 = tick()
    end
    function u212.TargetPosition(p233)
        if typeof(p233) == 'CFrame' then
            u83(p233)
            EnableBuso()
            _EquipTool()
        end
    end
    function u212.GetNextAxis(p234)
        if tick() - p234.axisDebounce <= 0.4 then
            return p234.nextAxis
        end

        local v235 = Vector3[math.random() <= 0.5 and 'xAxis' or 'zAxis'] * (math.random() <= 0.5 and u38.FarmDistance or -u38.FarmDistance) + Vector3.yAxis * 8
        local v236 = tick()

        p234.nextAxis = v235
        p234.axisDebounce = v236

        return v235
    end
    function u212.Mastery(_, p237, p238)
        local _Health = p238.Health
        local v240 = _Enemies
        local v241, v242, v243 = ipairs(v240:GetChildren())

        while true do
            local v244

            v243, v244 = v241(v242, v243)

            if v243 == nil then
                break
            end
            if v244.PrimaryPart then
                local _Humanoid2 = v244:FindFirstChild('Humanoid')

                if _Humanoid2 and 0 < _Humanoid2.Health and _Humanoid2.Health <= _Health then
                    _Health = _Humanoid2.Health
                    p237 = v244.PrimaryPart
                    p238 = _Humanoid2
                end
            end
        end

        local v246 = p237.CFrame + u38.FarmPos
        local v247 = p238.Health / p238.MaxHealth * 100

        _EquipTool(v247 <= u38.mHealth and u38.mTool or 'Melee', true)
        u82:BringEnemies(p237.Parent)
        EnableBuso()

        if _LocalPlayer:DistanceFromCharacter(v246.Position) >= 2.5 then
            u83(v246)
        end
        if v247 <= u38.mHealth and _LocalPlayer:DistanceFromCharacter(v246.Position) < 5 then
            u82.Hooking:SetTarget(p237, p237.Parent, true)
            u82.UseSkills(p237, u38.MasterySkills)
        end
    end
    function u212.attack(p248, p249, p250, p251)
        local _Humanoid3 = p248:FindFirstChild('Humanoid')

        if not _Humanoid3 then
            return nil
        end
        if u45.Mastery and _Humanoid3.MaxHealth < 40000 then
            u212:Mastery(p248.PrimaryPart, _Humanoid3)

            return true
        end
        if p249 then
            u82:BringEnemies(p248, p250)
        end
        if tick() - u217 >= 1 then
            _EquipTool()
        end

        EnableBuso()
        u212.FarmModes[p251 or u38.FarmMode](u212, p248.PrimaryPart, p251)

        if u38.SmoothMode and ((p251 or u38.FarmMode) ~= 'Orbit' and task.wait(0.1) and (_IsAlive2(p248) and p248.PrimaryPart)) and u45[u38.RunningOption] then
            local v253 = u38
            local v254 = u32
            local v255 = 'Killing: ' .. p248.Name

            v254.OnFarm = true
            v253.RunningMethod = v255

            u212.attack(p248, p249, p250, p251)
        end

        return true
    end
    function u212.Material(p256, p257)
        local v258 = u231[p257]

        if v258 then
            v258 = u231[p257][u82.GameData.Sea]
        end

        local v259 = u232[p257]

        if v259 then
            local _EnemyLocation = p256.EnemyLocation
            local _CanFarm = p256.CanFarm

            if _CanFarm[p257] == nil then
                if v259[2][u82.GameData.Sea] then
                    _CanFarm[p257] = true
                else
                    _CanFarm[p257] = false
                end
            end
            if not _CanFarm[p257] then
                return nil
            end
            if _EnemyLocation[p257] == nil then
                local v262, v263, v264 = ipairs(v259[1])

                while true do
                    local v265

                    v264, v265 = v262(v263, v264)

                    if v264 == nil then
                        break
                    end

                    local v266 = _EnemyLocations2[v265]

                    if v266 and 0 < #v266 then
                        _EnemyLocation[p257] = v266
                    end
                end

                if not _EnemyLocation[p257] then
                    _EnemyLocation[p257] = false
                end
            end

            local v267, v268, v269 = ipairs(v259[1])

            while true do
                local v270

                v269, v270 = v267(v268, v269)

                if v269 == nil then
                    break
                end

                local v271 = _EnemySpawned(v270)

                if v271 and v271.PrimaryPart then
                    p256.attack(v271, true, true)

                    return 'Killing: ' .. v270
                end
            end

            if _EnemyLocation[p257] then
                _Managers.PlayerTeleport:NPCs(_EnemyLocation[p257])
            else
                u83(v258)
            end

            return 'Farming Material: ' .. p257
        end
    end
    function u212.GetNpcPosition(p272, p273)
        if p272.NPCs[p273] then
            return p272.NPCs[p273]:GetPivot()
        end

        local v274 = _NPCs:FindFirstChild(p273) or _ReplicatedStorage.NPCs:FindFirstChild(p273)

        if v274 then
            p272.NPCs[p273] = v274

            local _ = v274.GetPivot
        end
    end

    return u212
end
function _Managers.RaidManager()
    if u82.GameData.Sea ~= 2 and u82.GameData.Sea ~= 3 then
        return nil
    end

    local v275 = {}
    local _ = u82.GameData.Sea ~= 2

    v275.RaidPosition = CFrame.new(-5033, 315, -2950)
    v275.requests = {}
    v275.Require = 0
    v275.Timer = _LocalPlayer.PlayerGui:WaitForChild('Main').Timer
    v275.Button = u82.GameData.Sea == 2 and 'CircleIsland.RaidSummon2.Button.Main' or (u82.GameData.Sea == 3 and 'Boat Castle.RaidSummon2.Button.Main' or false)

    function v275.IsRaiding(_)
        local _Raid = u45.Raid

        if _Raid then
            _Raid = _LocalPlayer:GetAttribute('IslandRaiding')
        end

        return _Raid
    end
    function v275.GetRaidIsland(_)
        return u82:GetRaidIsland()
    end
    function v275.CanStartRaid(_)
        local v277

        if _Level.Value < 1200 then
            v277 = false
        else
            v277 = VerifyTool('Special Microchip')
        end

        return v277
    end
    function v275.start(p278)
        if not p278:IsRaiding() and p278:CanStartRaid() then
            local v279 = p278.Button:split('.')
            local v280 = _Map

            for v281 = 1, #v279 do
                if v280 then
                    v280 = v280:FindFirstChild(v279[v281])
                end
            end

            if v280 and v280:FindFirstChild('ClickDetector') then
                fireclickdetector(v280.ClickDetector)
                task.wait(1)
            else
                local _ = p278.RaidPosition
            end
        end
    end
    function v275.requestFragment(p282, p283, p284)
        if p282.requests[p283] then
            return nil
        end

        p282.Require = p282.Require + (p284 or 0)
    end

    return v275
end
function _Managers.ItemsQuests()
    local u285 = {
        CursedDualKatana = {},
        SkullGuitar = {},
    }
    local _IsSpawned = u82.Enemies.IsSpawned
    local _EnemySpawned2 = u82.EnemySpawned
    local _EnemyLocations3 = u82.EnemyLocations
    local _EquipTool2 = u82.EquipTool
    local _FireRemote2 = u82.FireRemote

    if u82.GameData.Sea == 3 then
        local u291 = nil

        local function u300()
            if u291 and u291.Value > 0 then
                return u291
            end

            local _huge2 = math.huge
            local v293, v294, v295 = ipairs(_LocalPlayer.QuestHaze:GetChildren())
            local v296 = nil

            while true do
                local v297

                v295, v297 = v293(v294, v295)

                if v295 == nil then
                    break
                end
                if v297.Value > 0 then
                    local _Position3 = v297:GetAttribute('Position')
                    local v299

                    if typeof(_Position3) ~= 'Vector3' then
                        v299 = false
                    else
                        v299 = _LocalPlayer:DistanceFromCharacter(_Position3)
                    end
                    if v299 then
                        if v299 <= _huge2 then
                            v296 = v297
                            _huge2 = v299
                        end
                    end
                end
            end

            u291 = v296

            return v296
        end
        local function u304(p301)
            for v302 = 1, 3 do
                local v303 = p301:FindFirstChild('Torch' .. v302)

                if v303 then
                    if v303:FindFirstChild('ProximityPrompt') then
                        if v303.ProximityPrompt.Enabled then
                            return v303
                        end
                    end
                end
            end
        end
        local function u308(p305)
            for v306 = 1, 3 do
                local v307 = p305:FindFirstChild('Pedestal' .. v306)

                if v307 then
                    if v307:FindFirstChild('ProximityPrompt') then
                        if v307.ProximityPrompt.Enabled then
                            return v307
                        end
                    end
                end
            end
        end
        local function u317(p309)
            local _huge3 = math.huge
            local v311, v312, v313 = ipairs(_ReplicatedStorage.NPCs:GetChildren())
            local v314 = nil

            while true do
                local v315

                v313, v315 = v311(v312, v313)

                if v313 == nil then
                    break
                end
                if v315.Name == 'Luxury Boat Dealer' and not p309[v315] then
                    local _PrimaryPart3 = v315.PrimaryPart

                    if _PrimaryPart3 and _LocalPlayer:DistanceFromCharacter(_PrimaryPart3.Position) <= _huge3 then
                        _huge3 = _LocalPlayer:DistanceFromCharacter(_PrimaryPart3.Position)
                        v314 = v315
                    end
                end
            end

            return v314
        end

        local v329 = {
            function(p318, _)
                if VerifyTool('Yama') then
                    _EquipTool2('Yama')

                    local _ForestPirate = _EnemySpawned2('Forest Pirate')

                    if _ForestPirate and _ForestPirate.PrimaryPart then
                        u82.AttackCooldown = tick()

                        u83(_ForestPirate.PrimaryPart.CFrame * CFrame.new(0, 0, -2))
                    else
                        u83(p318.ForestPirate)
                    end
                else
                    _FireRemote2('LoadItem', 'Yama')
                end

                return true
            end,
            function(_, _)
                local v320 = _LocalPlayer:FindFirstChild('QuestHaze') and u300()

                if v320 then
                    local _Name = v320.Name
                    local v322 = _EnemySpawned2(_Name)

                    if v322 and v322.PrimaryPart then
                        _Managers.FarmManager.attack(v322, true)
                    elseif _EnemyLocations3[_Name] then
                        _Managers.PlayerTeleport:NPCs(_EnemyLocations3[_Name])
                    else
                        u83(v320:GetAttribute('Position'))
                    end

                    return true
                end
            end,
            function(p323, p324)
                local _HellDimension = _Map:FindFirstChild('HellDimension')

                if _HellDimension then
                    local v326 = u304(_HellDimension) or _HellDimension:FindFirstChild('Exit')

                    if v326 and _LocalPlayer:DistanceFromCharacter(v326.Position) <= 600 then
                        local v327 = _EnemySpawned2(p323.Hell)

                        if v327 and v327.PrimaryPart then
                            u83(v327.PrimaryPart.CFrame + u38.FarmPos)

                            return true, u82.KillAura(125)
                        end
                        if v326.Name == 'Exit' or _LocalPlayer:DistanceFromCharacter(v326.Position) >= 5 then
                            u83(v326.CFrame)
                        else
                            fireproximityprompt(v326.ProximityPrompt)
                        end
                    end

                    return true
                end
                if not _IsSpawned('Soul Reaper') then
                    return p324.SoulReaper() or p324.Bones()
                end

                local _SoulReaper = _EnemySpawned2('Soul Reaper')

                if _SoulReaper and _SoulReaper.PrimaryPart and _LocalPlayer:DistanceFromCharacter(_SoulReaper.PrimaryPart.Position) > 6 then
                    u83(_SoulReaper.PrimaryPart.CFrame * CFrame.new(0, 0, -2))

                    return true
                end
            end,
        }

        u285.CursedDualKatana.Yama = v329

        local v338 = {
            function(p330, _)
                if _LocalPlayer:FindFirstChild('BoatQuest') then
                    local _CurrentDealer = p330.CurrentDealer

                    if not _CurrentDealer or p330.BoatsDealer[_CurrentDealer] then
                        _CurrentDealer = _NPCs:FindFirstChild('Luxury Boat Dealer')

                        if not (_CurrentDealer and _CurrentDealer.PrimaryPart) or p330.BoatsDealer[_CurrentDealer] then
                            _CurrentDealer = u317(p330.BoatsDealer)
                        end
                    end
                    if _CurrentDealer and _CurrentDealer.PrimaryPart then
                        if p330.CurrentDealer ~= _CurrentDealer then
                            p330.CurrentDealer = _CurrentDealer
                        end
                        if _LocalPlayer:DistanceFromCharacter(_CurrentDealer.PrimaryPart.Position) >= 5 then
                            return true, u83(_CurrentDealer.PrimaryPart.CFrame)
                        end
                        if _FireRemote2('CDKQuest', 'BoatQuest', _CurrentDealer, 'Check') then
                            _FireRemote2('CDKQuest', 'BoatQuest', _CurrentDealer)
                        end

                        p330.BoatsDealer[_CurrentDealer] = true
                    else
                        task.wait(0.5)
                    end
                end
            end,
            function(_, p332)
                return p332.PirateRaid()
            end,
            function(p333, _)
                local _HeavenlyDimension = _Map:FindFirstChild('HeavenlyDimension')

                if _HeavenlyDimension then
                    local v335 = u304(_HeavenlyDimension) or _HeavenlyDimension:FindFirstChild('Exit')

                    if v335 and _LocalPlayer:DistanceFromCharacter(v335.Position) <= 600 then
                        local v336 = _EnemySpawned2(p333.Heaven)

                        if v336 and v336.PrimaryPart then
                            u83(v336.PrimaryPart.CFrame + u38.FarmPos)

                            return true, u82.KillAura(125)
                        end
                        if v335.Name == 'Exit' or _LocalPlayer:DistanceFromCharacter(v335.Position) >= 5 then
                            u83(v335.CFrame)
                        else
                            fireproximityprompt(v335.ProximityPrompt)
                        end
                    end

                    return true
                end
                if _IsSpawned('Cake Queen') then
                    local _CakeQueen = _EnemySpawned2('Cake Queen')

                    if _CakeQueen and _CakeQueen.PrimaryPart then
                        _Managers.FarmManager.attack(_CakeQueen)
                    else
                        u83(p333.CakeQueen)
                    end

                    return true
                end
            end,
        }

        u285.CursedDualKatana.Tushita = v338

        function u285.CursedDualKatana.FinalQuest(p339, _)
            if VerifyTool('Tushita') or VerifyTool('Yama') then
                if _IsSpawned('Cursed Skeleton Boss') then
                    local _CursedSkeletonBoss = _EnemySpawned2('Cursed Skeleton Boss')

                    if not (_CursedSkeletonBoss and _CursedSkeletonBoss.PrimaryPart) then
                        return nil
                    end

                    _EquipTool2('Sword', true)
                    _Managers.FarmManager.ToolDebounce()
                    _Managers.FarmManager.attack(_CursedSkeletonBoss)

                    return true
                end
                if _LocalPlayer.PlayerGui.Main.Dialogue.Visible then
                    _VirtualUser:ClickButton1(Vector2.new(10000, 10000))
                end

                local v341 = u308(_Map.Turtle.Cursed)

                if v341 then
                    if _LocalPlayer:DistanceFromCharacter(v341.Position) >= 5 then
                        u83(v341.CFrame)
                    else
                        fireproximityprompt(v341.ProximityPrompt)
                    end

                    return true
                end

                local v342 = _LocalPlayer:DistanceFromCharacter(p339.CursedSkeleton[1].Position)

                if v342 > 6 then
                    u83(p339.CursedSkeleton[1], v342 <= 100 and 40 or false)
                else
                    u83(p339.CursedSkeleton[2])
                end

                task.wait(0.5)

                return true
            end

            _FireRemote2('LoadItem', 'Yama')
        end
    end
    if u82.GameData.Sea == 3 then
        local u343 = CFrame.new(5867, 1208, 872)
        local u344 = CFrame.new(5771, 1209, 804)
        local _RFInteractDragonQuest = _Net:WaitForChild('RF/InteractDragonQuest')
        local _Count = u82.Inventory.Count
        local _Unlocked2 = u82.Inventory.Unlocked
        local u348 = {
            Progress = {},
            CurrentBelt = 'Null',
            YellowQuest = ToDictionary({
                'Piranha',
                'Shark',
            }),
            RedQuest = ToDictionary({
                'Terrorshark',
                'Sea Beast',
            }),
        }
        local u349 = {
            CheckStart = {
                'CanTransform',
                'CanLearnTether',
                'TetherLearned',
                'AvailableVQuest',
            },
            Complete = {
                NPC = 'Dragon Wizard',
                Command = 'Ascension',
                Action = 'Complete',
            },
            Begin = {
                NPC = 'Dragon Wizard',
                Command = 'Ascension',
                Action = 'Begin',
            },
            LearnTether = {
                NPC = 'Dragon Wizard',
                Command = 'LearnTether',
            },
            BuyDraco = {
                NPC = 'Dragon Wizard',
                Command = 'DragonRace',
            },
        }
        local u350 = {
            DojoClaim = {
                NPC = 'Dojo Trainer',
                Command = 'ClaimQuest',
            },
            DojoProgress = {
                NPC = 'Dojo Trainer',
                Command = 'RequestQuest',
            },
            SpeakWizard = {
                NPC = 'Dragon Wizard',
                Command = 'Speak',
            },
            RaceV3 = ToDictionary({
                'Terrorshark',
                'Sea Beast',
            }),
        }

        function u348.CollectReward(_, p351)
            if _Unlocked2['Dojo Belt (' .. p351 .. ')'] then
                u348.Progress[p351] = nil

                return nil
            else
                if _LocalPlayer:DistanceFromCharacter(u343.Position) > 3 then
                    u83(u343)
                else
                    _RFInteractDragonQuest:InvokeServer(u350.DojoClaim)

                    u285.CurrentBeltQuest = nil
                end

                return true
            end
        end
        function u348.White(p352, p353)
            if p352.Progress.White < 20 then
                return p353.Level()
            else
                return p352:CollectReward('White')
            end
        end
        function u348.Green(p354)
            if p354.Progress.Green >= 330 then
                return p354:CollectReward('Green')
            end
            if _LocalPlayer:GetAttribute('DangerLevel') >= 500 and p354.GreenTimer then
                p354.Progress.Green = p354.Progress.Green + (tick() - p354.GreenTimer)
            end

            p354.GreenTimer = tick()

            if _Managers.SeaManager:GetPlayerBoat() then
                _Managers.SeaManager:RandomTeleport('inf')
            else
                _Managers.SeaManager:BuyNewBoat()
            end

            return true
        end
        function u348.Purple(p355, p356)
            if p355.Progress.Purple >= 3 then
                return p355:CollectReward('Purple')
            end
            if p355.PurpleProgress then
                if p356.EliteHunter() then
                    return true
                end

                local v357 = u82

                p355.Progress.Purple = p355.StartPurpleProgress + (v357:GetProgress('EliteProgress', 'EliteHunter', 'Progress') - p355.PurpleProgress)
            else
                p355.StartPurpleProgress = p355.Progress.Purple
                p355.PurpleProgress = u82:GetProgress('EliteProgress', 'EliteHunter', 'Progress')
            end
        end
        function u348.Red(p358, p359)
            if p358.Progress.Red < 1 then
                return p359.Sea(p358.RedQuest)
            else
                return p358:CollectReward('Red')
            end
        end
        function u348.Yellow(p360, p361)
            if p360.Progress.Yellow < 5 then
                return p361.Sea(p360.YellowQuest)
            else
                return p360:CollectReward('Yellow')
            end
        end
        function u348.Blue(p362, p363)
            if p362.Progress.Blue >= 1 then
                return p362:CollectReward('Blue')
            end
            if _LocalPlayer.Character then
                local _Tool = _LocalPlayer.Character:FindFirstChildOfClass('Tool')

                if _Tool and _Tool:FindFirstChild('Fruit') and (_Tool.ToolTip ~= 'Blox Fruit' and _Tool:GetAttribute('DroppedBy')) and _Tool:GetAttribute('DroppedBy'):len() > 0 then
                    p362.Progress.Blue = 1

                    return nil
                end

                local v365, v366, v367 = ipairs(_LocalPlayer.Backpack:GetChildren())

                while true do
                    local v368

                    v367, v368 = v365(v366, v367)

                    if v367 == nil then
                        break
                    end
                    if v368:IsA('Tool') and v368:FindFirstChild('Fruit') and (v368.ToolTip ~= 'Blox Fruit' and _Tool:GetAttribute('DroppedBy')) and _Tool:GetAttribute('DroppedBy'):len() > 0 then
                        p362.Progress.Blue = 1

                        return nil
                    end
                end

                local _ = p363.Fruits
            end
        end
        function u348.Black(p369, p370)
            if p369.Progress.Black < 3 then
                if p369.BlackProgress then
                    p369.Progress.Black = _Count['Dinosaur Bones'] - p369.BlackProgress

                    return p370.LavaGolem() or p370.PrehistoricBones() or p370.PrehistoricIsland()
                else
                    p369.BlackProgress = p369.Progress.Black - _Count['Dinosaur Bones']

                    return true
                end
            else
                return p369:CollectReward('Black')
            end
        end
        function u285.BeltProgress(p371, p372, p373)
            if u348.CurrentBelt ~= p372 then
                if p371.CurrentDracoQuest and p371.CurrentDracoQuest.AvailableVQuest == 'V3InProgress' then
                    p371.KilledTerrorshark = true
                end
            else
                u348.Progress[p372] = u348.Progress[p372] + p373
            end
        end
        function u285.BeltQuest(p374, p375, p376)
            local _BeltName = p375.BeltName

            if u348[_BeltName] then
                if _Unlocked2['Dojo Belt (' .. _BeltName .. ')'] then
                    return p374:GetNextBeltQuest()
                end
                if not (u348.Progress[_BeltName] and p375.UpdatedProgress) then
                    local _Progress = u348.Progress
                    local _Progress2 = p375.Progress

                    p375.UpdatedProgress = true
                    _Progress[_BeltName] = _Progress2
                end

                u348.CurrentBelt = _BeltName

                if u348[_BeltName](u348, p376) then
                    return 'Belt Quest: ' .. _BeltName
                end
            end
        end
        function u285.GetNextBeltQuest(p380)
            if _LocalPlayer:DistanceFromCharacter(u343.Position) > 5 then
                u83(u343)
            else
                p380.CurrentBeltQuest = _RFInteractDragonQuest:InvokeServer(u350.DojoProgress)
            end

            return 'Getting Belt Quest'
        end
        function u285.BeltQuests(p381, p382)
            local _CurrentBeltQuest = p381.CurrentBeltQuest

            if type(_CurrentBeltQuest) ~= 'table' then
                local _ = p381.GetNextBeltQuest
            else
                if _CurrentBeltQuest.Timeout or _CurrentBeltQuest.Completed then
                    return nil
                end
                if _CurrentBeltQuest.Quest then
                    return p381:BeltQuest(_CurrentBeltQuest.Quest, p382)
                end
            end
        end
        function u285.SpeakWizard(p384)
            if _LocalPlayer:DistanceFromCharacter(u344.Position) > 5 then
                u83(u344)
            else
                p384.CurrentDracoQuest = _RFInteractDragonQuest:InvokeServer(u350.SpeakWizard)
            end

            return 'Teleporting to NPC: Dragon Wizard'
        end
        function u285.TalkNpc(p385, p386, p387, p388)
            if _LocalPlayer:DistanceFromCharacter(p386.Position) > 5 then
                u83(p386)
            elseif _RFInteractDragonQuest:InvokeServer(p387) and p388 then
                p385[p388] = nil
            end

            return 'Teleporting to NPC: ' .. (p387.NPC or '???')
        end
        function u285.GetDracoRace(p389, p390)
            if not _Unlocked2['Dojo Belt (Black)'] then
                return p390.DojoTrainer()
            end

            local _CurrentDracoQuest = p389.CurrentDracoQuest

            if type(_CurrentDracoQuest) ~= 'table' then
                local _ = p389.SpeakWizard
            else
                if not (_CurrentDracoQuest.TetherLearned or _CurrentDracoQuest.CanLearnTether) then
                    return nil
                end
                if not _CurrentDracoQuest.FoundPrehistoric then
                    return p390.PrehistoricBones() or p390.PrehistoricEgg() or (p390.LavaGolem() or p390.PrehistoricIsland())
                end
                if _Data.Race.Value ~= 'Draco' then
                    if _CurrentDracoQuest.CanTransform or _CurrentDracoQuest.CanTransformFree then
                        return p389:TalkNpc(u344, u349.BuyDraco, 'CurrentDracoQuest')
                    elseif _CurrentDracoQuest.TetherLearned then
                        if _Unlocked2['Dragon Egg'] then
                            return p389:TalkNpc(u344, u349.BuyDraco, 'CurrentDracoQuest')
                        else
                            return p390.PrehistoricBones() or p390.PrehistoricEgg() or (p390.LavaGolem() or p390.PrehistoricIsland())
                        end
                    else
                        return p389:TalkNpc(u344, u349.LearnTether, 'CurrentDracoQuest')
                    end
                end

                local _AvailableVQuest = _CurrentDracoQuest.AvailableVQuest

                if _AvailableVQuest == 'V2' or _AvailableVQuest == 'V3' then
                    return p389:TalkNpc(u344, u349.Begin, 'CurrentDracoQuest')
                end
                if _AvailableVQuest == 'V2InProgress' then
                    if _Count['Fire Flower'] < 5 then
                        return u45.EliteHunter and p390.EliteHunter() or u45.BerryBush and u45.BerryBush() or p390.FireFlowers(5)
                    else
                        return p389:TalkNpc(u344, u349.Complete, 'CurrentDracoQuest')
                    end
                end
                if _AvailableVQuest == 'V3InProgress' then
                    if p389.KilledTerrorshark then
                        return p389:TalkNpc(u344, u349.Complete, 'CurrentDracoQuest')
                    else
                        return p390.Sea(u350.RaceV3)
                    end
                end
                if _AvailableVQuest == 'V2TurnInReady' then
                    if _Data.Level.Value < 1000000 then
                        return p390.Level()
                    else
                        return p389:TalkNpc(u344, u349.Complete, 'CurrentDracoQuest')
                    end
                end
                if _AvailableVQuest == 'V3TurnInReady' then
                    if _Data.Level.Value < 3000000 then
                        return p390.Level()
                    else
                        return p389:TalkNpc(u344, u349.Complete, 'CurrentDracoQuest')
                    end
                end
            end
        end
    end

    return u285
end
function _Managers.IslandManager()
    return {
        Islands = {},
        GetMirageFruitDealer = function(p393)
            if p393.MirageFruitDealer then
                return p393.MirageFruitDealer
            end

            local v394 = _NPCs:FindFirstChild('Advanced Fruit Dealer') or _ReplicatedStorage.NPCs:FindFirstChild('Advanced Fruit Dealer')

            if v394 then
                p393.MirageFruitDealer = v394

                return v394
            end
        end,
        GetMirageGear = function(p395, p396)
            if p395.MirageGear and p395.MirageGear.Parent then
                return p395.MirageGear
            end

            local v397, v398, v399 = ipairs(p396:GetChildren())

            while true do
                local v400

                v399, v400 = v397(v398, v399)

                if v399 == nil then
                    break
                end
                if v400:IsA('MeshPart') and v400.MeshId == 'rbxassetid://10153114969' then
                    p395.MirageGear = v400

                    return v400
                end
            end
        end,
        GetMirageTop = function(p401, p402)
            if p401.MirageTop and p401.MirageTop.Parent then
                return p401.MirageTop
            end

            local v403, v404, v405 = ipairs(p402:GetChildren())

            while true do
                local v406

                v405, v406 = v403(v404, v405)

                if v405 == nil then
                    break
                end

                local _dbz_map1_Cube012 = v406:FindFirstChild('dbz_map1_Cube.012')

                if _dbz_map1_Cube012 then
                    p401.MirageTop = _dbz_map1_Cube012

                    return _dbz_map1_Cube012
                end
            end
        end,
        GetPrehistoricActivationPrompt = function(p408, p409)
            local _PrehistoricPrompt = p408.PrehistoricPrompt

            if _PrehistoricPrompt and _PrehistoricPrompt:IsDescendantOf(_Map) then
                return _PrehistoricPrompt
            end

            local _Core = p409:FindFirstChild('Core')

            if _Core and _Core:FindFirstChild('ActivationPrompt') then
                p408.PrehistoricPrompt = _Core.ActivationPrompt

                return _Core.ActivationPrompt
            end
        end,
        GetSpawnedIsland = function(p412, p413)
            local v414 = p412.Islands[p413]

            if v414 and v414.Parent == _Map then
                return v414
            end

            local v415 = _Map:FindFirstChild(p413)

            if v415 then
                p412.Islands[p413] = v415

                return v415
            end
        end,
    }
end
function _Managers.EspManager()
    local u416 = {}

    u416.__index = u416

    function u416.__newindex(p417, p418, p419)
        if p418 == 'Enabled' then
            return task.spawn(p417.toggle, p417, p419)
        else
            return rawset(p417, p418, p419)
        end
    end

    local function u421(p420)
        if p420:FindFirstChild('Humanoid') then
            return p420.PrimaryPart or p420
        elseif p420:FindFirstChild('Handle') then
            return p420.Handle
        else
            return p420
        end
    end
    local function u423(p422)
        if p422.Object and p422.Section.List[p422.Object] then
            p422.Section.List[p422.Object] = nil
        end
        if p422.EspHandle then
            p422.EspHandle:Destroy()
        end
    end

    local _FruitsName = u82.FruitsName
    local u425 = "%s<font color='rgb(160, 160, 160)'> [ %im ]</font>\n<font color='rgb(25, 240, 25)'>[%i/%i]</font>"
    local _Folder = Instance.new('Folder', _CoreGui)

    _Folder.Name = 'rz_EspFolder'

    local v427 = _CoreGui:FindFirstChild(_Folder.Name)

    if v427 and v427 ~= _Folder then
        v427:Destroy()
    end

    function u416.new(p428, p429, p430, p431)
        local v432 = setmetatable({}, u416)
        local _Folder2 = Instance.new('Folder', _Folder)

        _Folder2.Name = p428
        v432.List = {}
        v432.Name = p428
        v432.Folder = _Folder2
        v432.IsEnabled = p431
        v432.Instance = p429
        v432.IsEspObject = p430

        return v432
    end
    function u416.clear(p434)
        p434.Folder:ClearAllChildren()
        table.clear(p434.List)
    end
    function u416.add(p435, p436, p437, p438, _)
        local u439 = {
            Section = p435,
            Color = p437 or Color3.fromRGB(255, 255, 255),
            Name = p438 or p436.Name,
            Object = p436,
            EspHandle = nil,
        }
        local _BoxHandleAdornment = Instance.new('BoxHandleAdornment')

        _BoxHandleAdornment.Size = Vector3.new(1, 0, 1, 0)
        _BoxHandleAdornment.AlwaysOnTop = true
        _BoxHandleAdornment.ZIndex = 10
        _BoxHandleAdornment.Transparency = 0

        local _BillboardGui = Instance.new('BillboardGui')

        _BillboardGui.Adornee = p436
        _BillboardGui.Size = UDim2.new(0, 100, 0, 150)
        _BillboardGui.StudsOffset = Vector3.new(0, 2, 0)
        _BillboardGui.AlwaysOnTop = true

        local _TextLabel = Instance.new('TextLabel')

        _TextLabel.BackgroundTransparency = 1
        _TextLabel.Position = UDim2.new(0, 0, 0, -50)
        _TextLabel.Size = UDim2.new(0, 100, 0, 100)
        _TextLabel.TextSize = 10
        _TextLabel.TextColor3 = u439.Color
        _TextLabel.TextStrokeTransparency = 0
        _TextLabel.TextYAlignment = Enum.TextYAlignment.Bottom
        _TextLabel.Text = '...'
        _TextLabel.ZIndex = 15
        _TextLabel.RichText = true
        _TextLabel.Parent = _BillboardGui
        _BillboardGui.Parent = _BoxHandleAdornment
        _BoxHandleAdornment.Parent = p435.Folder
        u439.EspHandle = _BoxHandleAdornment

        task.spawn(function()
            local _IsEnabled = p435.IsEnabled
            local _EspHandle = u439.EspHandle
            local _Object = u439.Object

            while true do
                if not (u38.SmoothMode and task.wait(0.25)) then
                    _Stepped:Wait()
                end
                if not (_Object and _Object:IsDescendantOf(workspace) and _EspHandle) or _IsEnabled and not _IsEnabled(_Object) then
                    return u423(u439)
                end

                local v446 = u421(_Object)

                if not v446 then
                    return u423(u439)
                end
                if v446:IsA('Model') then
                    v446 = v446:GetPivot()
                end

                local v447 = _LocalPlayer
                local v448 = math.floor(v447:DistanceFromCharacter(v446.Position) / 5)
                local _Humanoid4 = _Object:FindFirstChildOfClass('Humanoid')

                if _Humanoid4 then
                    _TextLabel.Text = u425:format(u439.Name, v448, math.floor(_Humanoid4.Health), math.floor(_Humanoid4.MaxHealth))
                elseif _Object.Parent ~= workspace or _Object.Name ~= 'Fruit ' then
                    _TextLabel.Text = ('%s < %i >'):format(u439.Name, v448)
                else
                    _TextLabel.Text = 'Fruit [ ??? ]'
                    _TextLabel.Text = ('%s < %i >'):format(_FruitsName[_Object], v448)
                end
            end
        end)

        return u439
    end
    function u416.toggle(p450, p451)
        local v452 = 'Esp' .. p450.Name

        u32[v452] = p451

        local _IsEnabled2 = p450.IsEnabled
        local _Instance = p450.Instance
        local _IsEspObject = p450.IsEspObject

        while u32[v452] do
            local v456

            if type(_Instance) ~= 'table' or not _Instance then
                v456 = _Instance:GetChildren()
            else
                v456 = _Instance
            end

            for v457 = 1, #v456 do
                local v458 = v456[v457]

                if not p450.List[v458] then
                    local v459, v460, v461, v462 = _IsEspObject(v458)

                    if v459 then
                        p450.List[v458] = p450:add(v462 or v458, v460, v461, _IsEnabled2)
                    end
                end
            end

            task.wait(0.25)
        end

        p450:clear()
    end

    return u416
end
function _Managers.SeaManager()
    if u82.GameData.Sea == 1 then
        return nil
    end

    local v463 = {
        oldTool = 'Melee',
        SeaEvents = {},
        BoatTweenDebounce = 0,
        randomNumber = 1,
        toolDebounce = 0,
        rdDebounce = 0,
        nextNum = 1,
        SeaEnemyVector = Vector3.new(0, 32, 0),
        DodgeVector = Vector3.new(0, 160, 0),
        nextTool = {
            Melee = 'Blox Fruit',
            ['Blox Fruit'] = 'Sword',
            Sword = 'Gun',
            Gun = 'Melee',
        },
        BuyBoat = {
            Position = u82.GameData.Sea == 2 and CFrame.new(94, 10, 2951) or CFrame.new(-6123, 16, -2247),
            TikiIsland = CFrame.new(-16917, 9, 510),
            BoatName = 'BeastHunter',
            OthersBoats = {
                'BeastHunter',
                'Guardian',
                'Lantern',
                'Sleigh',
                'PirateGrandBrigade',
                'MarineGrandBrigade',
            },
        },
        RandomPosition = ({
            false,
            {
                CFrame.new(-43, 21, 5054),
                CFrame.new(1744, 21, 4393),
                CFrame.new(1003, 21, 3598),
                CFrame.new(-935, 21, 3813),
            },
            {
                inf = -100000000,
                ['6'] = -43200,
                ['5'] = -38200,
                ['4'] = -34000,
                ['3'] = -30000,
                ['2'] = -26000,
                ['1'] = -22000,
            },
        })[u82.GameData.Sea],
        Directions = {
            Vector3.new(60, 0, 0),
            Vector3.new(0, 0, 60),
            Vector3.new(-60, 0, 0),
            Vector3.new(0, 0, -60),
            Vector3.new(0, 0, 0),
        },
        TerrorSkills = {
            'FinalSpinAttachment',
            'GroundExplosionSplashStart',
            'SpinSlash',
            'SpinSlash3',
            'SpinSlash4',
        },
    }
    local _ = u82.Inventory.Unlocked
    local _Count2 = u82.Inventory.Count
    local _IsAlive3 = u82.IsAlive
    local _UseSkills = u82.UseSkills
    local _EquipTool3 = u82.EquipTool
    local _FireRemote3 = u82.FireRemote
    local u469 = nil
    local _SubclassNetwork = _Remotes:WaitForChild('SubclassNetwork')

    if u82.GameData.Sea == 3 then
        local _RandomPosition = v463.RandomPosition
        local v472, v473, v474 = pairs(_RandomPosition)

        while true do
            local v475

            v474, v475 = v472(v473, v474)

            if v474 == nil then
                break
            end

            _RandomPosition[v474] = {
                CFrame.new(v475, 21, 500),
                CFrame.new(v475 - 3000, 21, 500),
                CFrame.new(v475 - 3000, 21, 2000),
                CFrame.new(v475, 21, -1000),
            }
        end
    end

    function v463.IsOwner(p476)
        local _Owner = p476:FindFirstChild('Owner')

        if _Owner then
            _Owner = p476.Owner.Value.Name == _LocalPlayer.Name
        end

        return _Owner
    end
    function v463.GetPlayerBoat(p478)
        if _IsAlive3(_LocalPlayer.Character) then
            local _PlayerBoat = p478.PlayerBoat

            if _PlayerBoat and (not _PlayerBoat:FindFirstChild('Health') or _IsAlive3(_PlayerBoat)) and _PlayerBoat:IsDescendantOf(_Boats) then
                return _PlayerBoat
            end

            local _SeatPart = _LocalPlayer.Character.Humanoid.SeatPart

            if _SeatPart and _SeatPart.Name == 'VehicleSeat' then
                p478.PlayerBoat = _SeatPart.Parent

                return p478.PlayerBoat
            end

            local v481 = _Boats
            local v482, v483, v484 = ipairs(v481:GetChildren())

            while true do
                local v485

                v484, v485 = v482(v483, v484)

                if v484 == nil then
                    break
                end
                if (not v485:FindFirstChild('Health') or _IsAlive3(v485)) and p478.IsOwner(v485) then
                    if v485.Name ~= p478.BuyBoat.BoatName then
                        p478.BuyBoat.BoatName = v485.Name
                    end

                    p478.PlayerBoat = v485

                    return v485
                end
            end
        end
    end
    function v463.BuyNewBoat(p486)
        if not u82.IsAlive(_LocalPlayer.Character) then
            return nil
        end

        local _BuyBoat = p486.BuyBoat
        local _Position4 = _BuyBoat.Position

        if u82.GameData.Sea == 3 then
            local v489 = _LocalPlayer

            if _LocalPlayer:DistanceFromCharacter(_BuyBoat.TikiIsland.Position) < v489:DistanceFromCharacter(_Position4.Position) then
                _Position4 = _BuyBoat.TikiIsland
            end
        end
        if _LocalPlayer:DistanceFromCharacter(_Position4.Position) >= 10 then
            u83(_Position4)
        elseif _FireRemote3('BuyBoat', _BuyBoat.BoatName) ~= 1 then
            for v490 = 1, #_BuyBoat.OthersBoats do
                local v491 = _BuyBoat.OthersBoats[v490]

                if v491 ~= _BuyBoat.BoatName then
                    if _FireRemote3('BuyBoat', v491) == 1 then
                        break
                    end
                end
            end
        end
    end
    function v463.teleportBoat(p492, p493, p494, p495)
        if tick() - p492.BoatTweenDebounce >= 0.5 then
            local _Unit = (p494.Position - p493.Position).Unit

            u82.Tween.Velocity = _Unit * (p495 or u38.BoatSpeed)

            u82:RemoveBoatCollision(p493.Parent)

            p492.BoatTweenDebounce = tick()
        end
    end
    function v463.StopBoat(_)
        u82.Tween.Velocity = Vector3.zero
    end
    function v463.GetSelectedLevel(p497, p498)
        return p497.RandomPosition[p498 or u38.SeaLevel]
    end
    function v463.RandomTeleport(p499, p500)
        if not u469 or u469.Health <= 0 then
            local _Character = _LocalPlayer.Character

            if _Character then
                _Character = _LocalPlayer.Character:FindFirstChild('Humanoid')
            end

            u469 = _Character

            return nil
        end
        if not u469.SeatPart then
            return p499:TeleportToBoat()
        end

        local _PrimaryPart4 = p499:GetPlayerBoat().PrimaryPart

        if not _PrimaryPart4 then
            return nil
        end

        local _Position5 = _PrimaryPart4.Position
        local v504 = u82.GameData.Sea == 3 and p499:GetSelectedLevel(p500) or p499.RandomPosition

        if #v504 ~= 1 then
            if #v504 > 1 then
                if p499.nextNum > #v504 then
                    p499.nextNum = 1
                end

                local v505 = v504[p499.nextNum]

                if (_Position5 - v505.Position).Magnitude >= 100 then
                    p499:teleportBoat(_PrimaryPart4, v505)
                else
                    p499.nextNum = p499.nextNum + 1
                end
            end
        else
            p499:teleportBoat(_PrimaryPart4, v504[1])
        end
    end
    function v463.RandomTool(p506)
        if tick() - p506.toolDebounce < 2 then
            return p506.oldTool
        end

        p506.toolDebounce = tick()

        local v507 = p506.nextTool[p506.oldTool]
        local v508 = 0

        while not VerifyToolTip(v507) do
            v507 = p506.nextTool[v507]
            v508 = v508 + 1

            if v508 >= 3 then
                p506.oldTool = v507

                return v507
            end
        end

        p506.oldTool = v507

        return v507
    end
    function v463.GetSeaEvent(_, p509)
        local v510 = _Enemies
        local v511, v512, v513 = ipairs(v510:GetChildren())

        while true do
            local v514

            v513, v514 = v511(v512, v513)

            if v513 == nil then
                break
            end
            if v514.Name == p509 and _IsAlive3(v514) then
                return v514
            end
        end
    end
    function v463.attackBoat(p515, p516)
        local _PrimaryPart5 = p516.PrimaryPart

        if not _PrimaryPart5 then
            return nil
        end

        local v518 = _PrimaryPart5.CFrame + Vector3.new(0, 20, 0)

        EnableBuso()
        u83(v518)
        p515:StopBoat()

        if _LocalPlayer:DistanceFromCharacter(v518.Position) < 50 then
            _UseSkills(_PrimaryPart5, u38.SeaSkills)
            _EquipTool3(p515:RandomTool(), true)
        end
    end
    function v463.attackFish(p519, p520)
        local _PrimaryPart6 = p520.PrimaryPart

        if _PrimaryPart6 then
            if (p520.Name == 'Terrorshark' or p520.Name == 'Shark') and u38.DodgeShark then
                local _TerrorSkills = p519.TerrorSkills

                for v523 = 1, #_TerrorSkills do
                    local v524 = __WorldOrigin:FindFirstChild(_TerrorSkills[v523])

                    if v524 then
                        if (v524.Position - _PrimaryPart6.Position).Magnitude <= 100 then
                            return u83(_PrimaryPart6.CFrame + p519.DodgeVector)
                        end
                    end
                end
            end

            u83(_PrimaryPart6.CFrame + p519.SeaEnemyVector)
            _EquipTool3()
            EnableBuso()
            p519:StopBoat()
        end
    end
    function v463.StartHolding(_, p525)
        if not p525:GetAttribute('Repairing') then
            _VirtualInputManager:SendMouseButtonEvent(0, 0, 0, true, game, 1)
            print('Segurando o mouse')
            p525.AncestryChanged:Wait()
            _VirtualInputManager:SendMouseButtonEvent(0, 0, 0, false, game, 1)
            print('Parou de segurar')
        end
    end
    function v463.RepairBoat(p526, p527)
        local v528 = u38.RepairBoat and (_Subclass.Value == 'Shipwright' and 0 < _Count2['Wooden Plank']) and p527:FindFirstChild('Humanoid')

        if v528 and (p527:GetAttribute('__Repair') or v528.Value < (p527:GetAttribute('MaxHealth') or v528.Value) / 1.2) then
            local __RepairHammer = (_LocalPlayer.Character or _LocalPlayer.CharacterAdded:Wait()):FindFirstChild('_RepairHammer')

            if v528.Value >= (p527:GetAttribute('MaxHealth') or v528.Value) then
                p527:SetAttribute('__Repair', nil)
            else
                p527:SetAttribute('__Repair', true)
            end
            if not (__RepairHammer and __RepairHammer:WaitForChild('Marker')) then
                if p527:FindFirstChild('VehicleSeat') then
                    local v530 = p527.VehicleSeat.CFrame + Vector3.yAxis * 20

                    if _LocalPlayer:DistanceFromCharacter(v530.Position) > 5 then
                        u83(v530)
                    else
                        _SubclassNetwork.UseSubclass:InvokeServer({
                            Action = 'RequestHammer',
                        })
                    end
                end

                return true, p526:StopBoat(p527)
            end

            u83(__RepairHammer.Marker.Value.WorldCFrame + Vector3.xAxis * 10)
            task.spawn(p526.StartHolding, p526, __RepairHammer)

            return true
        end
        if _Subclass.Value == 'Shipwright' and u38.RepairBoat and _LocalPlayer.Character and _LocalPlayer.Character:FindFirstChild('_RepairHammer') then
            _SubclassNetwork.UseSubclass:InvokeServer({
                Action = 'RequestHammer',
            })
        end
    end
    function v463.attackSeaEvent(p531, p532)
        if p532:GetAttribute('IsBoat') then
            p531:attackBoat(p532)
        else
            p531:attackFish(p532)
        end
    end
    function v463.RandomDirection(p533)
        if tick() - p533.rdDebounce < 1.5 then
            return p533.Directions[p533.randomNumber]
        end

        p533.rdDebounce = tick()
        p533.randomNumber = math.random(#p533.Directions)

        return p533.Directions[p533.randomNumber]
    end
    function v463.attackSeaBeast(p534, p535)
        local v536 = p534:RandomDirection()
        local _HumanoidRootPart = p535:FindFirstChild('HumanoidRootPart')

        if not _HumanoidRootPart then
            return nil
        end

        local _Position6 = _HumanoidRootPart.Position
        local v539 = CFrame.new(_Position6.X, 25, _Position6.Z) + v536

        EnableBuso()
        u83(v539)
        p534:StopBoat()
        _EquipTool3(p534:RandomTool(), true)
        _UseSkills(v539, u38.SeaSkills)
    end
    function v463.GetSeaBeast(p540)
        local _SeaBeast = p540.SeaBeast

        if _SeaBeast and (_SeaBeast.Parent == _SeaBeasts and _IsAlive3(_SeaBeast)) then
            return _SeaBeast
        end

        local _huge4 = math.huge
        local v543 = _SeaBeasts
        local v544, v545, v546 = ipairs(v543:GetChildren())
        local v547 = nil

        while true do
            local v548

            v546, v548 = v544(v545, v546)

            if v546 == nil then
                break
            end
            if v548:IsA('Model') then
                local v549 = _LocalPlayer:DistanceFromCharacter(v548:GetPivot().Position)

                if _IsAlive3(v548) then
                    if v549 < _huge4 then
                        v547 = v548
                        _huge4 = v549
                    end
                end
            end
        end

        p540.SeaBeast = v547

        return v547
    end
    function v463.TeleportToBoat(p550)
        if not u469 or u469.Health <= 0 or not u469:IsDescendantOf(_Characters) then
            local _Character2 = _LocalPlayer.Character

            if _Character2 then
                _Character2 = _LocalPlayer.Character:FindFirstChild('Humanoid')
            end

            u469 = _Character2

            return nil
        end

        local _VehicleSeat = p550.VehicleSeat

        if _VehicleSeat and _VehicleSeat:IsDescendantOf(p550.PlayerBoat) then
            if u469.SeatPart and u469.SeatPart ~= _VehicleSeat then
                u469.Sit = false
            elseif _LocalPlayer:DistanceFromCharacter(_VehicleSeat.Position) >= 150 then
                u83(_VehicleSeat.CFrame)
            else
                _VehicleSeat:Sit(u469)
            end

            task.wait(0.25)
        elseif p550.PlayerBoat then
            p550.VehicleSeat = p550.PlayerBoat:FindFirstChild('VehicleSeat')
        end
    end

    return v463
end
function _Managers.FruitManager()
    local v553 = {
        RandomDebounce = 0,
        MoneyToReroll = 0,
    }
    local _IsAlive4 = u82.IsAlive
    local _ = u82.FruitsName
    local _Count3 = u82.Inventory.Count
    local _ = u82.Inventory.Unlocked

    function v553.GetRealFruitName(_, p556)
        local v557 = string.gsub(p556.Name, ' Fruit', '')

        return v557 .. '-' .. v557
    end
    function v553.CanStoreFruit(p558, p559)
        return _Count3[p558:GetRealFruitName(p559)] < _FruitCap.Value
    end
    function v553.StoreFruit(p560, p561)
        return u82.FireRemote('StoreFruit', p560:GetRealFruitName(p561), p561)
    end
    function v553.IsFruit(_, p562)
        local v563

        if string.sub(p562.Name, -6, -1) ~= ' Fruit' then
            v563 = false
        else
            v563 = p562:GetAttribute('DroppedBy')
        end

        return v563
    end
    function v553.GetInventoryItems(_)
        local v564 = _LocalPlayer.Backpack:GetChildren()
        local _Tool2 = _LocalPlayer.Character:FindFirstChildOfClass('Tool')

        if _Tool2 then
            table.insert(v564, _Tool2)
        end

        return v564
    end
    function v553.CanBuyMicrochip(p566)
        if not _IsAlive4(_LocalPlayer.Character) then
            return false
        end
        if _LocalPlayer:GetAttribute('IslandRaiding') then
            return false
        end
        if _LocalPlayer.Backpack:FindFirstChild('Microchip') or _LocalPlayer.Character:FindFirstChild('Microchip') then
            return false
        end

        local v567, v568, v569 = ipairs(p566:GetInventoryItems())

        while true do
            local v570

            v569, v570 = v567(v568, v569)

            if v569 == nil then
                break
            end
            if v570:IsA('Tool') and p566:IsFruit(v570) then
                return true
            end
        end

        return -1
    end
    function v553.GetStorableFruit(p571, p572)
        if not _IsAlive4(_LocalPlayer.Character) then
            return false
        end

        local v573, v574, v575 = ipairs(p571:GetInventoryItems())

        repeat
            local v576

            v575, v576 = v573(v574, v575)
        until v575 == nil or v576.Name ~= p572 and not _IsAlive4(_LocalPlayer.Character)
    end
    function v553.RerollRandomFruit(p577)
        if _Level.Value < 50 then
            return _Level:GetPropertyChangedSignal('Value'):Wait()
        end
        if _Beli.Value < p577.MoneyToReroll then
            return _Beli:GetPropertyChangedSignal('Value'):Wait()
        end
        if tick() - p577.RandomDebounce >= 1 then
            local _Cousin = u82.FireRemote('Cousin', 'Buy')

            if _Cousin == 1 then
                p577.RandomDebounce = tick() + 7200
            elseif _Cousin == 2 then
                local _, _, v579 = u82.FireRemote('Cousin', 'Check')

                p577.MoneyToReroll = v579 or 0
            elseif type(_Cousin) ~= 'string' or not _Cousin:match('%d%d:%d%d') then
                p577.RandomDebounce = tick() + 5
            else
                local _dd, v581 = _Cousin:match('(%d+):(%d+)')
                local v582 = tonumber(_dd)
                local v583 = tonumber(v581)

                if v582 and v583 then
                    local v584 = v582 * 60 * 60
                    local v585 = v583 * 60

                    p577.RandomDebounce = tick() + (v584 + v585)
                end
            end
        end
    end

    return v553
end
function u102.RunModules(p586)
    local v587 = next
    local _Managers2 = p586.Managers
    local v589 = nil

    while true do
        local v590

        v589, v590 = v587(_Managers2, v589)

        if v589 == nil then
            break
        end

        local v591, v592 = pcall(v590)

        if v591 then
            p586.Managers[v589] = v592
            u32[v589] = v592
        else
            u32[v589] = nil

            warn('falha ao carregar Module [ redz hub ]: ' .. v589 .. ' : ' .. v592)
        end
    end
end
function u102.Initialize(p593)
    u81 = __loadstring(u1.LibraryUrl or '{Owner}RedzLibV5/refs/heads/main/Source.lua')
    u82 = __loadstring(u1.ModuleUrl or '{Repository}Utils/Module.luau', ' return Module', {u38, u76})
    p593.IsCustomUrl = (u1.LibraryUrl or u1.ModuleUrl or u1.CustomFunctions) and true or false

    u102:RunModules()
end
function u102.LoadTabs(_, p594)
    return {
        Discord = p594:MakeTab({
            'Discord',
            'Info',
        }),
        MainFarm = p594:MakeTab({
            'Farm',
            'Home',
        }),
        Sea = p594:MakeTab({
            'Sea',
            'Waves',
        }),
        RaceV4 = p594:MakeTab({
            'Race-V4',
            '',
        }),
        Islands = p594:MakeTab({
            'Islands',
            'PalmTree',
        }),
        Items = p594:MakeTab({
            'Quests/Items',
            'Swords',
        }),
        FruitRaid = p594:MakeTab({
            'Fruit/Raid',
            'Cherry',
        }),
        Stats = p594:MakeTab({
            'Stats',
            'Signal',
        }),
        Teleport = p594:MakeTab({
            'Teleport',
            'Locate',
        }),
        Status = p594:MakeTab({
            'Status',
            'scroll',
        }),
        Visual = p594:MakeTab({
            'Visual',
            'User',
        }),
        Shop = p594:MakeTab({
            'Shop',
            'ShoppingCart',
        }),
        Misc = p594:MakeTab({
            'Misc',
            'Settings',
        }),
    }
end
function u102.InstallPlugin(_)
    return {
        Toggle = u82.RunFunctions.LibraryToggle(u45, u34),
    }
end
function u102.GetTranslation(_, p595)
    local v596 = {
        BR = 'Portuguese.json',
        VN = 'Vietnamese.json',
        TH = 'Thai.json',
    }

    if v596[p595] then
        local _ = _HttpService.JSONDecode
        local _ = __httpget
        local _ = '{Owner}BloxFruits/refs/heads/main/Translator/' .. v596[p595]
    end
end
function u102.Translator(p597, p598)
    if not u1.Translator then
        return p598
    end

    local v601, v602, v603 = pcall(function()
        local v599 = readfile

        if v599 then
            v599 = pcall(readfile, 'PlayerCountry.txt')
        end

        local v600 = nil

        if v599 and type(v600) == 'string' then
            return v600, true
        else
            return _LocalizationService:GetCountryRegionForPlayerAsync(_LocalPlayer)
        end
    end)

    if v601 and v602 and (v603 ~= true and writefile) then
        pcall(writefile, 'PlayerCountry.txt', v602)
    end
    if v601 then
        v601 = p597:GetTranslation(v602)
    end
    if v601 then
        local _ = u82.RunFunctions.Translator
    end

    return p598
end
function u102.DisableOption(_)
    if u38.RunningOption and u34[u38.RunningOption] then
        u34[u38.RunningOption]:Set(false, true)
    end
end
function u102.LoadLibrary(p604)
    local v605 = u81:MakeWindow({
        'redz Hub : Blox Fruits',
        'by real_redz',
        'redzHub-BloxFruits.json',
    })

    p604:Translator(v605)

    local v606 = p604:InstallPlugin(v605)
    local v607 = p604:LoadTabs(v605)
    local _FruitManager = p604.Managers.FruitManager
    local _QuestManager = p604.Managers.QuestManager
    local _FarmManager = p604.Managers.FarmManager
    local _FireRemote4 = u82.FireRemote
    local _Count4 = u82.Inventory.Count
    local _Unlocked3 = u82.Inventory.Unlocked
    local _Sea3 = u82.GameData.Sea
    local _Toggle = v606.Toggle

    v605:SelectTab(v607.MainFarm)
    v605:AddMinimizeButton({
        Button = {
            Image = 'rbxassetid://15298567397',
            BackgroundTransparency = 0,
        },
        Corner = {
            CornerRadius = UDim.new(0, 6),
        },
    })

    local _Discord = v607.Discord

    _Discord:AddDiscordInvite({
        Name = 'redz Hub | Community',
        Description = 'Join our discord community to receive information about the next update',
        Logo = 'rbxassetid://17382040552',
        Invite = 'https://discord.gg/7aR7kNVt4g',
    })
    _Discord:AddSection('')
    _Discord:AddParagraph({
        'Mentions:\n Honorable Mention: acsu123\n Honorable Mention 2: XFister',
    })

    local _MainFarm = v607.MainFarm
    local u618 = {
        Bigger = 380,
        Large = 450,
        Medium = 620,
        Small = 760,
    }
    local v619 = {
        {
            'Z',
            'X',
            'C',
            'V',
            'F',
        },
        ToDictionary({
            'Z',
            'X',
            'C',
            'V',
        }),
    }

    local function v621(p620)
        pcall(u81.SetScale, u81, u618[p620] or 450)
    end
    local function v624(p622)
        u32.TradeBones = p622

        while u32.TradeBones do
            task.wait()

            local _Bones = _Count4.Bones

            if _Bones >= 50 then
                _FireRemote4('Bones', 'Buy', 1, 1)

                if _Bones == _Count4.Bones then
                    task.wait(5)
                end
            else
                task.wait(0.5)
            end
        end
    end

    local u625 = nil

    local function v631()
        local v626, v627, v628 = pairs(u82.Bosses)
        local v629 = {}

        while true do
            local v630

            v628, v630 = v626(v627, v628)

            if v628 == nil then
                break
            end
            if u82.Enemies.IsSpawned(v628) then
                table.insert(v629, v628)
            end
        end

        u625:Set(v629)
    end

    _MainFarm:AddDropdown({
        'Select Tool',
        {
            'Melee',
            'Sword',
            'Blox Fruit',
            'Gun',
        },
        'Melee',
        {
            u38,
            'FarmTool',
        },
        'FarmTool',
    })
    _MainFarm:AddDropdown({
        'UI Scale',
        {
            'Small',
            'Medium',
            'Large',
            'Bigger',
        },
        'Large',
        v621,
        'UIScale',
    })
    _MainFarm:AddSection('Farm')
    _Toggle(_MainFarm, {
        'Auto Farm Level',
        'Level Farm',
    }, 'Level')
    _Toggle(_MainFarm, {
        'Auto Farm Nearest',
        'Farm Nearest Mobs',
    }, 'Nearest')

    if _Sea3 ~= 1 then
        if _Sea3 == 2 then
            _Toggle(_MainFarm, {
                'Auto Factory',
                'Spawns Every 1:30 [hours, minutes]',
            }, 'Factory')
            _MainFarm:AddSection('Ectoplasm')
            _Toggle(_MainFarm, {
                'Auto Farm Ectoplasm',
            }, 'Ectoplasm')
        elseif _Sea3 == 3 then
            _Toggle(_MainFarm, {
                'Auto Pirates Sea',
                'Auto Finish Pirate Raid in Sea Castle',
            }, 'PirateRaid')
            _MainFarm:AddSection('Bones')
            _Toggle(_MainFarm, {
                'Auto Farm Bones',
            }, 'Bones')
            _Toggle(_MainFarm, {
                'Auto Kill Soul Reaper',
            }, 'SoulReaper')
            _MainFarm:AddToggle({
                'Auto Trade Bones',
                false,
                v624,
                'TradeBones',
            })
        end
    end

    _MainFarm:AddSection('Chest')
    _Toggle(_MainFarm, {
        'Auto Chest [ Tween ]',
    }, 'ChestTween')
    _MainFarm:AddSection('Bosses')
    _MainFarm:AddButton({
        'Update Boss List',
        v631,
    })

    u625 = _MainFarm:AddDropdown({
        'Boss List',
        {},
        false,
        {
            u38,
            'BossSelected',
        },
        'B-Selected',
    })

    v631()
    _Toggle(_MainFarm, {
        'Auto Kill Boss Selected',
        'Kill boss Selected',
    }, 'BossSelected')
    _Toggle(_MainFarm, {
        'Auto Farm All Bosses',
        'Kill all bosses Spawned',
    }, 'AllBosses')
    _MainFarm:AddToggle({
        'Take Boss Quest',
        true,
        {
            u38,
            'BossQuest',
        },
        'B-Quest',
    })
    _MainFarm:AddSection('Material')

    local _AddDropdown = _MainFarm.AddDropdown
    local v633 = {}
    local v634 = {
        u38,
        'fMaterial',
    }

    __set_list(v633, 1, {
        'Material List',
        _FarmManager.Materials,
        false,
        v634,
        'S-Material',
    })
    _AddDropdown(_MainFarm, v633)
    _Toggle(_MainFarm, {
        'Auto Farm Material',
        'Farm material Selected',
    }, 'Material')
    _MainFarm:AddSection('Mastery')
    _MainFarm:AddSlider({
        'Select Enemy Health [ % ]',
        10,
        100,
        1,
        25,
        {
            u38,
            'mHealth',
        },
        'M-Health',
    })
    _MainFarm:AddDropdown({
        'Select Tool',
        {
            'Blox Fruit',
            'Gun',
        },
        {
            'Blox Fruit',
        },
        {
            u38,
            'mTool',
        },
        'M-Tool',
    })

    local _AddDropdown2 = _MainFarm.AddDropdown
    local v636 = {}
    local v637 = v619[1]
    local v638 = v619[2]
    local v639 = {
        u38,
        'MasterySkills',
    }

    v636.MultiSelect = true

    __set_list(v636, 1, {
        'Select Skills',
        v637,
        v638,
        v639,
        'M-Skills',
    })
    _AddDropdown2(_MainFarm, v636)
    _Toggle(_MainFarm, {
        'Auto Farm Mastery',
    }, 'Mastery')

    local _Sea4 = v607.Sea

    if _Sea3 == 1 then
        _Sea4:Destroy()
    elseif _Sea3 == 2 then
        local v641 = {
            {
                'Sea Beast',
                'PirateBrigade',
            },
            ToDictionary({
                'Sea Beast',
            }),
        }
        local v642 = {
            {
                'Z',
                'X',
                'C',
                'V',
                'F',
            },
            ToDictionary({
                'Z',
                'X',
                'C',
                'V',
            }),
        }

        _Sea4:AddSection('Farm')
        _Toggle(_Sea4, {
            'Auto Farm Sea',
        }, 'Sea')
        _Sea4:AddSection('Farm Select')

        local _AddDropdown3 = _Sea4.AddDropdown
        local v644 = {}
        local v645 = v641[1]
        local v646 = v641[2]
        local v647 = {
            u38,
            'seaEnemy',
        }

        v644.MultiSelect = true

        __set_list(v644, 1, {
            'Enemies',
            v645,
            v646,
            v647,
            'S-Enemies',
        })
        _AddDropdown3(_Sea4, v644)

        local _AddDropdown4 = _Sea4.AddDropdown
        local v649 = {}
        local v650 = v642[1]
        local v651 = v642[2]
        local v652 = {
            u38,
            'SeaSkills',
        }

        v649.MultiSelect = true

        __set_list(v649, 1, {
            'Select Skills',
            v650,
            v651,
            v652,
            'S-Skills',
        })
        _AddDropdown4(_Sea4, v649)
        _Sea4:AddSection('Configs')
        _Sea4:AddSlider({
            'Boat Tween Speed',
            100,
            300,
            10,
            250,
            {
                u38,
                'BoatSpeed',
            },
            'S-BoatSpeed',
        })
        _Sea4:AddToggle({
            'Auto Repair Boat [ BETA ]',
            false,
            {
                u38,
                'RepairBoat',
            },
            'S-RepairBoat',
        })
    elseif _Sea3 == 3 then
        local v653 = {
            {
                'Z',
                'X',
                'C',
                'V',
                'F',
            },
            ToDictionary({
                'Z',
                'X',
                'C',
                'V',
            }),
        }
        local v654 = {
            {
                'Sea Beast',
                'Terrorshark',
                'Fish Crew Member',
                'Piranha',
                'Shark',
            },
            ToDictionary({
                'Terrorshark',
                'Fish Crew Member',
                'Piranha',
                'Shark',
            }),
        }
        local u655 = nil
        local u656 = {
            ['Shipwright Teacher'] = CFrame.new(-16526, 76, 309),
            ['Shark Hunter'] = CFrame.new(-16526, 108, 752),
            ['Beast Hunter'] = CFrame.new(-16281, 73, 263),
            Spy = CFrame.new(-16471, 528, 539),
        }

        local function v658(p657)
            u32.teleporting = p657

            while u32.teleporting do
                task.wait()

                if u38.selectedNpc then
                    u83(u656[u38.selectedNpc])
                end
            end

            if p657 and u655 then
                u655:Set(false, true)
            end
        end
        local function v662(p659)
            if p659 then
                local _PlayerTeleport = p604.Managers.PlayerTeleport
                local _huge5 = math.huge

                while true do
                    task.wait()

                    if _PlayerTeleport.lastPosition then
                        _huge5 = _LocalPlayer:DistanceFromCharacter(_PlayerTeleport.lastPosition)
                    end
                    if not u32.teleporting or _huge5 < 15 then
                        u32.teleporting = false
                    end
                end
            else
                return
            end
        end

        _Sea4:AddSection('Sea')
        _Toggle(_Sea4, {
            'Auto Farm Sea',
        }, 'Sea')
        _Sea4:AddToggle({
            'Auto Drive Boat',
            true,
            {
                u38,
                'aTweenBoat',
            },
            'A-TweenBoat',
        })
        _Sea4:AddSection('Farm Select')

        local _AddDropdown5 = _Sea4.AddDropdown
        local v664 = {}
        local v665 = v654[1]
        local v666 = v654[2]
        local v667 = {
            u38,
            'fishSelected',
        }

        v664.MultiSelect = true

        __set_list(v664, 1, {
            'Fish',
            v665,
            v666,
            v667,
            'S-Fish',
        })
        _AddDropdown5(_Sea4, v664)

        local _AddDropdown6 = _Sea4.AddDropdown
        local v669 = {}
        local v670 = {
            u38,
            'boatSelected',
        }

        v669.MultiSelect = true

        __set_list(v669, 1, {
            'Boats',
            {
                'PirateBrigade',
                'PirateGrandBrigade',
                'GhostShip',
                'FishBoat',
            },
            nil,
            v670,
            'S-Boat',
        })
        _AddDropdown6(_Sea4, v669)

        local _AddDropdown7 = _Sea4.AddDropdown
        local v672 = {}
        local v673 = v653[1]
        local v674 = v653[2]
        local v675 = {
            u38,
            'SeaSkills',
        }

        v672.MultiSelect = true

        __set_list(v672, 1, {
            'Select Skills',
            v673,
            v674,
            v675,
            'S-Skills',
        })
        _AddDropdown7(_Sea4, v672)
        _Sea4:AddSection('Configs')
        _Sea4:AddDropdown({
            'Sea Level',
            {
                '1',
                '2',
                '3',
                '4',
                '5',
                '6',
                'inf',
            },
            '6',
            {
                u38,
                'SeaLevel',
            },
            'S-SeaLevel',
        })
        _Sea4:AddSlider({
            'Boat Tween Speed',
            100,
            300,
            10,
            250,
            {
                u38,
                'BoatSpeed',
            },
            'S-BoatSpeed',
        })
        _Sea4:AddToggle({
            'Auto Repair Boat [ BETA ]',
            false,
            {
                u38,
                'RepairBoat',
            },
            'S-RepairBoat',
        })
        _Sea4:AddSection('NPCs')
        _Sea4:AddDropdown({
            'Select NPC',
            {
                'Shipwright Teacher',
                'Shark Hunter',
                'Beast Hunter',
                'Spy',
            },
            'Spy',
            {
                u38,
                'selectedNpc',
            },
        })

        u655 = _Sea4:AddToggle({
            'Teleport to NPC',
            false,
            v658,
        })

        local v676 = u655

        u655.Callback(v676, v662)
        _Sea4:AddSection('Quests/Items')
        _Toggle(_Sea4, {
            'Auto Unlock Shipwright Subclass [ BETA ]',
        }, 'Shipwright')
    end

    local _Stats = v607.Stats

    if _Level.Value >= u82.GameData.MaxLevel then
        _Stats:Destroy()
    else
        local u678 = {}
        local _Points = _Data:WaitForChild('Points')
        local _Stats2 = _Data:WaitForChild('Stats')

        local function v687(p681)
            u32.AutoStats = p681

            while task.wait() and u32.AutoStats do
                local _Value = _Points.Value

                if _Value > 0 then
                    local v683, v684, v685 = pairs(u678)

                    while true do
                        local v686

                        v685, v686 = v683(v684, v685)

                        if v685 == nil then
                            break
                        end
                        if v686 and _Stats2[v685].Level.Value < u82.GameData.MaxLevel then
                            _FireRemote4('AddPoint', v685, (math.clamp(math.clamp(u38.StatsPoints or 3, 0, _Value), 0, u82.GameData.MaxLevel)))
                        end
                    end
                end
            end
        end
        local function v689(_, p688)
            _Stats:AddToggle({
                p688,
                false,
                {u678, p688},
                'Stats-' .. p688,
            })
        end

        _Stats:AddSlider({
            'Points Amount',
            1,
            100,
            1,
            3,
            {
                u38,
                'StatsPoints',
            },
            'P-Stats',
        })
        _Stats:AddToggle({
            'Auto Stats',
            false,
            v687,
            'A-Stats',
        })
        _Stats:AddSection('Select Stats')
        table.foreach({
            'Melee',
            'Defense',
            'Gun',
            'Sword',
            'Demon Fruit',
        }, v689)
    end

    local _RaceV4 = v607.RaceV4

    if _Sea3 == 4 then
        _RaceV4:AddSection('Race V4')
        _Toggle(_RaceV4, {
            'Auto Finish Trial',
        }, 'TrialV4')
        _Toggle(_RaceV4, {
            'Auto Kill Players in Trial',
        }, 'KillPlayersV4')
        _Toggle(_RaceV4, {
            'Auto Train Race',
        }, 'TrainV4')
    else
        _RaceV4:Destroy()
    end

    local _Islands = v607.Islands

    if _Sea3 == 3 then
        local function v694(p692)
            u32.LookMoon = p692

            while u32.LookMoon do
                local v693 = _Lighting

                _CurrentCamera.CFrame = CFrame.new(_CurrentCamera.CFrame.Position, v693:GetMoonDirection() + _CurrentCamera.CFrame.Position)

                task.wait()
            end
        end
        local function v696(p695)
            u32.TradeAzure = p695

            while u32.TradeAzure do
                if _Lighting:GetAttribute('IsBlueMoon') and (not _Lighting:GetAttribute('BlueMoonEnded') and _Count4['Azure Ember'] >= u38.Azure) then
                    _Net['RF/KitsuneStatuePray']:InvokeServer()
                end

                task.wait(1)
            end
        end
        local function v702(p697, p698)
            local v699 = _Islands:AddParagraph({
                p697 .. ' : not Spawn',
            })

            while task.wait() do
                local v700 = _Map:FindFirstChild(p698)

                if v700 then
                    local v701 = _LocalPlayer

                    v699:SetTitle(p697 .. ' : Spawned | Distance : ' .. math.floor(v701:DistanceFromCharacter(v700.WorldPivot.Position) / 5))
                else
                    v699:SetTitle(p697 .. ' : not Spawn')
                    _Map.ChildAdded:Wait()
                end
            end
        end

        _Islands:AddSection('Islands Stats')
        task.spawn(v702, 'Mirage Island', 'MysticIsland')
        task.spawn(v702, 'Kitsune Island', 'KitsuneIsland')
        task.spawn(v702, 'Prehistoric Island', 'PrehistoricIsland')
        _Islands:AddSection('Prehistoric Island')
        _Toggle(_Islands, {
            'Auto Craft Volcanic Magnet',
        }, 'CraftVolcanicMagnet')
        _Toggle(_Islands, {
            'Auto Prehistoric Island',
        }, 'PrehistoricIsland')
        _Toggle(_Islands, {
            'Auto Kill Lava Golem',
        }, 'LavaGolem')
        _Toggle(_Islands, {
            'Auto Collect Dinosaur Bones',
        }, 'PrehistoricBones')
        _Toggle(_Islands, {
            'Auto Collect Dragon Egg',
        }, 'PrehistoricEgg')
        _Islands:AddToggle({
            'Reset after finishing',
            false,
            {
                u38,
                'ResetPrehistoric',
            },
            'P-Reset',
        })
        _Islands:AddSection('Leviathan [ BETA ]')
        _Toggle(_Islands, {
            'Auto Attack Leviathan',
        }, 'Leviathan')
        _Islands:AddSection('Kitsune Island')
        _Islands:AddSlider({
            'Trade Azure Ember Amount',
            10,
            25,
            5,
            20,
            {
                u38,
                'Azure',
            },
            'A-Amount',
        })
        _Islands:AddToggle({
            'Auto Trade Azure Ember',
            false,
            v696,
        }, 'Trade-Azure')
        _Toggle(_Islands, {
            'Auto Kitsune Island',
        }, 'KitsuneIsland')
        _Islands:AddSection('Mirage Island')
        _Toggle(_Islands, {
            'Teleport To Gear',
        }, 'MirageGear')
        _Toggle(_Islands, {
            'Teleport To Mirage',
        }, 'TeleportMirage')
        _Toggle(_Islands, {
            'Teleport To Fruit Dealer',
        }, 'MirageFruitDealer')
        _Toggle(_Islands, {
            'Collect Mirage Chests',
        }, 'MirageChests')
        _Islands:AddToggle({
            'Look To Moon',
            false,
            v694,
            'MirageLookMoon',
        })
    else
        _Islands:Destroy()
    end

    local _FruitRaid = v607.FruitRaid
    local u704 = {
        'Rocket',
        'Spin',
        'Blade',
        'Spring',
        'Bomb',
        'Smoke',
        'Spike',
    }
    local v705 = 'Only on Sea 2 and 3'
    local u706 = true
    local u707 = nil

    local function v711(p708)
        u32.auto_store = p708

        while u32.auto_store do
            task.wait(u38.SmoothMode and 0.3 or 0.2)

            u706 = false

            local v709 = not _LocalPlayer:GetAttribute('IslandRaiding') and u32.unstore_common_fruits

            if v709 then
                v709 = u707
            end

            local v710 = _FruitManager:GetStorableFruit(v709)

            if v710 then
                _FruitManager:StoreFruit(v710)

                u707 = nil
            else
                u706 = true
            end
        end

        u706 = true
    end
    local function v713(p712)
        u32.random_fruit = p712

        while u32.random_fruit do
            _FruitManager:RerollRandomFruit()
            task.wait(0.1)
        end
    end
    local function v715(p714)
        u32.raid_microchip = p714

        while u32.raid_microchip do
            if u706 then
                if _FruitManager:CanBuyMicrochip() then
                    _FireRemote4('RaidsNpc', 'Select', u38.SelectedChip)
                else
                    task.wait(0.1)
                end
            else
                task.wait()
            end
        end
    end
    local function v720(p716)
        u32.unstore_common_fruits = p716

        while u32.unstore_common_fruits do
            if _FruitManager:CanBuyMicrochip() == -1 and u706 then
                for v717 = 1, #u704 do
                    local v718 = u704[v717]
                    local v719 = v718 .. '-' .. v718

                    if _LocalPlayer.Character:FindFirstChild(v719) or _LocalPlayer.Backpack:FindFirstChild(v719) then
                        break
                    end
                end
            end

            task.wait(0.25)
        end
    end

    _FruitRaid:AddSection('Fruits')
    _FruitRaid:AddToggle({
        'Auto Store Fruits',
        false,
        v711,
        'F-AutoStore',
    })
    _Toggle(_FruitRaid, {
        'Teleport To Fruits',
    }, 'Fruits')
    _FruitRaid:AddToggle({
        'Auto Random Fruit',
        false,
        v713,
        'F-RandomFruit',
    })
    _FruitRaid:AddSection('Raid')

    if _Sea3 == 2 or _Sea3 == 3 then
        local _AddDropdown8 = _FruitRaid.AddDropdown
        local v722 = {}
        local v723 = {
            u38,
            'SelectedChip',
        }

        __set_list(v722, 1, {
            'Select Chip',
            u82.RaidList,
            '',
            v723,
            'R-RaidChip',
        })
        _AddDropdown8(_FruitRaid, v722)
        _Toggle(_FruitRaid, {
            'Auto Farm Raid',
            'Kill Aura, Start & Awaken',
        }, 'Raid')
        _FruitRaid:AddToggle({
            'Auto Buy Chip',
            false,
            v715,
            'R-BuyChip',
        })
        _FruitRaid:AddToggle({
            'Unstore Common Fruits',
            false,
            v720,
            'R-Unstore',
        })
    else
        _FruitRaid:AddParagraph({v705})
    end

    local _Teleport = v607.Teleport
    local u725 = nil
    local u726 = CFrame.new(28286, 14897, 103)
    local v727 = ({
        {
            'WindMill',
            'Marine',
            'Middle Town',
            'Jungle',
            'Pirate Village',
            'Desert',
            'Snow Island',
            'MarineFord',
            'Colosseum',
            'Sky Island 1',
            'Sky Island 2',
            'Sky Island 3',
            'Prison',
            'Magma Village',
            'Under Water Island',
            'Fountain City',
        },
        {
            'The Cafe',
            'Frist Spot',
            'Dark Area',
            'Flamingo Mansion',
            'Flamingo Room',
            'Green Zone',
            'Zombie Island',
            'Two Snow Mountain',
            'Punk Hazard',
            'Cursed Ship',
            'Ice Castle',
            'Forgotten Island',
            'Ussop Island',
        },
        {
            'Mansion',
            'Port Town',
            'Great Tree',
            'Castle On The Sea',
            'Hydra Island',
            'Floating Turtle',
            'Haunted Castle',
            'Ice Cream Island',
            'Peanut Island',
            'Cake Island',
            'Candy Cane Island',
            'Tiki Outpost',
        },
    })[_Sea3]
    local u728 = {
        ['Middle Town'] = CFrame.new(-688, 15, 1585),
        MarineFord = CFrame.new(-4810, 21, 4359),
        Marine = CFrame.new(-2728, 25, 2056),
        WindMill = CFrame.new(889, 17, 1434),
        Desert = CFrame.new(1054, 53, 4490),
        ['Snow Island'] = CFrame.new(1298, 87, -1344),
        ['Pirate Village'] = CFrame.new(-1173, 45, 3837),
        Jungle = CFrame.new(-1614, 37, 146),
        Prison = CFrame.new(4870, 6, 736),
        ['Under Water Island'] = CFrame.new(61164, 5, 1820),
        Colosseum = CFrame.new(-1535, 7, -3014),
        ['Magma Village'] = CFrame.new(-5290, 9, 8349),
        ['Sky Island 1'] = CFrame.new(-4814, 718, -2551),
        ['Sky Island 2'] = CFrame.new(-4652, 873, -1754),
        ['Sky Island 3'] = CFrame.new(-7895, 5547, -380),
        ['Fountain City'] = CFrame.new(5041, 1, 4101),
        ['The Cafe'] = CFrame.new(-382, 73, 290),
        ['Frist Spot'] = CFrame.new(-11, 29, 2771),
        ['Dark Area'] = CFrame.new(3494, 13, -3259),
        ['Flamingo Mansion'] = CFrame.new(-317, 331, 597),
        ['Flamingo Room'] = CFrame.new(2285, 15, 905),
        ['Green Zone'] = CFrame.new(-2258, 73, -2696),
        ['Zombie Island'] = CFrame.new(-5552, 194, -776),
        ['Two Snow Mountain'] = CFrame.new(752, 408, -5277),
        ['Punk Hazard'] = CFrame.new(-5897, 18, -5096),
        ['Cursed Ship'] = CFrame.new(919, 125, 32869),
        ['Ice Castle'] = CFrame.new(5505, 40, -6178),
        ['Forgotten Island'] = CFrame.new(-3050, 240, -10178),
        ['Ussop Island'] = CFrame.new(4816, 8, 2863),
        Mansion = CFrame.new(-12471, 374, -7551),
        ['Port Town'] = CFrame.new(-334, 7, 5300),
        ['Castle On The Sea'] = CFrame.new(-5073, 315, -3153),
        ['Hydra Island'] = CFrame.new(5666, 1013, -310),
        ['Great Tree'] = CFrame.new(2683, 275, -7008),
        ['Floating Turtle'] = CFrame.new(-12528, 332, -8658),
        ['Haunted Castle'] = CFrame.new(-9517, 142, 5528),
        ['Ice Cream Island'] = CFrame.new(-902, 79, -10988),
        ['Peanut Island'] = CFrame.new(-2062, 50, -10232),
        ['Cake Island'] = CFrame.new(-1897, 14, -11576),
        ['Candy Cane Island'] = CFrame.new(-1038, 10, -14076),
        ['Tiki Outpost'] = CFrame.new(-16224, 9, 439),
    }

    local function v729()
        for _ = 1, 10 do
            task.wait()
            _LocalPlayer.Character:SetPrimaryPartCFrame(u726)
        end
    end
    local function v731(p730)
        u32.teleporting = p730

        while u32.teleporting do
            task.wait()

            if u728[u32.SelectedIsland] then
                u83(u728[u32.SelectedIsland])
            end
        end

        if p730 and u725 then
            u725:Set(false, true)
        end
    end
    local function v735(p732)
        if p732 then
            local _PlayerTeleport2 = p604.Managers.PlayerTeleport
            local _huge6 = math.huge

            while true do
                task.wait()

                if _PlayerTeleport2.lastPosition then
                    _huge6 = _LocalPlayer:DistanceFromCharacter(_PlayerTeleport2.lastPosition)
                end
                if not u32.teleporting or _huge6 < 15 then
                    u32.teleporting = false
                end
            end
        else
            return
        end
    end

    _Teleport:AddSection('Travel')

    local _AddButton = _Teleport.AddButton
    local v737 = {}

    local function v738()
        u82:TravelTo(1)
    end

    v737.Desc = 'Main'

    __set_list(v737, 1, {
        'Teleport to Sea 1',
        v738,
    })
    _AddButton(_Teleport, v737)

    local _AddButton2 = _Teleport.AddButton
    local v740 = {}

    local function v741()
        u82:TravelTo(2)
    end

    v740.Desc = 'Dressrosa'

    __set_list(v740, 1, {
        'Teleport to Sea 2',
        v741,
    })
    _AddButton2(_Teleport, v740)

    local _AddButton3 = _Teleport.AddButton
    local v743 = {}

    local function v744()
        u82:TravelTo(3)
    end

    v743.Desc = 'Zou'

    __set_list(v743, 1, {
        'Teleport to Sea 3',
        v744,
    })
    _AddButton3(_Teleport, v743)
    _Teleport:AddSection('Islands')
    _Teleport:AddDropdown({
        'Select Island',
        v727,
        '',
        {
            u32,
            'SelectedIsland',
        },
    })

    u725 = _Teleport:AddToggle({
        'Teleport to Island',
        false,
        v731,
    })

    local v745 = u725

    u725.Callback(v745, v735)

    if _Sea3 == 3 then
        _Teleport:AddSection('Race V4')
        _Teleport:AddButton({
            'Teleport to Temple of Time',
            v729,
        })
    end

    local _Status = v607.Status
    local u747 = _Sea3
    local _ = _FarmManager.Enemies.Elites
    local _IsSpawned2 = u82.Enemies.IsSpawned
    local u749 = nil
    local u750 = '\u{fffd}\u{fffd}\u{fffd}\u{fffd}\u{fffd}'
    local u751 = '\u{fffd}\u{fffd}\u{fffd}\u{fffd}\u{fffd}'
    local u752 = {}
    local u753 = 0

    local function v759(p754, p755)
        if p755 or p755 == nil then
            local _insert = table.insert
            local v757 = u752
            local v758 = {
                Paragraph = _Status:AddParagraph({
                    '',
                }),
                Function = p754,
            }

            _insert(v757, v758)
        end
    end

    v759(function()
        local _EliteProgress = u82:GetProgress('EliteProgress', 'EliteHunter', 'Progress')
        local _Elite = u82.Enemies:GetEnemyByTag('Elite')

        if _Elite then
            return ('Elite Progress: %i\nElite Hunter: %s %s'):format(_EliteProgress, _Elite.Name, u750)
        else
            return ('Elite Progress: %i\nElite Hunter: %s'):format(_EliteProgress, (u749 and 0 <= 600 - (tick() - u749) and (u101.GetTimer(600 - (tick() - u749) or '00:00') or '') or '') .. u751)
        end
    end, u747 == 3)
    v759(function()
        local v762 = _IsSpawned2('Cake Prince') and 'Cake Prince'

        if not v762 then
            local _DoughKing = _IsSpawned2('Dough King')

            v762 = _DoughKing and 'Dough King' or _DoughKing
        end
        if v762 then
            return ('Katakuri: %s %s'):format(v762, u750)
        end

        local v764 = u82
        local v765 = string.gsub(v764:GetProgress('Katakuri', 'CakePrinceSpawner', true), '%D', '')

        return 'Katakuri: ' .. (v765:len() == 0 and ('0' or v765) or v765)
    end, u747 == 3)
    v759(function()
        local _SwordDealer = u82:GetProgress('Sword Dealer', 'LegendarySwordDealer', '1')

        if type(_SwordDealer) ~= 'string' then
            return ('Sword Dealer: %s'):format(u751)
        else
            return ('Sword Dealer: %s %s'):format(_SwordDealer, u750)
        end
    end, u747 == 2)
    v759(function()
        local _BaristaCousin, v768 = u82:GetProgress('BaristaCousin', 'ColorsDealer', '1')

        if type(_BaristaCousin) ~= 'string' then
            return 'Barista Cousin: ' .. u751
        else
            return ('Barista Cousin: %s [ %s ] %s'):format(_BaristaCousin, 3 <= v768 and 'LEGENDARY' or 'Rare', u750)
        end
    end)
    v759(function()
        if workspace:FindFirstChild('Fruit ') then
            return ('Devil Fruit: %s %s'):format(u82.FruitsName[workspace['Fruit '] ], u750)
        else
            return 'Devil Fruit: ' .. u751
        end
    end)
    v759(function()
        local v769 = {}

        for v770 = 1, #_BerryBush do
            if v770 % 10 == 0 then
                task.wait(0.1)
            end

            local v771 = _BerryBush[v770]
            local v772, v773, v774 = pairs(v771:GetAttributes())

            while true do
                local v775

                v774, v775 = v772(v773, v774)

                if v774 == nil then
                    break
                end

                table.insert(v769, v775)
            end
        end

        if #v769 <= 0 then
            return 'Berries: ' .. u751
        else
            return ('Berries: #%i [ %s ] %s'):format(#v769, table.concat(v769, ', '), u750)
        end
    end)
    v759(function()
        return 'Players: ' .. #_Players:GetPlayers() .. '/12'
    end)
    v759(function()
        return ('Enabled Options: %i/%i\nFarm Status: %s [ %s ]'):format(#u37, #u36, u38.RunningOption or 'Null', u38.RunningMethod or 'Null')
    end)
    v759(function()
        return 'Is Private Server: ' .. (_ReplicatedStorage.PrivateServerOwnerId.Value ~= 0 and u750 or u751)
    end)

    local u776 = 1
    local u777 = nil

    u777 = _Stepped:Connect(function()
        if not (_Status and _Status.Cont) then
            return u777:Disconnect()
        end
        if u747 == 3 and u776 == 1 and tick() - u753 >= 1 then
            if not _Status.Cont.Parent then
                u753 = tick()
            end
            if u82.Enemies:GetEnemyByTag('Elite') then
                u749 = tick()
            end
        end
        if tick() - u753 >= 1 and _Status.Cont.Parent then
            local v778 = u752[u776]

            u776 = (u776 >= #u752 and 0 or u776) + 1

            if u776 >= #u752 then
                u753 = tick()
            end
            if v778 and not v778.Updating then
                v778.Updating = true

                v778.Paragraph:SetTitle(v778.Function())

                v778.Updating = false
            end
        end
    end)

    local _Visual = v607.Visual
    local _EspManager = p604.Managers.EspManager
    local u781 = u1.EspColors or {
        Players = Color3.fromRGB(220, 220, 220),
        Fruits = Color3.fromRGB(255, 0, 0),
        Islands = Color3.fromRGB(0, 255, 255),
        Berries = Color3.fromRGB(255, 255, 0),
        Chests = {
            Chest1 = Color3.fromRGB(150, 150, 150),
            Chest2 = Color3.fromRGB(255, 255, 0),
            Chest3 = Color3.fromRGB(0, 255, 255),
            Null = Color3.fromRGB(150, 0, 255),
        },
    }
    local v799 = {
        Players = _EspManager.new('Player', _Characters, function(p782)
            if p782 ~= _LocalPlayer.Character then
                return true, u781.Players
            end
        end),
        Islands = _EspManager.new('Island', _Locations, function(p783)
            if p783.Name ~= 'Sea' then
                return true, u781.Islands
            end
        end),
        Fruits = _EspManager.new('Fruit', workspace, function(p784)
            if p784:IsA('Model') and p784:GetPivot().Position == Vector3.zero then
                return nil
            end
            if string.sub(p784.Name, -6, -1) == ' Fruit' or p784.Name == 'Fruit ' then
                return true, u781.Fruits, p784:FindFirstChild('Handle') or p784
            end
        end),
        Flowers = _EspManager.new('Flower', workspace, function(p785)
            if p785:IsA('BasePart') and p785.Name:find('Flower') then
                return true, p785.Color
            end
        end),
        Chests = _EspManager.new('Chests', __ChestTagged, function(p786)
            return not p786:GetAttribute('IsDisabled'), u781.Chests[p786.Name]
        end, function(p787)
            return not p787:GetAttribute('IsDisabled')
        end),
        Berries = _EspManager.new('Berries', _BerryBush, function(p788)
            local v789, v790, v791 = pairs(p788:GetAttributes())
            local v792, v793 = v789(v790, v791)

            if v792 ~= nil then
                return true, u781.Berries, v793, p788.Parent
            end
        end, function(p794)
            if p794:FindFirstChild('Berries') then
                local v795, v796, v797 = pairs(p794.Berries:GetAttributes())
                local v798, _ = v795(v796, v797)

                if v798 ~= nil then
                    return true
                end
            end
        end),
    }

    if not u82:IsBlacklistedExecutor() then
        _Visual:AddSection('Aimbot Nearest')
        _Visual:AddToggle({
            'Aimbot Gun',
            false,
            {
                u32,
                'AimBot_Gun',
            },
        })
        _Visual:AddToggle({
            'Aimbot Tap',
            false,
            {
                u32,
                'AimBot_Tap',
            },
        })
        _Visual:AddToggle({
            'Aimbot Skills',
            false,
            {
                u32,
                'AimBot_Skills',
            },
        })
        _Visual:AddToggle({
            'Ignore Mobs',
            true,
            {
                u38,
                'NoAimMobs',
            },
        })
    end

    _Visual:AddSection('ESP')

    if _Sea3 == 2 then
        _Visual:AddToggle({
            'ESP Flowers',
            false,
            {
                v799.Flowers,
                'Enabled',
            },
            'Esp-Flower',
        })
    end

    _Visual:AddToggle({
        'ESP Players',
        false,
        {
            v799.Players,
            'Enabled',
        },
        'Esp-Players',
    })
    _Visual:AddToggle({
        'ESP Fruits',
        false,
        {
            v799.Fruits,
            'Enabled',
        },
        'Esp-Fruits',
    })
    _Visual:AddToggle({
        'ESP Berries',
        false,
        {
            v799.Berries,
            'Enabled',
        },
        'Esp-Berry',
    })
    _Visual:AddToggle({
        'ESP Chests',
        false,
        {
            v799.Chests,
            'Enabled',
        },
        'Esp-Chests',
    })
    _Visual:AddToggle({
        'ESP Islands',
        false,
        {
            v799.Islands,
            'Enabled',
        },
        'Esp-Island',
    })
    _Visual:AddSection('Visual')
    _Visual:AddButton({
        'Meteor Rain',
        function()
            require(game:GetService('ReplicatedStorage').Effect.Container.UzothSpec)({
                Position = _LocalPlayer.Character.PrimaryPart.Position,
            })
        end,
    })
    _Visual:AddButton({
        'Remove Portal Dash Cooldown',
        function()
            local v800 = _LocalPlayer.Backpack:FindFirstChild('Portal-Portal') or _LocalPlayer.Character:FindFirstChild('Portal-Portal')

            if v800 then
                local v801 = next
                local v802, v803 = getconnections(v800.Activated)

                while true do
                    local v804

                    v803, v804 = v801(v802, v803)

                    if v803 == nil then
                        break
                    end
                    if #debug.getupvalues(v804.Function) == 9 then
                        while task.wait() and v800 and v800:IsDescendantOf(game) do
                            debug.setupvalue(v804.Function, 2, 0)
                        end
                    end
                end
            end
        end,
    })

    local _Shop = v607.Shop
    local v806, v807, v808 = ipairs(u82.Shop)
    local u809 = _FireRemote4

    while true do
        local v810

        v808, v810 = v806(v807, v808)

        if v808 == nil then
            break
        end

        _Shop:AddSection(v810[1])

        local v811, v812, v813 = ipairs(v810[2])

        while true do
            local u814

            v813, u814 = v811(v812, v813)

            if v813 == nil then
                break
            end

            local v815 = u814[2]
            local v816 = type(u814[2]) == 'table' and function()
                u809(unpack(u814[2]))
            end or v815

            _Shop:AddButton({
                u814[1],
                v816,
            })
        end
    end

    local _Misc = v607.Misc
    local u818 = nil

    local function v819()
        loadstring((getclipboard or fromclipboard)())()
    end
    local function u822(p820)
        local v821 = p820:gsub('\n', ''):gsub('```', ''):gsub('`', '')

        if v821:find('-') then
            return v821
        else
            return v821:gsub('v', '-'):gsub('q', '00'):gsub('x', '22'):gsub('f', '11'):gsub('d', '44'):gsub('a', '55'):gsub('h', '66'):gsub('s', '77'):gsub('j', '88'):gsub('g', '99'):gsub('i', '33'):gsub('y', '1'):gsub('p', '2'):gsub('u', '3'):gsub('z', '4'):gsub('o', '5'):gsub('l', '6'):gsub('r', '7'):gsub('k', '8'):gsub('t', '9'):gsub('e', '0'):lower()
        end
    end
    local function v824(p823)
        return u822(p823)
    end
    local function u826(p825)
        _ReplicatedStorage.__ServerBrowser:InvokeServer('teleport', p825)
    end
    local function v827()
        u826((getclipboard or fromclipboard)())
    end

    local u828 = nil
    local u829 = nil

    local function v833(p830)
        if p830 then
            u82.Hooking:EnableBypass()
        end

        local v831 = u32
        local v832 = p830 and u829 or false

        u828 = p830
        v831.WalkSpeedBypass = v832
    end
    local function v837(p834)
        local v835 = u32
        local v836 = u828 and p834 and p834 or false

        u829 = p834
        v835.WalkSpeedBypass = v836
    end
    local function v842(p838)
        u32.WalkOnWater = p838

        local _WaterBasePlane = _Map:WaitForChild('WaterBase-Plane', 9000000000)
        local v840 = u818 or _WaterBasePlane.Size
        local v841 = Vector3.new(v840.X, 113, v840.Z)

        u818 = v840

        while task.wait(0.25) and u32.WalkOnWater do
            if u82.IsAlive(_LocalPlayer.Character) and _LocalPlayer.Character.Humanoid.Sit then
                _WaterBasePlane.Size = v840
            else
                _WaterBasePlane.Size = v841
            end
        end

        _WaterBasePlane.Size = v840
    end
    local function v844(p843)
        u32.AntiAFK = p843

        while u32.AntiAFK do
            _VirtualUser:CaptureController()
            _VirtualUser:ClickButton1(Vector2.new(math.huge, math.huge))
            task.wait(600)
        end
    end
    local function v846(p845)
        u32.ActiveRaceV3 = p845

        while u32.ActiveRaceV3 do
            if _Data.Race:FindFirstChild('Evolved') then
                _Remotes.CommE:FireServer('ActivateAbility')
            else
                _Data.Race.ChildAdded:Wait()
            end

            task.wait(u38.SmoothMode and 2.5 or 1)
        end
    end
    local function v852(p847)
        u32.ActiveRaceV4 = p847

        local _Character3 = _LocalPlayer.Character

        while u32.ActiveRaceV4 do
            _Character3 = _Character3 or _LocalPlayer.CharacterAdded:Wait()

            local _RaceTransformed = _Character3:FindFirstChild('RaceTransformed')
            local _RaceEnergy = _Character3:FindFirstChild('RaceEnergy')

            if _RaceEnergy and 1 <= _RaceEnergy.Value and (_RaceTransformed and not _RaceTransformed.Value) then
                local v851 = _LocalPlayer.Backpack:FindFirstChild('Awakening') or _Character3:FindFirstChild('Awakening')

                if v851:FindFirstChild('RemoteFunction') then
                    v851.RemoteFunction:InvokeServer(true)
                end
            end

            task.wait(u38.SmoothMode and 1 or 0.5)
        end
    end

    if IsOwner then
        _Misc:AddSection('Executor')
        _Misc:AddButton({
            'Execute Clipboard',
            v819,
        })
    end
    if u82.JobIds then
        _Misc:AddSection('Join Server')

        _Misc:AddTextBox({
            'Input Job Id',
            '1',
            true,
            u826,
            'JobId',
        }).OnChanging = v824

        _Misc:AddButton({
            'Join Clipboard',
            v827,
        })
    end

    _Misc:AddSection('Settings')
    _Misc:AddDropdown({
        'Farm Mode',
        {
            'Up',
            'Orbit',
            'Star',
        },
        'Up',
        {
            u38,
            'FarmMode',
        },
        'S-FarmMode',
    })
    _Misc:AddSlider({
        'Farm Distance',
        5,
        30,
        1,
        15,
        function(p853)
            u38.FarmPos = Vector3.new(0, p853, 0)
            u38.FarmDistance = p853
        end,
        'S-Distance',
    })
    _Misc:AddSlider({
        'Tween Speed',
        50,
        300,
        5,
        200,
        {
            u38,
            'TweenSpeed',
        },
        'S-TweenSpeed',
    })
    _Misc:AddSlider({
        'Bring Mobs Distance',
        50,
        400,
        10,
        250,
        {
            u38,
            'BringDistance',
        },
        'S-BringDistance',
    })
    _Misc:AddToggle({
        'Bring Mobs',
        true,
        {
            u38,
            'BringMobs',
        },
        'S-BringMobs',
    })
    _Misc:AddToggle({
        'Auto Haki',
        true,
        {
            u38,
            'AutoBuso',
        },
        'S-AutoBuso',
    })
    _Misc:AddToggle({
        'Auto Attack',
        true,
        {
            u38,
            'AutoClick',
        },
        'S-AutoClick',
    })
    _Misc:AddToggle({
        'Auto Shoot',
        false,
        {
            u38,
            'AutoShoot',
        },
        'S-AutoShoot',
    })

    local _AddToggle = _Misc.AddToggle
    local v855 = {}
    local v856 = {
        p604.Managers.QuestManager,
        'takeQuestDebounce',
    }

    v855.Desc = 'Wait 75 seconds to take the next mission'

    __set_list(v855, 1, {
        'Take Quest Debounce',
        false,
        v856,
        'S-QuestDenounce',
    })
    _AddToggle(_Misc, v855)
    _Misc:AddSection('Codes')
    _Misc:AddButton({
        'Redeem all Codes',
        u101.AllCodes,
    })
    _Misc:AddSection('Server')
    _Misc:AddButton({
        'Server Hop',
        function()
            u82:ServerHop()
        end,
    })
    _Misc:AddButton({
        'Rejoin',
        function()
            u82.Rejoin()
        end,
    })
    _Misc:AddSection('Team')
    _Misc:AddButton({
        'Join Pirates Team',
        u84.Pirates,
    })
    _Misc:AddButton({
        'Join Marines Team',
        u84.Marines,
    })
    _Misc:AddSection('Race')
    _Misc:AddToggle({
        'Auto Active Race V3',
        false,
        v846,
        'S-RaceV3',
    })
    _Misc:AddToggle({
        'Auto Active Race V4',
        false,
        v852,
        'S-RaceV4',
    })
    _Misc:AddSection('Menu')
    _Misc:AddButton({
        'Devil Fruit Shop',
        function()
            require(_LocalPlayer.PlayerGui.Main.UIController.FruitShop):Open('FruitDealer')
        end,
    })
    _Misc:AddButton({
        'Advanced Fruit Dealer',
        function()
            require(_LocalPlayer.PlayerGui.Main.UIController.FruitShop):Open('AdvancedFruitDealer')
        end,
    })
    _Misc:AddButton({
        'Titles',
        function()
            u809('getTitles')

            _LocalPlayer.PlayerGui.Main.Titles.Visible = true
        end,
    })
    _Misc:AddButton({
        'Haki Color',
        function() end,
    })

    if not u82:IsBlacklistedExecutor() then
        _Misc:AddSection('Local-Player')
        _Misc:AddToggle({
            'Enable Speed Hack',
            false,
            v833,
            'M-WalkSpeed:A',
        })
        _Misc:AddSlider({
            'Walk Speed',
            10,
            300,
            5,
            150,
            v837,
            'M-WalkSpeed:B',
        })
    end

    _Misc:AddSection('Visual')
    _Misc:AddButton({
        'Remove Fog',
        u101.RemoveFog,
    })
    _Misc:AddSection('More FPS')

    local _AddToggle2 = _Misc.AddToggle
    local v858 = {}
    local v859 = {
        u38,
        'SmoothMode',
    }

    v858.Desc = 'Reduces calculation speed to improve FPS'

    __set_list(v858, 1, {
        'Smooth Farm Mode',
        false,
        v859,
        'SmoothFarm',
    })
    _AddToggle2(_Misc, v858)
    _Misc:AddToggle({
        'Remove Damage',
        false,
        function(p860)
            _ReplicatedStorage.Assets.GUI.DamageCounter.Enabled = not p860
        end,
        'M-DamageCounter',
    })
    _Misc:AddToggle({
        'Remove Notifications',
        false,
        function(p861)
            _LocalPlayer.PlayerGui.Notifications.Enabled = not p861
        end,
        'M-Notifications',
    })
    _Misc:AddSection('Others')
    _Misc:AddToggle({
        'Walk On Water',
        true,
        v842,
        'M-WalkOnWater',
    })
    _Misc:AddToggle({
        'Anti AFK',
        true,
        v844,
        'M-AntiAFK',
    })

    local _Items = v607.Items

    if _Sea3 ~= 3 then
        if _Sea3 ~= 2 then
            if _Sea3 == 1 then
                _Items:AddSection('Second Sea')
                _Toggle(_Items, {
                    'Auto Second Sea',
                    'Automatically unlocks access to the Second Sea',
                }, 'SecondSea')
                _Items:AddSection('Swords')
                _Toggle(_Items, {
                    'Auto Unlock Saber',
                    'Automatically unlocks the Saber Sword',
                }, 'Saber')
                _Toggle(_Items, {
                    'Auto Pole V1',
                    'Kill Thunder God',
                }, 'PoleV1')
                _Toggle(_Items, {
                    'Auto Saw Sword',
                    'Kill The Saw',
                }, 'TheSaw')
            end
        else
            local function v865(p863)
                u32.LegendSword = p863

                while task.wait() and u32.LegendSword do
                    local _LegendarySwordDealer = u809('LegendarySwordDealer', '1')

                    if type(_LegendarySwordDealer) ~= 'string' then
                        task.wait(5)
                    elseif _Unlocked3[_LegendarySwordDealer] then
                        task.wait(13500)
                    elseif _Beli.Value < 2000000 then
                        _Beli:GetPropertyChangedSignal('Value'):Wait()
                    else
                        u809('LegendarySwordDealer', '2')
                    end
                end
            end

            _Items:AddSection('Third Sea')
            _Toggle(_Items, {
                'Auto Third Sea',
                'Automatically unlocks access to the Third Sea',
            }, 'ThirdSea')
            _Toggle(_Items, {
                'Auto Kill Don Swan',
                'Automatically defeats Don Swan',
            }, 'DonSwan')
            _Items:AddSection('Bosses')
            _Toggle(_Items, {
                'Auto Darkbeard',
                'Automatically spawns and defeats Darkbeard',
            }, 'Darkbeard')
            _Toggle(_Items, {
                'Auto Cursed Captain',
                'Automatically summons and defeats the Cursed Captain',
            }, 'CursedCaptain')
            _Items:AddSection('Law')
            _Toggle(_Items, {
                'Auto Kill Law',
                'Automatically spawns and defeats Law (Order)',
            }, 'Order')

            local _AddToggle3 = _Items.AddToggle
            local v867 = {}
            local v868 = {
                u38,
                'FullyLawRaid',
            }

            v867.Desc = 'Buy the raid law Microchip'

            __set_list(v867, 1, {
                'Auto Buy Microchip',
                false,
                v868,
                'S-FullyLaw',
            })
            _AddToggle3(_Items, v867)
            _Items:AddSection('Sword')
            _Items:AddToggle({
                Desc = 'Automatically purchases Legendary Swords when available',
                'Auto Buy Legendary Sword',
                false,
                v865,
                'LegendSword',
            })
            _Toggle(_Items, {
                'Auto Rengoku',
                'Automatically kill Ice Admiral to unlock the Rengoku sword',
            }, 'Rengoku')
            _Items:AddSection('Race')
            _Toggle(_Items, {
                'Auto Race V2',
                'Automatically evolves the Race to V2',
            }, 'RaceV2')
            _Toggle(_Items, {
                'Auto Race V3',
                'Mink, Human & Shark',
            }, 'RaceV3')
            _Items:AddSection('Bartilo')
            _Toggle(_Items, {
                'Auto Bartilo Quest',
                'Req: Level 850',
            }, 'Bartilo')
        end
    else
        _Items:AddSection('Dragon Dojo')
        _Toggle(_Items, {
            'Auto Dojo Trainer Quest',
            'Automatically completes Dojo Trainer quests',
        }, 'DojoTrainer')
        _Toggle(_Items, {
            'Auto Dragon Hunter Quest',
            'Automatically completes Dragon Hunter quests',
        }, 'DragonHunter')
        _Toggle(_Items, {
            'Auto Draco V2 & V3',
            'Evolves the Draco Race to V2 and V3',
        }, 'DracoV2V3')
        _Items:AddSection('Farm')
        _Toggle(_Items, {
            'Auto Elite Hunter',
            'Automatically completes Elite Hunter quests',
        }, 'EliteHunter')
        _Toggle(_Items, {
            'Auto Rip Indra',
            'Activates the plates and summons Rip Indra',
        }, 'RipIndra')
        _Toggle(_Items, {
            'Auto Cake Prince',
            'Automatically summons the Cake Prince',
        }, 'CakePrince')
        _Toggle(_Items, {
            'Auto Dough King',
            'Automatically summons the Dough King',
        }, 'DoughKing')
        _Items:AddSection('Sword')
        _Toggle(_Items, {
            'Auto Collect Yama',
            'Automatically collects the Yama sword after defeating 30 Elite Hunters',
        }, 'Yama')
        _Toggle(_Items, {
            'Auto Tushita',
            'Solves the Tushita puzzle and defeats Longma',
        }, 'Tushita')
        _Toggle(_Items, {
            'Auto Cursed Dual Katana',
            'Complete the Cursed Dual Katana puzzle',
        }, 'CursedDualKatana')
        _Items:AddSection('Quest')
        _Toggle(_Items, {
            'Auto Citizen Quest',
        }, 'Citizen')
        _Toggle(_Items, {
            'Auto Rainbow Haki',
        }, 'RainbowHaki')
    end

    _Items:AddSection('Berries')
    _Toggle(_Items, {
        'Auto Collect Berries',
    }, 'BerryBush')
    _Items:AddToggle({
        'Auto Berry Hop',
        false,
        {
            u38,
            'BerryHop',
        },
        'S-BerryHop',
    })

    if _Sea3 ~= 1 and _QuestManager.GetColorsList then
        local function v872(p869)
            u32.barista_cousin = p869

            while u32.barista_cousin do
                local _BaristaCousin2, _ = u809('BaristaCousin', 'ColorsDealer', '1')

                if type(_BaristaCousin2) ~= 'string' then
                    task.wait(5)
                else
                    local _ColorsDealer = u809('ColorsDealer', '2')

                    if _ColorsDealer == 1 or _ColorsDealer == 2 then
                        task.wait(250)
                    elseif _ColorsDealer == 0 then
                        _Beli:GetPropertyChangedSignal('Value'):Wait()
                    end
                end
            end
        end

        _Items:AddSection('Aura Color')

        local _AddDropdown9 = _Items.AddDropdown
        local v874 = {}
        local v875 = {
            u38,
            'CraftAura',
        }

        __set_list(v874, 1, {
            'Select Aura',
            _QuestManager:GetColorsList(),
            false,
            v875,
            'S-Aura',
        })
        _AddDropdown9(_Items, v874)
        _Toggle(_Items, {
            'Auto Craft Aura Color',
        }, 'AuraColor')
        _Items:AddToggle({
            'Auto Craft Hop',
            false,
            {
                u38,
                'CraftHop',
            },
            'S-CraftHop',
        })
        _Items:AddToggle({
            'Auto Barista Cousin',
            false,
            v872,
            'B-Cousin',
        })
    end
end
function u102.StartFarm(_)
    if not u32.loadedFarm then
        u32.loadedFarm = true

        task.spawn(u82.RunFunctions.FarmQueue, u37)
    end
end
function u102.StartFunctions(p876)
    table.clear(u36)

    local u877 = {}

    local function v885(p878, p879, p880)
        if p880 == false then
            return
        end
        if not u877[p878] then
            u877[p878] = p879

            table.insert(u36, {
                Name = p878,
                Function = p879,
            })

            return nil
        end

        u877[p878] = p879

        local v881, v882, v883 = ipairs(u36)

        while true do
            local v884

            v883, v884 = v881(v882, v883)

            if v883 == nil then
                break
            end
            if v884.Name == p878 then
                v884.Function = p879

                break
            end
        end
    end

    local _ = p876.Managers.FightingStyle
    local _IslandManager = p876.Managers.IslandManager
    local _QuestManager2 = p876.Managers.QuestManager
    local _FarmManager2 = p876.Managers.FarmManager
    local _RaidManager = p876.Managers.RaidManager
    local _ItemsQuests = p876.Managers.ItemsQuests
    local _SeaManager = p876.Managers.SeaManager
    local _PlayerTeleport3 = p876.Managers.PlayerTeleport
    local _ = u82.GameData.MaxMastery
    local _MaxLevel = u82.GameData.MaxLevel
    local _Sea5 = u82.GameData.Sea
    local _IsAlive5 = u82.IsAlive
    local _Inventory = u82.Inventory
    local _EquipTool4 = u82.EquipTool
    local _FireRemote5 = u82.FireRemote
    local _Unlocked4 = _Inventory.Unlocked
    local _Count5 = _Inventory.Count
    local _Mastery = _Inventory.Mastery
    local _IsSpawned3 = u82.Enemies.IsSpawned
    local _EnemySpawned3 = u82.EnemySpawned
    local _EnemyLocations4 = u82.EnemyLocations
    local _Elites = _FarmManager2.Enemies.Elites
    local _ = _FarmManager2.Enemies.Bones
    local _ = _FarmManager2.Enemies.Katakuri
    local _Ectoplasm = _FarmManager2.Enemies.Ectoplasm
    local _attack = _FarmManager2.attack
    local u908 = Vector3.new(0, 3, 0)
    local u909 = Vector3.new(0, 5, 0)
    local u910 = Vector3.new(0, 50, 0)
    local u911 = Vector3.new(0, -10, 0)
    local u912 = CFrame.new(-1926, 13, 1738)
    local u913 = CFrame.new(-5556, 300, -2988)
    local u914 = CFrame.new(914, 126, 33100)
    local u915 = CFrame.new(-5410, 314, -2628)
    local u916 = CFrame.new(-5561, 314, -2663)
    local u917 = CFrame.new(-8932.85, 142.87, 6063.31)
    local u918 = CFrame.new(1346, 37, -1329)
    local u919 = CFrame.new(-2103, 70, -12165)
    local u920 = CFrame.new(224, 25, -12771)
    local u921 = CFrame.new(3779, 16, -3500)
    local u922 = CFrame.new(912, 186, 33591)
    local u923 = CFrame.new(-5417, 313, -2822)
    local u924 = CFrame.new(-9513, 164, 5786)
    local u925 = CFrame.new(-1461, 30, -51)
    local u926 = CFrame.new(5864, 1209, 810)
    local u927 = CFrame.new(5251, 20, 454)
    local u928 = CFrame.new(-7739, 5657, -2289)
    local u929 = CFrame.new(-690, 15, 1583)
    local u930 = CFrame.new(-26952, 21, 329)
    local u931 = CFrame.new(-462, 73, 300)
    local u932 = CFrame.new(2289, 15, 808)
    local u933 = CFrame.new(-2777, 73, -3570)
    local u934 = CFrame.new(-1988, 124, -70)
    local u935 = CFrame.new(-12512, 340, -9872)
    local u936 = CFrame.new(-12445, 332, -7676)
    local u937 = CFrame.new(-12445, 332, -7676)
    local _RFInteractSubclassQuest = _Net:WaitForChild('RF/InteractSubclassQuest')

    _Net:WaitForChild('RF/InteractDragonQuest')

    local _RFStartSubclassQuest = _Net:WaitForChild('RF/StartSubclassQuest')
    local _RETouchKitsuneStatue = _Net:WaitForChild('RE/TouchKitsuneStatue')

    _Net:WaitForChild('RE/DragonDojoEmber')

    local _RFJuiceNetworkRF = _Net:WaitForChild('RF/JuiceNetworkRF')
    local _RFDragonHunter = _Net:WaitForChild('RF/DragonHunter')
    local _RFClaimBerry = _Net:WaitForChild('RF/ClaimBerry')
    local _SubclassNetwork2 = _Remotes:WaitForChild('SubclassNetwork')

    _Remotes:WaitForChild('QuestUpdate')

    local u945 = nil
    local u946 = 0
    local u947 = nil
    local u948 = nil
    local u949 = nil
    local u950 = nil
    local u951 = {}
    local u952 = {}
    local u953 = {
        SegmentVector = Vector3.new(0, 75, 0),
        Segment = nil,
    }
    local u954 = {
        ['Forest Pirate'] = {
            CFrame.new(-13335, 380, -7660),
            CFrame.new(-13138, 380, -7713),
            CFrame.new(-13298, 380, -7876),
            CFrame.new(-13512, 380, -7983),
            CFrame.new(-13632, 380, -7815),
        },
        ['Swan Pirate'] = {
            CFrame.new(778, 110, 1129),
            CFrame.new(1018, 110, 1128),
            CFrame.new(1020, 110, 1366),
            CFrame.new(1016, 110, 1115),
        },
    }
    local u955 = {
        Quests = {
            Evil = 'Yama',
            Good = 'Tushita',
        },
        CurrentQuest = {
            Quest = false,
            Frags = -1,
        },
        BoatsDealer = {},
        CakeQueen = CFrame.new(-710, 382, -11150),
        DoorNpc = CFrame.new(-12131, 578, -6707),
        ForestPirate = CFrame.new(-13350, 332, -7645),
        Heaven = {
            "Heaven's Guardian",
            'Cursed Skeleton',
        },
        Hell = {
            "Hell's Messenger",
            'Cursed Skeleton',
        },
        CursedSkeleton = {
            CFrame.new(-12360, 603, -6551),
            CFrame.new(-12331, 603, -6551),
        },
        OpenedDoor = false,
    }
    local u956 = {
        'Stone',
        'Hydra Leader',
        'Kilo Admiral',
        'Captain Elephant',
        'Beautiful Pirate',
    }
    local u957 = {
        GravestoneEvent = CFrame.new(-8654, 141, 6169),
        Gravestones = CFrame.new(-8760, 142, 6018),
        BuySkullGuitar = CFrame.new(-9680, 6, 6346),
        Zombies = CFrame.new(-10139, 154, 6001),
        Trophies = CFrame.new(-9529, 6, 6039),
        Ghost = CFrame.new(-9758, 270, 6291),
        Pipes = CFrame.new(-9576, 6, 6230),
    }
    local u958 = {
        FireFlower = {
            'Forest Pirate',
            'Mythological Pirate',
        },
        RequestQuest = {
            Context = 'RequestQuest',
        },
        Check = {
            Context = 'Check',
        },
    }
    local u959 = {
        Human = {
            'Fajita',
            'Diamond',
            'Jeremy',
        },
        Shark = ToDictionary({
            'Sea Beast',
        }),
    }

    ({}).Races = ToDictionary({
        'Human',
        'Skypiea',
        'Fishman',
        'Mink',
        'Cyborg',
        'Ghoul',
    })

    local u960 = {
        ['Really red'] = 'Pure Red',
        Oyster = 'Snow White',
        ['Hot pink'] = 'Winter Sky',
        Hot_Green = BrickColor.new('Lime green'),
    }
    local u961 = {
        Shipwright = ToDictionary({
            'Shark',
        }),
        SharkAnchor = ToDictionary({
            'Terrorshark',
        }),
    }

    local function u966()
        if u945 and _IsSpawned3(u945) then
            return u945
        end

        local v962, v963, v964 = pairs(u82.Bosses)

        while true do
            local v965

            v964, v965 = v962(v963, v964)

            if v964 == nil then
                break
            end
            if _IsSpawned3(v964) then
                u945 = v964

                return v964
            end
        end
    end
    local function u977()
        local v967 = _QuestManager2:GetUnlockedHakiColors()
        local _Circle = _Map['Boat Castle'].Summoner.Circle
        local _Hot_Green = u960.Hot_Green
        local v970, v971, v972 = ipairs(_Circle:GetChildren())
        local v973 = 0

        while true do
            local v974

            v972, v974 = v970(v971, v972)

            if v972 == nil then
                break
            end
            if v974:IsA('BasePart') and v974:FindFirstChild('Part') then
                local v975 = u960[v974.BrickColor.Name]
                local _Position7 = v974.Position

                if v974.Part.BrickColor ~= _Hot_Green then
                    if v967[v975] then
                        if _LocalPlayer:DistanceFromCharacter(_Position7) > 3 then
                            u83(v974.CFrame)
                        else
                            u83(place.CFrame + u909)
                            _Net:FindFirstChild('RF/FruitCustomizerRF'):InvokeServer({
                                StorageName = place_color_name,
                                Type = 'AuraSkin',
                                Context = 'Equip',
                            })
                        end
                    end
                else
                    v973 = v973 + 1
                end
            end
        end

        return v973
    end
    local function u978()
        fireclickdetector(_Map.Waterfall.SealedKatana.Hitbox.ClickDetector)
    end
    local function u984(p979, p980, p981)
        local _Quest2 = p979.Quest

        if _Quest2 and (p981 == false or not p981 and u38.BossQuest) and (_Level.Value >= p979.Level and not _QuestManager2:VerifyQuest(p980)) then
            _QuestManager2:StartQuest(_Quest2[1], _Quest2[3] or 3, _Quest2[2])

            return 'Getting Boss Quest: ' .. p980
        end

        local v983 = _EnemySpawned3(p980)

        if v983 and v983.PrimaryPart then
            return 'Killing: ' .. p980, _attack(v983)
        end
        if p979.Position then
            return 'Waiting for: ' .. p980, u83(p979.Position)
        end
    end
    local function u992()
        local _huge7 = math.huge
        local v986, v987, v988 = ipairs(workspace:GetChildren())
        local v989 = nil

        while true do
            local v990

            v988, v990 = v986(v987, v988)

            if v988 == nil then
                break
            end
            if v990.Name == 'EmberTemplate' and v990:FindFirstChild('Part') and v990.Part.Position.Y > 0 then
                local v991 = _LocalPlayer:DistanceFromCharacter(v990.Part.Position)

                if v991 < _huge7 then
                    v989 = v990.Part
                    _huge7 = v991
                end
            end
        end

        return v989
    end
    local function u994()
        if _Fragments.Value >= 1000 and not VerifyTool('Microchip') then
            _FireRemote5('BlackbeardReward', 'Microchip', '2')

            local v993 = tick()

            repeat
                task.wait()
            until VerifyTool('Microchip') or tick() - v993 > 5
        end
    end
    local function u1001()
        if u950 and u950:IsDescendantOf(_Map) then
            return u950
        end

        local v995 = _Map.Waterfall.IslandModel:GetChildren()
        local v996, v997, v998 = ipairs(v995)

        while true do
            local v999

            v998, v999 = v996(v997, v998)

            if v998 == nil then
                break
            end
            if v999:IsA('Model') and v999.Name == 'Tree' then
                local _Group = v999:FindFirstChild('Group')

                if _Group then
                    _Group = _Group:FindFirstChild('Meshes/bambootree')
                end
                if _Group and _Group.Anchored then
                    u950 = _Group

                    return _Group
                end
            end
        end
    end
    local function u1003()
        local v1002 = u1001()

        if v1002 and _LocalPlayer:DistanceFromCharacter(v1002.Position) <= 3 then
            if _Unlocked4['Skull Guitar'] then
                if VerifyTool('Skull Guitar') then
                    u82.Hooking:SetTarget(v1002)
                    _EquipTool4('Skull Guitar')
                    u82.FastAttack:ShootInTarget(v1002.Position + u911)
                else
                    _FireRemote5('LoadItem', 'Skull Guitar')
                end

                return nil
            end

            _EquipTool4(_SeaManager:RandomTool(), true)
            u82.UseSkills(v1002, u38.SeaSkills)
        elseif v1002 then
            local _ = v1002.CFrame
        end
    end
    local function u1013()
        if _LocalPlayer:DistanceFromCharacter(u957.Zombies) >= 10 then
            return u83(u957.Zombies)
        end

        local v1004 = 0
        local _Character4 = _LocalPlayer.Character
        local v1006

        if _Character4 then
            v1006 = _Character4.PrimaryPart
        else
            v1006 = _Character4
        end
        if not v1006 then
            return nil
        end

        local v1007 = _Enemies
        local v1008, v1009, v1010 = ipairs(v1007:GetChildren())

        while true do
            local v1011

            v1010, v1011 = v1008(v1009, v1010)

            if v1010 == nil then
                break
            end

            local _PrimaryPart7 = v1011.PrimaryPart

            if v1011.Name == 'Living Zombie' and _IsAlive5(v1011) and _PrimaryPart7 then
                v1004 = v1004 + 1
                _PrimaryPart7.CFrame = v1006.CFrame * CFrame.new(0, -15, -15)
                _PrimaryPart7.CanCollide = false
                _PrimaryPart7.Size = Vector3.new(60, 60, 60)
                v1011.Humanoid.WalkSpeed = 0
                v1011.Humanoid.JumpPower = 0

                v1011.Humanoid:ChangeState(14)
            end
        end

        pcall(sethiddenproperty, _LocalPlayer, 'SimulationRadius', math.huge)

        if v1004 > 5 then
            _EquipTool4()
            EnableBuso()
        elseif _Character4:FindFirstChildOfClass('Tool') then
            _Character4:FindFirstChildOfClass('Tool').Parent = _LocalPlayer.Backpack
        end
    end
    local function u1019()
        if _LocalPlayer:FindFirstChild('QuestHaze') then
            return 'Yama', 2
        end
        if _LocalPlayer:FindFirstChild('BoatQuest') then
            return 'Tushita', 1
        end
        if _Map:FindFirstChild('HellDimension') then
            return 'Yama', 3
        end
        if _Map:FindFirstChild('HeavenlyDimension') then
            return 'Tushita', 3
        end
        if _Count5['Alucard Fragment'] == 6 then
            return 'FinalQuest'
        end

        local v1014, v1015, v1016 = pairs(u955.Quests)

        while true do
            local v1017

            v1016, v1017 = v1014(v1015, v1016)

            if v1016 == nil then
                break
            end

            local v1018 = _FireRemote5('CDKQuest', 'Progress', v1016)[v1016]

            if v1018 < -2 then
                return v1017, (v1018 + 2) * -1
            end
            if 0 <= v1018 and v1018 < 3 then
                _FireRemote5('CDKQuest', 'StartTrial', v1016)

                return v1017, v1018 + 1
            end
        end
    end
    local function u1022(p1020)
        local _Specs = p1020:FindFirstChild('Specs')

        if _Specs then
            _Specs = p1020.Specs.Enabled
        end

        return _Specs
    end
    local function u1029(p1023)
        if u949 and (u949:IsDescendantOf(p1023) and u1022(u949)) then
            return u949
        end

        local v1024, v1025, v1026 = ipairs(p1023.Core.VolcanoRocks:GetChildren())

        while true do
            local v1027

            v1026, v1027 = v1024(v1025, v1026)

            if v1026 == nil then
                break
            end

            local _VFXLayer = v1027:FindFirstChild('VFXLayer')

            if _VFXLayer and u1022(_VFXLayer) then
                u949 = _VFXLayer

                return _VFXLayer
            end
        end
    end
    local function u1032(p1030)
        EnableBuso()
        _SeaManager:StopBoat()

        if p1030.Name == 'Leviathan Segment' and p1030:FindFirstChild('Head') then
            _EquipTool4(_SeaManager:RandomTool(), true)
            u82.UseSkills(p1030.Head.CFrame + u953.SegmentVector, u38.SeaSkills)

            return true, u83(p1030.Head.CFrame + u953.SegmentVector)
        end
        if p1030:FindFirstChild('Head') then
            local v1031 = CFrame.new(p1030.Head.Position.X, 60, p1030.Head.Position.Z)

            EnableBuso()
            _SeaManager:StopBoat()
            _EquipTool4(_SeaManager:RandomTool(), true)
            u82.UseSkills(v1031, u38.SeaSkills)

            return true, u83(v1031)
        end
    end

    v885('Tushita', function()
        if _Unlocked4.Tushita then
            if not _IsSpawned3('rip_indra True Form') then
                return nil
            end

            local _rip_indraTrueForm = _EnemySpawned3('rip_indra True Form')

            if _rip_indraTrueForm and _rip_indraTrueForm.PrimaryPart then
                _attack(_rip_indraTrueForm)
            else
                u83(u915)
            end

            return true
        else
            local _Tushita = u82:GetProgress('Tushita', 'TushitaProgress')

            if _Tushita.OpenedDoor then
                if _IsSpawned3('Longma') then
                    return u984(u82.Bosses.Longma, 'Longma')
                else
                    return nil
                end
            elseif VerifyTool('Holy Torch') then
                for v1035 = 1, #_Tushita.Torches do
                    if not _Tushita.Torches[v1035] then
                        _FireRemote5('TushitaProgress', 'Torch', v1035)
                    end
                end

                return true
            elseif _IsSpawned3('rip_indra True Form') then
                u83(CFrame.new(5713, 38, 255))

                return true
            else
                local v1036

                if u45.EliteHunter then
                    v1036 = false
                else
                    v1036 = u877.EliteHunter()
                end

                return v1036
            end
        end
    end, _Sea5 == 3)
    v885('Darkbeard', function()
        if _IsSpawned3('Darkbeard') then
            local _Darkbeard = _EnemySpawned3('Darkbeard')

            if _Darkbeard and _Darkbeard.PrimaryPart then
                _attack(_Darkbeard)
            else
                u83(u921)
            end

            return true
        end
        if VerifyTool('Fist of Darkness') then
            _EquipTool4('Fist of Darkness')
            u83(u921)

            return true
        end
    end, _Sea5 == 2)
    v885('CursedCaptain', function()
        if _IsSpawned3('Cursed Captain') then
            local _CursedCaptain = _EnemySpawned3('Cursed Captain')

            if _CursedCaptain and _CursedCaptain.PrimaryPart then
                _attack(_CursedCaptain)
            else
                u83(u922)
            end

            return true
        end
    end, _Sea5 == 2)
    v885('Factory', function()
        local v1039 = _Enemies:FindFirstChild('Core') or _ReplicatedStorage:FindFirstChild('Core')

        if v1039 and _IsAlive5(v1039) and v1039.PrimaryPart then
            return 'Defeating Factory', _FarmManager2.TargetPosition(v1039.PrimaryPart.CFrame)
        end
    end, _Sea5 == 2)
    v885('SkullGuitar', function()
        if _Level.Value < 2300 or (_Lighting:GetAttribute('MoonPhase') ~= 5 or _Unlocked4['Skull Guitar']) then
            return nil
        else
            local _SkullGuitar = u82:GetProgress('SkullGuitar', 'GuitarPuzzleProgress', 'Check')

            if _SkullGuitar then
                local _ = _SkullGuitar.CraftedOnce
                local _Gravestones = _SkullGuitar.Gravestones
                local _Trophies = _SkullGuitar.Trophies
                local _Swamp = _SkullGuitar.Swamp
                local _Ghost = _SkullGuitar.Ghost

                if _SkullGuitar.Pipes then
                    if _LocalPlayer:DistanceFromCharacter(u957.BuySkullGuitar.Position) then
                        _FireRemote5('soulGuitarBuy', true)
                    else
                        u83(u957.BuySkullGuitar)
                    end

                    return true
                else
                    if _Trophies then
                        u83(u957.Pipes)
                        _PlayerTeleport3:NPCTalk(u957.Pipes, 'GuitarPuzzleProgress', 'Pipes')
                    elseif _Ghost then
                        u83(u957.Trophies)
                        _PlayerTeleport3:NPCTalk(u957.Trophies, 'GuitarPuzzleProgress', 'Trophies')
                    elseif _Gravestones then
                        u83(u957.Ghost)
                        _PlayerTeleport3:NPCTalk(u957.Ghost, 'GuitarPuzzleProgress', 'Ghost')
                    elseif _Swamp then
                        u83(u957.Gravestones)
                        _PlayerTeleport3:NPCTalk(u957.Gravestones, 'GuitarPuzzleProgress', 'Gravestones')
                    else
                        u1013()
                    end

                    return true
                end
            else
                if _LocalPlayer:DistanceFromCharacter(u957.GravestoneEvent.Position) then
                    _FireRemote5('gravestoneEvent', 2, true)
                else
                    u83(u957.GravestoneEvent)
                end

                return true
            end
        end
    end, _Sea5 == 3)
    v885('CursedDualKatana', function()
        if _Unlocked4['Cursed Dual Katana'] then
            return nil
        end
        if not _Unlocked4.Tushita then
            return u877.Tushita()
        end
        if not _Unlocked4.Yama then
            return u877.Yama() or u877.EliteHunter()
        end

        local _Tushita2 = _Mastery.Tushita
        local _Yama = _Mastery.Yama

        if 350 > _Tushita2 or 350 > _Yama then
            local v1047 = _Tushita2 < 350 and 'Tushita' or 'Yama'

            if not VerifyTool(v1047) then
                _FireRemote5('LoadItem', v1047)

                return 'Getting 350 in: ' .. v1047
            end

            _EquipTool4(v1047)
            _FarmManager2.ToolDebounce()

            return u45.PirateRaid and u877.PirateRaid() or u45.Fruits and u877.Fruits() or (u45.EliteHunter and u877.EliteHunter() or u877.Bones())
        end

        local _CurrentQuest = u955.CurrentQuest
        local _ = _Map.Turtle.Cursed

        if not u955.OpenedDoor then
            local _CDKQuest = _FireRemote5('CDKQuest', 'OpenDoor')

            if _CDKQuest == 'opened' or _CDKQuest == 'can' and _FireRemote5('CDKQuest', 'OpenDoor', true) then
                u955.OpenedDoor = true

                setclipboard('Destruindo porta')

                if _Map.Turtle.Cursed:FindFirstChild('Breakable') then
                    _Map.Turtle.Cursed.Breakable:Destroy()
                end
            end

            return nil
        end
        if not _CurrentQuest.Quest or _CurrentQuest.Frags ~= _Count5['Alucard Fragment'] then
            local _AlucardFragment = _Count5['Alucard Fragment']

            _CurrentQuest.Quest = {
                u1019(),
            }
            _CurrentQuest.Frags = _AlucardFragment
        end

        local _CursedDualKatana = _ItemsQuests.CursedDualKatana
        local v1052 = _CurrentQuest.Quest[1]
        local v1053 = _CurrentQuest.Quest[2]

        if v1052 then
            if v1053 then
                if _CursedDualKatana[v1052][v1053](u955, u877) then
                    return v1052 .. v1053
                end
            elseif _CursedDualKatana[v1052](u955, u877) then
                return v1052
            end
        end
    end, _Sea5 == 3)
    v885('Raid', function()
        local _lglisedeProphtie = _Locations:FindFirstChild("l'\u{c9}glise de Proph\u{e9}tie")

        if _lglisedeProphtie and _LocalPlayer:DistanceFromCharacter(_lglisedeProphtie.Position) <= 150 then
            local _Awakener = _FireRemote5('Awakener', 'Check')

            if type(_Awakener) ~= 'table' then
                if _Awakener ~= 0 then
                    return true, _FireRemote5('Awakener', 'Teleport')
                end
            else
                if _Fragments.Value < (_Awakener.Cost or 0) then
                    return true, _FireRemote5('Awakener', 'Teleport')
                end

                _FireRemote5('Awakener', 'Awaken')
                _FireRemote5('Awakener', 'Teleport')
            end
        end
        if _RaidManager:IsRaiding() then
            local v1056 = u82:GetRaidIsland()

            if not v1056 then
                return true
            end

            local v1057 = _Enemies
            local v1058, v1059, v1060 = ipairs(v1057:GetChildren())

            while true do
                local v1061

                v1060, v1061 = v1058(v1059, v1060)

                if v1060 == nil then
                    break
                end

                local _PrimaryPart8 = v1061.PrimaryPart

                if _IsAlive5(v1061) and _PrimaryPart8 and ((v1056.Position - _PrimaryPart8.Position).Magnitude <= 1000 and 0 < _PrimaryPart8.Position.Y) then
                    return true, _attack(v1061, true, true, u38.FarmMode ~= 'Up' and u38.FarmMode or 'Star')
                end
            end

            if _LocalPlayer:DistanceFromCharacter(v1056.Position) <= 3000 then
                u83(v1056.CFrame + u910)
            end

            return true
        end
        if VerifyTool('Special Microchip') then
            return true, _RaidManager:start()
        end
    end, _Sea5 == 2 or _Sea5 == 3)
    v885('Leviathan', function()
        if not _Map:FindFirstChild('FrozenHeart') then
            local _Segment = u953.Segment

            if _Segment and _IsAlive5(_Segment) and _Segment:GetAttribute('HealthEnabled') then
                return u1032(_Segment)
            end

            local v1064 = _SeaBeasts:GetChildren()

            for v1065 = 1, #v1064 do
                local v1066 = v1064[v1065]

                if v1066.name:find('Leviathan') then
                    if _IsAlive5(v1066) then
                        if v1066:GetAttribute('HealthEnabled') then
                            u953.Segment = v1066

                            return u1032(v1066)
                        end
                    end
                end
            end
        end
    end, _Sea5 == 3)
    v885('PirateRaid', function()
        local _PirateRaid = u82.Enemies:GetTagged('PirateRaid')

        if #_PirateRaid > 0 or tick() - u82.PirateRaid <= 10 then
            for v1068 = 1, #_PirateRaid do
                if _PirateRaid[v1068].PrimaryPart then
                    return true, _attack(_PirateRaid[v1068], true, true)
                end
            end

            return true, u83(u913)
        end
    end, _Sea5 == 3)
    v885('Fruits', function()
        local v1069 = workspace:FindFirstChild('Fruit ') or workspace:FindFirstChildOfClass('Tool')

        if v1069 and (v1069:IsA('Model') or v1069:IsA('Tool')) then
            local _Handle = v1069:FindFirstChild('Handle')

            if _Handle then
                _Handle = v1069.Handle.CFrame
            end

            local v1071

            if _Handle or not v1069:IsA('Model') then
                v1071 = _Handle
            else
                v1071 = v1069:GetPivot()

                if v1071.Position == Vector3.zero then
                    v1071 = _Handle
                end
            end
            if v1071 then
                if _LocalPlayer:DistanceFromCharacter(v1071.Position) > 2 then
                    u83(v1071)
                else
                    u83(v1071 + u908)
                end

                return true
            end
        end
    end)
    v885('FireFlowers', function(p1072)
        local _FireFlowers = workspace:FindFirstChild('FireFlowers')

        if _FireFlowers then
            local v1074 = _FireFlowers:GetChildren()

            for v1075 = 1, #v1074 do
                local v1076 = v1074[v1075]
                local v1077 = not v1076:IsA('Model') or v1076.PrimaryPart or v1076:FindFirstChildOfClass('MeshPart')

                if v1077 then
                    if _LocalPlayer:DistanceFromCharacter(v1077.Position) > 3 then
                        u83(v1077.CFrame)
                    elseif v1076:FindFirstChild('ProximityPrompt') and v1076.ProximityPrompt.Enabled then
                        fireproximityprompt(v1076.ProximityPrompt)
                        task.wait(0.5)
                    end

                    return 'Collecting Fire Flower'
                end
            end
        end

        local v1078 = _EnemySpawned3(u958.FireFlower)

        if v1078 and v1078.PrimaryPart then
            _attack(v1078, true)
        else
            _PlayerTeleport3:NPCs(u954['Forest Pirate'])
        end

        return ('Getting Fire Flowers: %i/%i'):format(_Count5['Fire Flower'], p1072 or 99)
    end, _Sea5 == 3)
    v885('DracoV2V3', function()
        return _ItemsQuests:GetDracoRace(u877)
    end, _Sea5 == 3)
    v885('DojoTrainer', function()
        local _DragonTalon = u951['Dragon Talon']

        if _DragonTalon and _DragonTalon >= 500 then
            return _ItemsQuests:BeltQuests(u877)
        end
        if VerifyTool('Dragon Talon') then
            if _DragonTalon then
                u951['Dragon Talon'] = GetToolMastery('Dragon Talon')

                _EquipTool4('Dragon Talon')
                _FarmManager2.ToolDebounce()

                return u877.Bones()
            end

            u951['Dragon Talon'] = GetToolMastery('Dragon Talon')
        else
            _FireRemote5('BuyDragonTalon')
        end

        return true
    end, _Sea5 == 3)
    v885('DragonHunter', function()
        if u947 == 'Locked' then
            return nil
        end

        local v1080 = u992()

        if v1080 then
            u83(v1080.CFrame)

            return 'Colleting Blaze Ember'
        end
        if not (u947 and u947.Text) then
            if _LocalPlayer:DistanceFromCharacter(u926.Position) >= 5 then
                u83(u926)
            else
                u947 = _RFDragonHunter:InvokeServer(u958.Check)

                if u947 and not u947.Text then
                    pcall(_RFDragonHunter.InvokeServer, _RFDragonHunter, u958.RequestQuest)
                end
            end

            return 'Getting Dragon Hunter Quest'
        end

        local _Text = u947.Text

        if _Text:find('Defeat') then
            local v1082 = _Text:find('Venomous') and 'Venomous Assailant' or 'Hydra Enforcer'
            local v1083 = _EnemySpawned3(v1082)
            local v1084 = _EnemyLocations4[v1082]

            if v1083 and v1083.PrimaryPart then
                _attack(v1083, true)
            elseif v1084 then
                _PlayerTeleport3:NPCs(v1084)
            end

            return 'Killing: ' .. v1082
        end
        if _Text:find('Destroy') then
            u1003()

            return "Breaking Hydra Island Tree's"
        end
    end, _Sea5 == 3)
    v885('MirageFruitDealer', function()
        if _IslandManager:GetSpawnedIsland('MysticIsland') then
            local v1085 = _IslandManager:GetMirageFruitDealer()

            if v1085 and v1085.PrimaryPart then
                u83(v1085.PrimaryPart.CFrame)

                return true
            end
        end
    end, _Sea5 == 3)
    v885('MirageGear', function()
        local _MysticIsland = _Map:FindFirstChild('MysticIsland')

        if _MysticIsland then
            local v1087 = _IslandManager:GetMirageGear(_MysticIsland)

            if v1087 and v1087.Transparency < 1 then
                u83(v1087.CFrame)

                return true
            end
        end
    end, _Sea5 == 3)
    v885('MirageChests', function()
        if _Map:FindFirstChild('MysticIsland') then
            local _ = u877.ChestTween
            local _ = _Map.MysticIsland
        end
    end)
    v885('TeleportMirage', function()
        local _MysticIsland2 = _Map:FindFirstChild('MysticIsland')

        if _MysticIsland2 then
            _MysticIsland2 = _IslandManager:GetMirageTop(_MysticIsland2)
        end
        if _MysticIsland2 then
            u83(_MysticIsland2.CFrame * CFrame.new(0, 211.8, 0))

            return true
        end
    end, _Sea5 == 3)
    v885('CraftVolcanicMagnet', function()
        if not (_Unlocked4['Volcanic Magnet'] or _Map:FindFirstChild('PrehistoricIsland')) then
            if _Count5['Scrap Metal'] < 10 then
                return _FarmManager2:Material('Leather + Scrap Metal')
            end
            if _Count5['Blaze Ember'] < 15 then
                return u877.DragonHunter()
            end
            if _LocalPlayer:DistanceFromCharacter(u926.Position) >= 3 then
                u83(u926)
            else
                _FireRemote5('CraftItem', 'Craft', 'Volcanic Magnet')
            end

            return true
        end
    end, _Sea5 == 3)
    v885('PrehistoricBones', function()
        if _Count5['Dinosaur Bones'] >= 99 then
            return nil
        end
        if _LocalPlayer:GetAttribute('PrehistoricIslandParticipant') and workspace:FindFirstChild('PrehistoricIsland') then
            local v1089 = workspace:GetChildren()

            for v1090 = 1, #v1089 do
                local v1091 = v1089[v1090]

                if v1091.Name == 'DinoBone' then
                    if v1091:IsA('BasePart') then
                        if (v1091.Position - workspace.PrehistoricIsland:GetPivot().Position).Magnitude <= 1500 then
                            if _LocalPlayer:DistanceFromCharacter(v1091.Position) > 3 then
                                u83(v1091.CFrame)
                            else
                                u83(v1091.CFrame + u909)
                            end

                            u946 = tick()

                            return 'Collecting Dinosaur Bones'
                        end
                    end
                end
            end
        end
    end, _Sea5 == 3)
    v885('PrehistoricEgg', function()
        local _PrehistoricIsland = _IslandManager:GetSpawnedIsland('PrehistoricIsland')

        if _PrehistoricIsland then
            local _Core2 = _PrehistoricIsland:FindFirstChild('Core')

            if _Core2 then
                _Core2 = _Core2:FindFirstChild('SpawnedDragonEggs')
            end
            if _Core2 and 0 < #_Core2:GetChildren() then
                local _DragonEgg = _Core2:FindFirstChild('DragonEgg')

                if _DragonEgg then
                    _DragonEgg = _DragonEgg:FindFirstChild('Molten')
                end
                if _DragonEgg and _DragonEgg:FindFirstChild('ProximityPrompt') and _DragonEgg.ProximityPrompt.Enabled then
                    if _LocalPlayer:DistanceFromCharacter(_DragonEgg.Position) >= 3 then
                        u83(_DragonEgg.CFrame)
                    else
                        fireproximityprompt(_DragonEgg.ProximityPrompt)
                        task.wait(0.5)
                    end

                    u946 = tick()

                    return 'Collecting Dragon Egg'
                end
            end
        end
    end, _Sea5 == 3)
    v885('LavaGolem', function()
        local _PrehistoricIsland2 = _IslandManager:GetSpawnedIsland('PrehistoricIsland')

        if _PrehistoricIsland2 and _PrehistoricIsland2:GetAttribute('IsMinigameActive') then
            local v1096 = _Enemies
            local v1097, v1098, v1099 = ipairs(v1096:GetChildren())

            while true do
                local v1100

                v1099, v1100 = v1097(v1098, v1099)

                if v1099 == nil then
                    break
                end

                local _PrimaryPart9 = v1100.PrimaryPart

                if v1100.Name == 'Lava Golem' and _PrimaryPart9 and _PrimaryPart9.Position.Y > 0 then
                    _attack(v1100, true)

                    u946 = tick()

                    return 'Defeating Lava Golem'
                end
            end
        end
    end, _Sea5 == 3)
    v885('PrehistoricIsland', function()
        local _PrehistoricIsland3 = _IslandManager:GetSpawnedIsland('PrehistoricIsland')

        if _PrehistoricIsland3 then
            local v1103 = _IslandManager:GetPrehistoricActivationPrompt(_PrehistoricIsland3)

            if not v1103 then
                return true, _SeaManager:StopBoat()
            end
            if v1103.Parent:FindFirstChild('InteriorLava') then
                v1103.Parent.InteriorLava:Destroy()
            end
            if _PrehistoricIsland3:GetAttribute('IsMinigameActive') then
                local v1104 = tick()

                RemoveCanTouch = tick()
                u946 = v1104

                local v1105 = u1029(_PrehistoricIsland3)

                if v1105 then
                    if _LocalPlayer:DistanceFromCharacter(v1105.Position) >= 5 then
                        u83(v1105.CFrame, false, false, true)
                    else
                        _EquipTool4(_SeaManager:RandomTool(), true)
                        u82.UseSkills(v1105, u38.SeaSkills)
                    end
                else
                    u83(v1103.CFrame, false, false, true)
                end

                return 'Volcano Patch'
            end
            if _LocalPlayer:DistanceFromCharacter(v1103.Position) > 3 then
                u946 = tick()

                u83(v1103.CFrame)

                return 'Teleporting to Prehistoric Island'
            end
            if v1103:FindFirstChild('ProximityPrompt') and v1103.ProximityPrompt.Enabled then
                u946 = tick()

                fireproximityprompt(v1103.ProximityPrompt)
                task.wait(0.5)

                return 'Waiting...'
            end
            if u38.ResetPrehistoric and 8 <= tick() - u946 and _IsAlive5(_LocalPlayer.Character) then
                _LocalPlayer.Character.Humanoid.Health = 0

                return 'Reseting...'
            end
        end
        if u45.Sea and u38.aTweenBoat or u45.KitsuneIsland and _Map:FindFirstChild('KitsuneIsland') then
            return nil
        end
        if _SeaManager:GetPlayerBoat() then
            _SeaManager:RandomTeleport('inf')
        else
            _SeaManager:BuyNewBoat()
        end

        return 'Finding Prehistoric Island'
    end, _Sea5 == 3)
    v885('KitsuneIsland', function()
        local _KitsuneIsland = _Map:FindFirstChild('KitsuneIsland')

        if not _KitsuneIsland or _Lighting:GetAttribute('MoonPhase') ~= 5 then
            if u45.Sea then
                return nil
            end
            if _SeaManager:GetPlayerBoat() then
                _SeaManager:RandomTeleport('6')
            else
                _SeaManager:BuyNewBoat()
            end

            return true
        end
        if _Lighting:GetAttribute('IsBlueMoon') and _Lighting:GetAttribute('BlueMoonEnded') then
            return nil
        end

        local v1107 = u992()

        if v1107 then
            u83(v1107.CFrame)

            return true
        end

        local _ShrineDialogPart = _KitsuneIsland:FindFirstChild('ShrineDialogPart')

        if _ShrineDialogPart then
            if _LocalPlayer:DistanceFromCharacter(_ShrineDialogPart.Position) > 3 then
                u83(_ShrineDialogPart.CFrame)
            elseif _Lighting:GetAttribute('MoonPhase') == 5 and not _Lighting:GetAttribute('IsBlueMoon') then
                _RETouchKitsuneStatue:FireServer()
            end
        elseif _KitsuneIsland.WorldPivot then
            u83(_KitsuneIsland.WorldPivot)
        end

        return true
    end, _Sea5 == 3)
    v885('Shipwright', function()
        if _Subclass.Value == 'Shipwright' then
            return nil
        end

        local _Shipwright, v1110 = _RFInteractSubclassQuest:InvokeServer('Shipwright')

        if _Shipwright == 1 then
            _RFStartSubclassQuest:InvokeServer('Shipwright')
        elseif _Shipwright == 3 then
            if (tonumber(v1110) or 0) < 20 then
                return u877.Sea(u961.Shipwright)
            end
        elseif _Shipwright == 4 or _Shipwright == 2 then
            if _SubclassNetwork2.GetPlayerData:InvokeServer().Purchased.Shipwright == nil then
                if _Fragments.Value >= 3000 then
                    _SubclassNetwork2.PurchaseSubclass:InvokeServer('Shipwright')
                end
            else
                _SubclassNetwork2.EquipSubclass:InvokeServer('Shipwright')
            end
        end
    end, _Sea5 == 3)
    v885('RaceV2', function()
        if _Data.Race.Value == 'Draco' or not _Unlocked4['Warrior Helmet'] or _Data.Race:FindFirstChild('Evolved') then
            return nil
        end

        local _RaceV2 = u82:GetProgress('RaceV2', 'Alchemist', '1')

        if _RaceV2 == 0 or _RaceV2 == 2 then
            if _RaceV2 ~= 2 or 500000 <= _Beli.Value then
                if _LocalPlayer:DistanceFromCharacter(u933.Position) >= 5 then
                    u83(u933)
                else
                    _FireRemote5('Alchemist', _RaceV2 == 0 and '2' or '3')
                end

                return true
            end
        elseif _RaceV2 == 1 then
            for v1112 = 1, 2 do
                local v1113 = workspace:FindFirstChild('Flower' .. v1112)

                if v1113 then
                    if v1113.Transparency ~= 1 then
                        if not VerifyTool('Flower ' .. v1112) then
                            return 'Collecting Flower: ' .. v1112, u83(v1113.CFrame)
                        end
                    end
                end
            end

            if not VerifyTool('Flower 3') then
                local _SwanPirate = _EnemySpawned3('Swan Pirate')

                if _SwanPirate and _SwanPirate.PrimaryPart then
                    _attack(_SwanPirate)
                else
                    _PlayerTeleport3:NPCs(u954['Swan Pirate'])
                end

                return 'Getting Flower: 3'
            end
        end
    end, _Sea5 == 2)
    v885('RaceV3', function()
        local _Value2 = _Data.Race.Value

        if _Value2 == 'Draco' or (not _Data.Race:FindFirstChild('Evolved') or u952.RaceV3 and u952.RaceV3[_Value2]) then
            return nil
        end

        local _RaceV3 = u82:GetProgress('RaceV3', 'Wenlocktoad', '1')

        if _RaceV3 == -2 then
            if u952.RaceV3 then
                u952.RaceV3[_Value2] = true
            else
                u952.RaceV3 = {[_Value2] = true}
            end

            return nil
        end
        if _RaceV3 == 0 or _RaceV3 == 2 then
            if _RaceV3 ~= 2 or 2000000 <= _Beli.Value then
                if _LocalPlayer:DistanceFromCharacter(u934.Position) >= 5 then
                    u83(u934)
                else
                    _FireRemote5('Wenlocktoad', _RaceV3 == 0 and '2' or '3')
                end

                return true
            end
        elseif _RaceV3 == 1 then
            if _Value2 == 'Fishman' then
                return u877.Sea(u959.Shark)
            end
            if _Value2 == 'Human' then
                local v1117, v1118, v1119 = ipairs(u959.Human)

                while true do
                    local v1120

                    v1119, v1120 = v1117(v1118, v1119)

                    if v1119 == nil then
                        break
                    end
                    if _IsSpawned3(v1120) then
                        return u984(u82.Bosses[v1120], v1120)
                    end
                end
            elseif _Value2 == 'Mink' then
                local _ = u877.ChestTween
            end
        end
    end, _Sea5 == 2)
    v885('Sea', function(p1121)
        local v1122 = _SeaManager:GetPlayerBoat()

        if not v1122 then
            _SeaManager:BuyNewBoat()

            return true
        end

        local v1123 = p1121 or u38.seaEnemy

        if not v1123 then
            return nil
        end

        local v1124 = v1123.PirateBrigade and _SeaManager:GetSeaEvent('PirateBrigade')

        if v1124 then
            _SeaManager:attackSeaEvent(v1124)

            return true
        end

        local v1125 = v1123['Sea Beast'] and _SeaManager:GetSeaBeast()

        if v1125 then
            _SeaManager:attackSeaBeast(v1125)

            return true
        end
        if _SeaManager:RepairBoat(v1122) then
            return true
        end
        if v1122 then
            _SeaManager:RandomTeleport()

            return true
        end
    end, _Sea5 == 2)
    v885('Sea', function(p1126, p1127)
        local v1128 = _SeaManager:GetPlayerBoat()

        if not v1128 then
            _SeaManager:BuyNewBoat()

            return true
        end

        local v1129 = p1127 or u38.boatSelected
        local v1130 = p1126 or u38.fishSelected
        local v1131 = v1130['Sea Beast'] and _SeaManager:GetSeaBeast()

        if v1131 then
            _SeaManager:attackSeaBeast(v1131)

            return true
        end

        local v1132, v1133, v1134 = pairs(v1130)

        while true do
            local v1135

            v1134, v1135 = v1132(v1133, v1134)

            if v1134 == nil then
                break
            end
            if v1135 and v1134 ~= 'Sea Beast' then
                local v1136 = _SeaManager:GetSeaEvent(v1134)

                if v1136 then
                    _SeaManager:attackSeaEvent(v1136)

                    return true
                end
            end
        end

        local v1137, v1138, v1139 = pairs(v1129)

        while true do
            local v1140

            v1139, v1140 = v1137(v1138, v1139)

            if v1139 == nil then
                break
            end
            if v1140 then
                local v1141 = _SeaManager:GetSeaEvent(v1139)

                if v1141 then
                    _SeaManager:attackSeaEvent(v1141)

                    return true
                end
            end
        end

        if _SeaManager:RepairBoat(v1128) then
            return true
        end
        if u38.aTweenBoat and v1128 then
            _SeaManager:RandomTeleport()

            return true
        end
    end, _Sea5 == 3)
    v885('Rengoku', function()
        if _Unlocked4.Rengoku or u45.Level and _Level.Value < 1350 then
            return nil
        end
        if VerifyTool('Library Key') then
            return _FireRemote5('OpenLibrary')
        end
        if VerifyTool('Hidden Key') then
            return _FireRemote5('OpenRengoku')
        end
        if _IsSpawned3('Awakened Ice Admiral') then
            return u984(u82.Bosses['Awakened Ice Admiral'], 'Awakened Ice Admiral')
        end
        if _Level.Value >= 1425 or not u45.Level then
            local _ArcticWarrior = _EnemySpawned3('Arctic Warrior', 'Snow Lurker')

            if _ArcticWarrior and _ArcticWarrior.PrimaryPart then
                _attack(_ArcticWarrior)

                return true
            end
        end
    end, _Sea5 == 2)
    v885('Bartilo', function()
        if _Level.Value < 850 or _Unlocked4['Warrior Helmet'] then
            return nil
        end

        local _Bartilo = u82:GetProgress('Bartilo', 'BartiloQuestProgress')

        if _Bartilo.KilledSpring then
            _FireRemote5('BartiloQuestProgress', 'DidPlates')
        elseif _Bartilo.KilledBandits then
            if _IsSpawned3('Jeremy') then
                local _Jeremy = _EnemySpawned3('Jeremy')

                if _Jeremy and _Jeremy.PrimaryPart then
                    _attack(_Jeremy)
                else
                    u83(CFrame.new(2316, 449, 787))
                end

                return true
            end
        elseif not _Bartilo.KilledBandits then
            local _SwanPirate2 = _QuestManager2:VerifyQuest('Swan Pirate')

            if _SwanPirate2 then
                _SwanPirate2 = _QuestManager2:VerifyQuest('50')
            end
            if _SwanPirate2 then
                local _SwanPirate3 = _EnemySpawned3('Swan Pirate')

                if _SwanPirate3 and _SwanPirate3.PrimaryPart then
                    _attack(_SwanPirate3)
                else
                    _PlayerTeleport3:NPCs(u954['Swan Pirate'])
                end
            else
                _QuestManager2:StartQuest('BartiloQuest', 1, u931)
            end

            return true
        end
    end, _Sea5 == 2)
    v885('Yama', function()
        if _Unlocked4.Yama then
            return nil
        end
        if u82:GetProgress('EliteProgress', 'EliteHunter', 'Progress') >= 30 then
            if _LocalPlayer:DistanceFromCharacter(u927.Position) >= 5 then
                u83(u927)
            else
                pcall(u978)
                task.wait(1)
            end

            return true
        end
    end, _Sea5 == 3)
    v885('Citizen', function()
        if _Level.Value < 1800 or _Unlocked4['Musketeer Hat'] then
            return nil
        end

        local _Citizen = u82:GetProgress('Citizen', 'CitizenQuestProgress')

        if _Citizen.FoundTreasure then
            return nil
        end
        if _Citizen.KilledBoss then
            u83(u935)

            return true
        end
        if not _Citizen.KilledBandits then
            local _ForestPirate2 = _QuestManager2:VerifyQuest('Forest Pirate')

            if _ForestPirate2 then
                _ForestPirate2 = _QuestManager2:VerifyQuest('50')
            end
            if not _ForestPirate2 then
                if _LocalPlayer:DistanceFromCharacter(u937.Position) < 5 then
                    u83(u937)
                else
                    _FireRemote5('CitizenQuest', 1)
                end

                return true
            end

            local _ForestPirate3 = _EnemySpawned3('Forest Pirate')

            if _ForestPirate3 and _ForestPirate3.PrimaryPart then
                _attack(_ForestPirate3, true)
            else
                _PlayerTeleport3:NPCs(u954['Forest Pirate'])
            end

            return true
        end
        if _IsSpawned3('Captain Elephant') then
            if not _QuestManager2:VerifyQuest('Captain Elephant') then
                if _LocalPlayer:DistanceFromCharacter(u937.Position) < 5 then
                    u83(u937)
                else
                    _FireRemote5('CitizenQuestProgress', 'Citizen')
                end

                return true
            end

            local _CaptainElephant = _EnemySpawned3('Captain Elephant')

            if _CaptainElephant and _CaptainElephant.PrimaryPart then
                _attack(_CaptainElephant)
            else
                u83(u936)
            end

            return true
        end
    end, _Sea5 == 3)
    v885('RainbowHaki', function()
        local v1151 = _QuestManager2:VerifyQuest(u956)

        if v1151 then
            if _IsSpawned3(v1151) then
                return u984(u82.Bosses[v1151], v1151, true)
            end
        else
            _FireRemote5('HornedMan', 'Bet')
        end
    end, _Sea5 == 3)
    v885('EliteHunter', function()
        local v1152 = _QuestManager2:VerifyQuest(_Elites)

        if (u45.DoughKing or (u45.CakePrince or u45.RipIndra)) and (_IsSpawned3('rip_indra True Form') or _IsSpawned3('Dough King') or (_IsSpawned3('Cake Prince') or VerifyTool("God's Chalice")) or VerifyTool('Sweet Chalice')) then
            return nil
        end
        if v1152 then
            local v1153 = _EnemySpawned3(v1152)

            if v1153 and v1153.PrimaryPart then
                return 'Killing Elite Hunter: ' .. v1152, _attack(v1153)
            end
        else
            local _Elite2 = u82.Enemies:GetEnemyByTag('Elite')

            if _Elite2 then
                u83(u923)
                _PlayerTeleport3:talkNpc(u923, 'EliteHunter')

                return 'Getting Elite Quest: ' .. _Elite2.Name
            end
        end
    end, _Sea5 == 3)
    v885('AuraColor', function()
        local _CraftAura = u38.CraftAura

        if _CraftAura and not _Unlocked4[_CraftAura] then
            local v1156 = _QuestManager2:GetAuraCraft(_CraftAura)

            if not type(v1156) ~= 'table' then
                return nil
            end

            local v1157, v1158, v1159 = ipairs(v1156)
            local v1160 = {}

            while true do
                local v1161

                v1159, v1161 = v1157(v1158, v1159)

                if v1159 == nil then
                    break
                end
                if _Count5[v1161.Name] < v1161.Amount then
                    table.insert(v1160, v1161.Name)
                end
            end

            if #v1160 <= 0 then
                local _Barista = _FarmManager2:GetNpcPosition('Barista')

                if _LocalPlayer:DistanceFromCharacter(_Barista.Position) >= 3 then
                    u83(_Barista)
                else
                    _RFJuiceNetworkRF:InvokeServer({
                        StorageName = _CraftAura,
                        Type = 'AuraSkin',
                        Context = 'Craft',
                    })
                end

                return true
            end
            if u45.BerryBush then
                v1160 = nil
            end
            if u877.BerryBush(v1160, u38.CraftHop) then
                return true
            end

            task.wait(0.3)
        end
    end, _Sea5 ~= 1)
    v885('BerryBush', function(p1163, p1164)
        local v1165 = u82.Berry(p1163)

        if v1165 and v1165.Parent then
            local v1166, v1167, v1168 = pairs(v1165:GetAttributes())
            local v1169, v1170 = v1166(v1167, v1168)

            if v1169 ~= nil then
                local _Parent2 = v1165.Parent
                local v1172 = _Parent2:GetPivot() * _Parent2:GetAttribute(v1169)

                if _LocalPlayer:DistanceFromCharacter(v1172.Position) >= 3 then
                    u83(v1172)
                else
                    _RFClaimBerry:InvokeServer(_Parent2.Name, v1169)
                end

                return 'Collecting Berry: ' .. v1170
            end
        elseif p1164 or p1164 == nil and u38.BerryHop then
            u82:ServerHop()
        end
    end)
    v885('ThirdSea', function()
        if _Level.Value < 1500 or _Level.Value >= 1850 then
            return nil
        else
            local _Zou1 = u82:GetProgress('Zou1', 'ZQuestProgress')

            if u952.Zou2 or u82:GetProgress('Zou2', 'ZQuestProgress', 'Check') then
                if not u952.Zou2 then
                    u952.Zou2 = true
                end
                if _LocalPlayer:DistanceFromCharacter(u930.Position) < 1200 then
                    local _rip_indra = _Enemies:FindFirstChild('rip_indra')

                    if _rip_indra and _rip_indra.PrimaryPart and _rip_indra.PrimaryPart.Position.Y > 0 then
                        _attack(_rip_indra)
                    end

                    return true
                end
                if _Zou1.KilledIndraBoss then
                    return u82:TravelTo(3)
                end
                if _LocalPlayer:DistanceFromCharacter(u912.Position) < 5 then
                    _FireRemote5('ZQuestProgress', 'Begin')

                    u32.OnFarm = false

                    repeat
                        task.wait()
                    until _LocalPlayer:DistanceFromCharacter(u930.Position) < 1200 or not u45[u38.RunningOption]

                    return true
                end

                u83(u912)

                return
            elseif u82:GetProgress('Unlockables', 'GetUnlockables').FlamingoAccess then
                return u877.DonSwan()
            else
                return nil
            end
        end
    end, _Sea5 == 2)
    v885('DonSwan', function()
        if not _Unlocked4['Warrior Helmet'] then
            return nil
        end
        if _IsSpawned3('Don Swan') then
            local _DonSwan = _EnemySpawned3('Don Swan')

            if _DonSwan and _DonSwan.PrimaryPart then
                _attack(_DonSwan)
            else
                u83(u932)
            end

            return true
        end
    end, _Sea5 == 2)
    v885('SecondSea', function()
        if _Level.Value < 700 then
            return nil
        end

        local _Dressrosa = u82:GetProgress('Dressrosa', 'DressrosaQuestProgress')

        if _Dressrosa.KilledIceBoss then
            return u82:TravelTo(2)
        end
        if _Dressrosa.TalkedDetective then
            if _Dressrosa.UsedKey then
                if not _Dressrosa.KilledIceBoss then
                    local _IceAdmiral = _EnemySpawned3('Ice Admiral')

                    if _IceAdmiral and _IceAdmiral.PrimaryPart then
                        _attack(_IceAdmiral)
                    else
                        u83(u918)
                    end
                end
            else
                if not VerifyTool('Key') then
                    _FireRemote5('DressrosaQuestProgress', 'Detective')
                end

                _EquipTool4('Key')
                _FireRemote5('DressrosaQuestProgress', 'UseKey')
            end
        else
            _FireRemote5('DressrosaQuestProgress', 'Detective')
        end

        return true
    end, _Sea5 == 1)
    v885('Order', function()
        local _Order = _Enemies:FindFirstChild('Order')

        if _Order and _Order.PrimaryPart then
            _attack(_Order)

            return true
        end
        if VerifyTool('Microchip') then
            return fireclickdetector(_Map.CircleIsland.RaidSummon.Button.Main.ClickDetector)
        end

        local _ = u38.FullyLawRaid
    end, _Sea5 == 2)
    v885('Saber', function()
        if _Level.Value < 200 or _Unlocked4.Saber then
            return nil
        end

        local _Shanks = u82:GetProgress('Shanks', 'ProQuestProgress')

        if _Shanks.UsedRelic then
            if u82.Enemies.IsSpawned('Saber Expert') then
                local _SaberExpert = _EnemySpawned3('Saber Expert')

                if _SaberExpert and _SaberExpert.PrimaryPart then
                    _attack(_SaberExpert)
                else
                    u83(u925)
                end

                return true
            end
        else
            if _Shanks.KilledMob then
                if VerifyTool('Relic') then
                    _FireRemote5('ProQuestProgress', 'PlaceRelic')
                else
                    _FireRemote5('ProQuestProgress', 'RichSon')
                end

                return true
            end
            if not _Shanks.UsedCup then
                if _Shanks.UsedTorch then
                    if VerifyTool('Cup') then
                        _FireRemote5('ProQuestProgress', 'FillCup', _LocalPlayer.Character and _LocalPlayer.Character:FindFirstChild('Cup') or _LocalPlayer.Backpack:FindFirstChild('Cup'))
                    else
                        _FireRemote5('ProQuestProgress', 'GetCup')
                    end

                    _FireRemote5('ProQuestProgress', 'SickMan')

                    return true
                end

                local v1181 = next
                local _Plates = _Shanks.Plates
                local v1183 = nil

                while true do
                    local v1184

                    v1183, v1184 = v1181(_Plates, v1183)

                    if v1183 == nil then
                        break
                    end
                    if not v1184 then
                        _FireRemote5('ProQuestProgress', 'Plate', v1183)

                        return true
                    end
                end

                if VerifyTool('Torch') then
                    _FireRemote5('ProQuestProgress', 'DestroyTorch')
                else
                    _FireRemote5('ProQuestProgress', 'GetTorch')
                end

                return true
            end
            if not _Shanks.TalkedSon then
                return _FireRemote5('ProQuestProgress', 'RichSon')
            end
            if u82.Enemies.IsSpawned('Mob Leader') then
                local _MobLeader = _EnemySpawned3('Mob Leader')

                if _MobLeader and _MobLeader.PrimaryPart then
                    _attack(_MobLeader)
                else
                    u83(CFrame.new(-2880, 9, 5430))
                end

                return true
            end
        end
    end, _Sea5 == 1)
    v885('PoleV1', function()
        if _Level.Value < 450 or _Unlocked4['Pole (1st Form)'] then
            return nil
        end
        if u82.Enemies.IsSpawned('Thunder God') then
            local _ThunderGod = _EnemySpawned3('Thunder God')

            if _ThunderGod and _ThunderGod.PrimaryPart then
                _attack(_ThunderGod)
            else
                u83(u928)
            end

            return true
        end
    end, _Sea5 == 1)
    v885('TheSaw', function()
        if _Level.Value < 100 or _Unlocked4['Shark Saw'] then
            return nil
        end
        if u82.Enemies.IsSpawned('The Saw') then
            local _TheSaw = _EnemySpawned3('The Saw')

            if _TheSaw and _TheSaw.PrimaryPart then
                _attack(_TheSaw)
            else
                u83(u929)
            end

            return true
        end
    end, _Sea5 == 1)
    v885('SoulReaper', function()
        local _SoulReaper2 = _EnemySpawned3('Soul Reaper')

        if _SoulReaper2 and _SoulReaper2.PrimaryPart then
            _attack(_SoulReaper2)

            return true
        end
        if VerifyTool('Hallow Essence') then
            _EquipTool4('Hallow Essence')
            u83(u917)

            return true
        end
    end, _Sea5 == 3)
    v885('RipIndra', function()
        if _IsSpawned3('rip_indra True Form') then
            local _rip_indraTrueForm2 = _EnemySpawned3('rip_indra True Form')

            if _rip_indraTrueForm2 and _rip_indraTrueForm2.PrimaryPart then
                _attack(_rip_indraTrueForm2)
            else
                u83(u915)
            end

            return 'Killing: rip_indra True Form'
        end
        if VerifyTool("God's Chalice") then
            if u977() < 3 then
                u83(u915)
            else
                u83(u916)
            end

            return "God's Chalice: rip_indra True Form"
        end
    end, _Sea5 == 3)
    v885('BossSelected', function()
        local _BossSelected = u38.BossSelected
        local v1191

        if _BossSelected then
            v1191 = _IsSpawned3(_BossSelected)
        else
            v1191 = _BossSelected
        end
        if v1191 then
            local _ = u82.Bosses[_BossSelected]
        end
    end)
    v885('AllBosses', function()
        local v1192 = u966()

        if v1192 then
            local _ = u82.Bosses[v1192]
        end
    end)
    v885('DoughKing', function()
        local v1193 = _EnemySpawned3('Dough King') or _EnemySpawned3('Cake Prince')

        if VerifyTool('Red Key') then
            _FireRemote5('CakeScientist', 'Check')

            return true
        else
            if v1193 and v1193.PrimaryPart then
                _attack(v1193)
            else
                if not VerifyTool('Sweet Chalice') and VerifyTool("God's Chalice") then
                    if _Count5['Conjured Cocoa'] < 10 then
                        return _FarmManager2:Material('Conjured Cocoa')
                    end

                    u83(u920)
                    _PlayerTeleport3:talkNpc(u920, 'SweetChaliceNpc')

                    return true
                end

                local _CakePrince = u82.Enemies:GetClosestByTag('CakePrince')

                if _CakePrince and _CakePrince.PrimaryPart then
                    _attack(_CakePrince, true, true)
                else
                    u83(u919)
                end
            end

            return true
        end
    end, _Sea5 == 3)
    v885('CakePrince', function()
        if u45.DoughKing then
            return nil
        end

        local v1195 = _EnemySpawned3('Dough King') or _EnemySpawned3('Cake Prince')

        if v1195 and v1195.PrimaryPart then
            _attack(v1195)
        else
            local _CakePrince2 = u82.Enemies:GetClosestByTag('CakePrince')

            if _CakePrince2 and _CakePrince2.PrimaryPart then
                _attack(_CakePrince2, true, true)
            else
                u83(u919)
            end
        end

        return true
    end, _Sea5 == 3)
    v885('ChestTween', function(p1197, p1198)
        local v1199 = u82.Chests()

        if v1199 then
            local v1200 = v1199:GetPivot(p1198)

            if _LocalPlayer:DistanceFromCharacter(v1200.Position) >= 3 then
                u83(v1200)
            else
                u83(v1200 + u909)
                task.wait(0.15)
            end

            return 'Collecting Chest' .. (p1197 or '')
        end
    end)
    v885('Ectoplasm', function()
        local v1201 = _EnemySpawned3(_Ectoplasm)

        if v1201 and v1201.PrimaryPart then
            return 'Killing: ' .. v1201.Name, _attack(v1201, true, true)
        else
            return 'Waiting for: Enemy Spawn', u83(u914)
        end
    end, _Sea5 == 2)
    v885('Bones', function()
        if u45.Level and _Level.Value < _MaxLevel then
            return nil
        else
            local _Bones2 = u82.Enemies:GetClosestByTag('Bones')

            if _Bones2 and _Bones2.PrimaryPart then
                return 'Killing: ' .. _Bones2.Name, _attack(_Bones2, true, true)
            else
                return 'Waiting for: Enemy Spawn', u83(u924)
            end
        end
    end, _Sea5 == 3)
    v885('Level', function()
        local v1203 = _QuestManager2:GetQuest()

        if not v1203 then
            return nil
        end

        local _Name2 = v1203.Enemy.Name
        local _Position8 = v1203.Enemy.Position
        local v1206 = _QuestManager2:VerifyQuest(_Name2)

        if v1206 and u82.IsBoss(v1206) then
            return u984(u82.Bosses[v1206], v1206, false)
        end
        if not v1206 then
            local v1207 = _QuestManager2

            return _QuestManager2:StartQuest(v1203.Name, v1203.Count, v1207:GetQuestPosition(v1203.Name))
        end

        local v1208 = _EnemySpawned3(v1206)

        if v1208 and v1208.PrimaryPart then
            return 'Killing: ' .. v1208.Name, _attack(v1208, true)
        end

        local v1209 = _QuestManager2:GetQuestPosition(v1203.Name)

        if #_Position8 <= 0 then
            if v1209 then
                u83(v1209 * _QuestManager2._Position)
            end
        else
            _PlayerTeleport3:NPCs(_Position8)
        end

        return 'Waiting for: ' .. v1206
    end)
    v885('Mastery', function()
        if _Sea5 ~= 3 or _MaxLevel > _Level.Value then
            return u877.Level()
        else
            return u877.Bones()
        end
    end)
    v885('Material', function()
        if u38.fMaterial then
            local _ = _FarmManager2.Material
            local _ = u38.fMaterial
        end
    end)
    v885('Nearest', function()
        local v1210 = u948

        if v1210 then
            v1210 = u948.PrimaryPart
        end
        if v1210 and _IsAlive5(u948) and _LocalPlayer:DistanceFromCharacter(v1210.Position) < 1500 then
            return 'Killing: ' .. u948.Name, _attack(u948, true, true)
        end

        local v1211 = _Enemies
        local v1212, v1213, v1214 = ipairs(v1211:GetChildren())
        local v1215 = 1500
        local v1216 = nil

        while true do
            local v1217

            v1214, v1217 = v1212(v1213, v1214)

            if v1214 == nil then
                break
            end

            local _PrimaryPart10 = v1217.PrimaryPart

            if _IsAlive5(v1217) and _PrimaryPart10 then
                local v1219 = _LocalPlayer:DistanceFromCharacter(_PrimaryPart10.Position)

                if v1219 < v1215 then
                    v1216 = v1217
                    v1215 = v1219
                end
            end
        end

        if v1216 then
            u948 = v1216

            _attack(v1216, true, true)

            return true
        end

        task.wait(0.4)
    end)

    local u1220

    if type(u1.CustomFunctions) ~= 'function' then
        u1220 = _FireRemote5
    else
        local v1221 = u1.CustomFunctions({
            Managers = p876.Managers,
            Module = u82,
            ScriptFunctions = u877,
            Functions = {
                GetNextBoss = u966,
                AttackSegment = u1032,
                GetVolcanoRock = u1029,
                KillBossByInfo = u984,
                GetCursedDualKatanaTask = u1019,
                GetEmberTemplate = u992,
                BreakTree = u1003,
            },
        })
        local v1222, v1223, v1224 = pairs(v1221)

        u1220 = _FireRemote5

        while true do
            local v1225

            v1224, v1225 = v1222(v1223, v1224)

            if v1224 == nil then
                break
            end

            v885(v1224, v1225)
        end
    end
    if _Sea5 == 3 then
        local u1226 = 'Do you want to open the portal now?'
        local u1227 = 0
        local u1228 = {
            ['Obtained <Color=Purple><Mutant Tooth><Color=/> (1x)'] = function()
                _ItemsQuests:BeltProgress('Red', 1)
            end,
            ['<Color=Yellow><QUEST COMPLETED!><Color=/>'] = function()
                _ItemsQuests:BeltProgress('White', 8)
            end,
            ['Head back to the Dojo to complete more tasks.'] = function()
                u947 = nil
            end,
            ['Dojo quest abandoned!'] = function()
                u947 = nil
            end,
        }

        table.insert(u76, u82.Signals.Notify:Connect(function(p1229)
            local v1230 = u1228[p1229]

            if v1230 then
                return v1230()
            end
            if p1229:find('Earned <Color=Green>%$%d+<Color=/>') then
                if _LocalPlayer:GetAttribute('DangerLevel') < 100 then
                    if u45.DoughKing and VerifyTool('Sweet Chalice') or u45.CakePrince then
                        u1227 = tick() + 9000000000

                        local v1231 = u1220('CakePrinceSpawner', true) or 'Error'

                        if tick() - u1227 >= 0.25 and string.find(v1231, u1226) then
                            u1220('CakePrinceSpawner')
                        end

                        u1227 = tick()
                    end
                else
                    _ItemsQuests:BeltProgress('Yellow', 1)
                end
            end
        end))
    end
end
function u102.Webhooks(_)
    if not u82.IsCustomUrl and u82.Webhooks then
        local v1232 = {u82}

        __loadstring('{Repository}Utils/Webhooks.lua', false, v1232)
    end
end

local function v1235(p1233, ...)
    local v1234 = tick()

    u102[p1233](u102, ...)
    print(p1233, tick() - v1234)
end

v1235('Initialize')
v1235('StartFarm')
v1235('StartFunctions')
task.spawn(v1235, 'LoadLibrary')
task.spawn(v1235, 'Webhooks')
