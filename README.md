# LESGE
## Lua Embedded Suky's Game Engine
The LPSE is a engine that uses lua and C++ to make a game.
In this version here's the features

- All key | mouse input
- Two Axis (Vertical, Horizontal)
- Compatible with png
- draw rectangles, points, and lines

## Lua Functions
- ```Init()```: this function init SDL *Returns 1 if failed*
- ```CreateWindow(title, width, height)```: this will create a SDL window *Returns 1 if failed*
- ```CreateRenderer()```: this will create the renderer of the window *Returns 1 if failed*
- ```PollEvent()```: this will execute all needed events
- ```IsAppOpen()```: this function returns a boolean to check if the window has been exited *Return boolean of if it was open the window.*
- ```Quit()```: this quit SDL, Window, and renderer
- ```ClearScreen()```: this will clear the screen and add a bg to the last color
- ```Render()```: this will show the graphics
- ```SetColor(r, g, b, a)```: set the current color
- ```DrawRect(x, y, w, h)```: this will draw a rectangle
- ```DrawRectScreen(x, y, w, h)```: this will draw a rectangle relatively to the screen
- ```GetAxis(axis: string)```: get a axis (Horizontal, Vertical) *Return a integer of the value of the axis. Ranging from -1 to 1*
- ```GetMillis()```: get all of the milliseconds that happened since the Init function *Returns the current millis since init function*
- ```DrawLine(x1, y1, x2, y2)```: Draw a line
- ```InitImage()```: Initialize SDL_Image
- ```LoadImage(file_path)```: takes a path and open a image to a texture *Returns a image class* **PNG ONLY**
- ```DrawImage(image)```: Draw a image
- ```DestroyImage(image)```: Destroy the image
- ```GetKey(key: char)```: Get the key if its pressed *return a 1 if the key is pressed*
- ```GetMouse(mouse_button)```: Get the mousebutton if its pressed *returns 1 if the button is pressed*
- ```GetMousePos()```: Get the mouse position *Returns a x and y variable*
**EXAMPLE**:
```lua
    x, y = GetMousePos()
```
- ```GetScrollY()```: Get the Y scroll from the scroll wheel *Return the direction of the scroll between -1 and 1*
- ```GetScrollX()```: Get the X scroll from the scroll wheel *Return the direction of the scroll between -1 and 1*
- ```DrawPoint()```: Draw a point
- ```DrawSpritesheet(image, x, y, width, height, imageX, imageY, spriteWidth, spriteHeight)```: this is for drawing from a spritesheet
- ```IMGUI_Begin(window_name)```: create a sub window for ImGUI
- ```IMGUI_End()```: end the sub window for ImGUI
- ```IMGUI_Text(text)```: create a text
- ```IMGUI_Button(text, width, height)```: create a button. width and height can be set to 0. *returns 1 if the button is pressed*
- ```IMGUI_Slider(text, val, minval, maxval)```: create a slider. *returns the val value. make sure to set the value variable to the function*
- ```SFX_Init()```: Initialize SFX (SDL2_mixer)
- ```SFX_Load(file_name)```: Load a sound effect. *returns a boolean to see if the file has loaded correctly and the sound object* **Example**:
```lua
    t, sound = SFX_Load("file_name.wav")
    if (t == true) then
        print("Loading \"file_name.wav\" has failed")
        return
    end
```
- ```SFX_Play(sound)```: Play the sound effect
- ```SFX_Close()```: Close SDL2_mixer. make sure to call it when the program has been closed.
## Creating a project
first copy all the files and the dlls. after create a src folder and add the lua file; this will be intrepreted. then for all image loading **DO NOT PUT IT IN THE SRC FOLDER** because the start path is where the exe is located.

## Sample Code
```lua
function main()
    if (Init() == 1) then
        print("Failed to load SDL")
        return
    end
    if (CreateWindow("Game", 1280, 720) == 1) then
        print("Create Window Failed")
        return
    end
    if (CreateRenderer() == 1) then
        print("Create Renderer Failed")
        return
    end
    if (InitImage() == 1) then
        print ("Init PNG failed")
        return
    end

    FPS = 1 / 60
    open = true
    frameTime = 0
	prevTime = 0
	currentTime = 0
	deltaTime = 0

    while open do
        prevTime = currentTime
		currentTime = GetMillis()
		deltaTime = (currentTime - prevTime) / 1000

        PollEvent()
        open = IsAppOpen()
        
        SetColor(100, 100, 100, 255)
        ClearScreen()

        frameTime = frameTime + deltaTime
        while (frameTime >= FPS) do
			frameTime = frameTime - FPS

            -- Call your updates function; called 60 time a second
		end

        -- Rendering here

        Render()
    end
end

main()
```
