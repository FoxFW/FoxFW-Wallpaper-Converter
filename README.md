<img width="1727" height="921" alt="Screenshot 2026-07-08 070925" src="https://github.com/user-attachments/assets/7bb65ffa-8b15-46b1-a2be-20c8dd678265" />


# FoxFW Wallpaper Converter

A single-file, double-click PowerShell tool (packaged as a `.bat`) for converting Flipper Zero **FoxFW** custom firmware wallpapers between `.xbm` (the format the firmware uses) and `.bmp` (an easy format to edit in MS Paint or any image editor).

No installs, no dependencies beyond what's already on Windows — just download and run.

## What it does

FoxFW stores its splash-screen wallpaper as a `wallpaper.xbm` file (a 128×64 monochrome bitmap) on the Flipper's SD card. That format isn't editable in normal image editors, so this tool lets you:

- Convert `wallpaper.xbm` → `wallpaper.bmp` so you can open and edit it in MS Paint (or Photoshop, GIMP, etc.)
- Convert your edited `wallpaper.bmp` back → `wallpaper.xbm` so you can drop it back on your SD card
- Generate a fresh template `wallpaper.xbm` or `wallpaper.bmp` (with the default FoxFW logo) if you want to start from scratch
- Auto-detect a `wallpaper.xbm` sitting on a connected SD card, in addition to one in the same folder as the tool

## Requirements

- Windows with PowerShell 5.1 (this ships with every modern version of Windows — no need to install anything extra)
- That's it

## Usage

1. Download `FoxFW_Wallpaper_Converter.bat`
2. Double-click it
3. Use the on-screen menu:

   ```
   [1] File: wallpaper.xbm  FOUND  (Same Dir)
   [2] File: wallpaper.xbm  NOT FOUND (SD Card)
   [3] File: wallpaper.bmp  FOUND  (Same Dir)
   [4] Generate New wallpaper.xbm (Same Dir)
   [5] Generate New wallpaper.bmp (Same Dir)
   [6] Exit
   ```

4. Typical workflow:
   - Copy `wallpaper.xbm` off your Flipper's SD card into the same folder as the tool (or just plug in the SD card and let the tool find it)
   - Run the tool, choose the option to convert `.xbm` → `.bmp`
   - Open `wallpaper.bmp` in MS Paint, make your edits, and save (keep it **128×64** and ideally pure black/white)
   - Run the tool again, choose the option to convert `.bmp` → `.xbm`
   - Copy the new `wallpaper.xbm` back onto your SD card

## Notes on image editing

- The image must stay **exactly 128×64 pixels** — the tool will refuse to convert anything else
- The converter treats any pixel darker than mid-gray as "on" (black) and everything else as "off" (white), so pure black-and-white source images convert most predictably
- If you're designing artwork from scratch, working in black-and-white (or 1-bit) mode from the start will give the cleanest results

## How it works

The `.bat` file is a small polyglot: the top few lines are a batch script, and everything below a marker line is an embedded PowerShell script. When you run it, the batch header extracts the embedded PowerShell code to a temp file and runs it — so you only need to distribute one file, but you get the full power of PowerShell (image handling via `System.Drawing`) for the actual conversion logic.

## License

Feel free to use, modify, and share this tool for your own FoxFW projects.
