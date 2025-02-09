# Vesktop2Vulkan
Vesktop, being a Chromium-based Discord client, **doesn’t let you tweak GPU settings easily**, but you can **force-enable Vulkan or SkiaGraphite** with a simple batch script.

This guide will walk you through:  
✅ Creating two batch scripts (one for **Vulkan**, one for **SkiaGraphite**).  
✅ **Disabling Direct Rendering Display Compositor & Raw Draw** (they break rendering).  
✅ Stopping **Vesktop from launching on startup** and replacing it with your custom batch script.  
✅ Setting up a **desktop shortcut with an icon**.

# Step 1: Create the Batch Script

There are **two versions** of this script—one optimized for **Vulkan**, and one for **SkiaGraphite**.

# 🟢 Vulkan Version

    u/echo off
    taskkill /F /IM Vesktop.exe
    timeout /t 2 /nobreak >nul
    
    start "" "%LOCALAPPDATA%\vesktop\Vesktop.exe" ^
    --enable-features=Vulkan,WebGPU,WebNN,AcceleratedVideoDecodeLinuxGL,AcceleratedVideoEncoder,AcceleratedVideoDecoder,AcceleratedVideoDecodeLinuxZeroCopyGL ^
    --use-vulkan ^
    --enable-vulkan ^
    --disable-software-rasterizer ^
    --allow-file-access-from-files ^
    --disable-renderer-backgrounding ^
    --disable-background-timer-throttling ^
    --disable-backgrounding-occluded-windows ^
    --autoplay-policy=no-user-gesture-required ^
    --enable-speech-dispatcher ^
    --disable-features=DirectRenderingDisplayCompositor,RawDraw,CalculateNativeWinOcclusion,WinRetrieveSuggestionsOnlyOnDemand,HardwareMediaKeyHandling,MediaSessionService

✅ **Forces Vulkan rendering**  
✅ **Disables known rendering issues**

# 🔵 SkiaGraphite Version

    u/echo off
    taskkill /F /IM Vesktop.exe
    timeout /t 2 /nobreak >nul
    
    start "" "%LOCALAPPDATA%\vesktop\Vesktop.exe" ^
    --enable-features=SkiaGraphite,WebGPU,WebNN,AcceleratedVideoDecodeLinuxGL,AcceleratedVideoEncoder,AcceleratedVideoDecoder,AcceleratedVideoDecodeLinuxZeroCopyGL ^
    --disable-software-rasterizer ^
    --allow-file-access-from-files ^
    --disable-renderer-backgrounding ^
    --disable-background-timer-throttling ^
    --disable-backgrounding-occluded-windows ^
    --autoplay-policy=no-user-gesture-required ^
    --enable-speech-dispatcher ^
    --disable-features=DirectRenderingDisplayCompositor,RawDraw,CalculateNativeWinOcclusion,WinRetrieveSuggestionsOnlyOnDemand,HardwareMediaKeyHandling,MediaSessionService

✅ **Forces SkiaGraphite rendering**  
✅ **Disables broken compositor features**

# Step 2: Save the File

1. Open **Notepad**.
2. Copy **one of the scripts** above.
3. Click **File > Save As**.
4. Change **Save as type: All Files**.
5. Name it something like:
   * `Launch_Vesktop_Vulkan.bat`
   * `Launch_Vesktop_SkiaGraphite.bat`
6. Save it somewhere convenient, like **Desktop** or **Documents**.

# Step 3: Disable Vesktop from Auto-Starting

1. Press `Ctrl + Shift + Esc` to open **Task Manager**.
2. Go to the **Startup** tab.
3. Find **Vesktop** and **Disable** it.

This stops Vesktop from launching normally so we can **force it to use the optimized batch script instead**.

# Step 4: Auto-Start Vesktop with the Custom Script

To make sure **Vesktop always launches with Vulkan or SkiaGraphite on boot**, do this:

1. Press `Win + R`, type:and hit **Enter**.shell:startup
2. Copy your **batch file** into this folder.
3. Now, every time Windows starts, **Vesktop will launch with the optimized settings**.

# Step 5: Create a Desktop Shortcut

For easy access, make a **shortcut to the batch script**:

1. **Right-click** your `.bat` file > **Create Shortcut**.
2. Move the shortcut to your **Desktop**.
3. **Right-click > Properties** on the shortcut.
4. Click **Change Icon** \> Pick a custom `.ico` file (optional, but makes it look clean).
5. Hit **OK > Apply**.

Now, you have a **one-click launcher** that **kills Vesktop if it's already running** and restarts it with your **custom settings**.

# Final Notes

* If **Vulkan breaks rendering**, switch to the **SkiaGraphite version**.

That’s it! Enjoy your **fully optimized Vesktop** with better performance. 🚀💨
