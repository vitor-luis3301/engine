# engine
A little engine that I'm developing in c++ using lua for creating the game 
<br>example<br>
```
w = 64
h = 64

collW = w
collH = h / 2

boxW = 64
boxH = 64

groundw = 1000
groundh = 20

camera = engine.newCamera(0,0,800,600)

player = engine.newCollider("dynamic", 200, 200, collW, collH, 0, true)
block  = engine.newCollider("dynamic", 100, 200,  boxW,  boxH, 0, true)
enemy  = engine.newCollider("dynamic", 200, 100,     w,     h, 0, true)
ground = engine.newCollider("static" ,   0, 600, groundw, groundh, 0, true)

function update()
    local vx, vy = 0, 0
    local playerVel = 0.35

    if engine.isKeyDown("a") then
        vx = -playerVel
    end
    if engine.isKeyDown("s") then
        vy = playerVel
    end
    if engine.isKeyDown("d") then
        vx = playerVel
    end

    player:setLinearVel(vx, vy)

    local evx, evy = 0, 0
    local enemyVel = 0.0

    if enemy:getX() < player:getX() then
        evx = enemyVel
    end
    if enemy:getX() > player:getX() then
        evx = -enemyVel
    end
    if enemy:getY() < player:getY() then
        evy = enemyVel
    end
    if enemy:getY() > player:getY() then
        evy = -enemyVel
    end

    enemy:setLinearVel(evx, evy)

    camera:setX(player:getX() - 400)
    camera:setY(player:getY() - 300)

    if camera:getX() < 0 then camera:setX(0) end
    if camera:getY() < 0 then camera:setY(0) end
    if camera:getX() > camera:getWidth() then camera:setX(camera:getWidth()) end
    if camera:getY() > camera:getHeight() then camera:setY(camera:getHeight()) end
end

function keyUp(input) 

end

function keyDown(input) 

end

function render()
    engine.newTexture("assets/textures/terra.png", block:getX() - (boxW / 2), block:getY() - (boxH / 2), boxW, boxH, block:getAngle(), camera:getX(), camera:getY())
    engine.newTexture("assets/textures/bixo.png", player:getX() - (w / 2), player:getY() - ((collH / 2) + (h / 2)), w, h, player:getAngle(), camera:getX(), camera:getY())
    engine.newTexture("assets/textures/bixoassasino.png", enemy:getX() - (w / 2), enemy:getY() - (h / 2), w, h, enemy:getAngle(), camera:getX(), camera:getY())
    engine.newTexture("assets/textures/H2O.png", ground:getX() - (groundw / 2), ground:getY() - (groundh / 2), groundw, groundh, ground:getAngle(), camera:getX(), camera:getY())
end
```
