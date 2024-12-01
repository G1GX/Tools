# Exploit Tutorial
## 1. Variable - ตัวแปร
```lua
Part = game.Workspace.Part
print(Part.Name)
```
สคริปต์นี้จะปริ้นชื่อ Part ที่มีอยู่ใน Workspace

## 1.5 if/elseif/else - เงื่อนไข
```lua
local Part = game.Workspace.Part
if Part then --ถ้าworkspaceมีPartจริงๆ
print(Part.Name)
elseif Part.Transparency == 1 then --เพิ่มเงื่อนไขถ้าPartล่องหนอยู่
Part.Transparency = 0 --ทำให้มันมองเห็นได้
else -- ถ้ามันเป็นอย่างอื่นที่ไม่ใช่Partหรือมันไม่เจอPart
print("Part Not Valid in workspace")
end

```

## 2.Teleport - วาป
```lua
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Part.CFrame
--แบบที่ 2
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Part.CFrame * CFrame.new(0, 5, 0)
```

## 3.Pcall - ป้องกัน
```lua
pcall(function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Part.CFrame * CFrame.new(0, 5, 0)
end)
```
คำอธิบาย : หากสคริปต์นี้เกิด Error มันจะไม่ส่งผลใดๆต่อสคริปต์อื่นๆ

## 4.FindFirstChild - ค้นหาอันแรก
FindFirstChild มี 2 แบบที่คนนิยมใช้กัน
1.FindFirstChild
2.FindFirstChildOfClass
```lua
game.Workspace:FindFirstChild("EZ") --ชื่อPart
game.Workspace:FindFirstChildOfClass("Part") --Classname
--Argument
game.Workspace:FindFirstChild("EZ", true) --มันจะค้นหาทุกอย่างแบบเจาะจงลึกลงไปจนกว่าจะเจอสิ่งที่มีชื่อว่า EZ ฟั่งชั่นนี้คล้ายกับการ GetDescendant
```

## 5.for _, v - ลูป
```lua
for _, v in pairs(game:GetService("Workspace")GetChildren()) do --ค้นหาแต่สิ่งที่เจออันแรก(ทั้งหมด)
if v:IsA("Part") then --ถ้า v มันคือPart หรือ เราสามารถให้ClassName หรือ Nameได้
      v:Destroy() --ทำลายPart
   end
end

for _, v in ipairs(game:GetService("Workspace")GetDescandant()) do --ค้นหาแบบเจาะลึกลงไป(ทั้งหมด)
if v:IsA("Part") then --ถ้า v มันคือPart หรือ เราสามารถให้ClassName หรือ Nameได้
      v:Destroy() --ทำลายPart
break -- หยุดการลูปหรือหยุดการทำซ้ำ
end
end
```
## 6.fireproximityprompt - การใช้งานพรอมท์แบบทันที

```lua
prompt = game.Workspace.Part:FindFirstChildOfClass("ProximityPrompt")
if prompt then
fireproximityprompt(prompt)
end

--การใช้กับทุกPrompt
for _, v in ipairs(game:GetService("Workspace"):GetSedcendants()) do
if v:IsA("Proximity") and v.Enabled == true then
fireproximityprompt(v)
end
end

```
