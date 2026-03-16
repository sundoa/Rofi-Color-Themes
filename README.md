# Rofi-Color-Themes
Welcome to my Rofi-Themes. They are color coded, so feel free to use any of them.
## Blue
![alt text](https://github.com/sundoa/Rofi-Color-Themes/blob/main/Blue1.png?raw=true)
## Pink
![alt text](https://github.com/sundoa/Rofi-Color-Themes/blob/main/Pink1.png?raw=true)
## Green
![alt text](https://github.com/sundoa/Rofi-Color-Themes/blob/main/Green1.png?raw=true)
## Purple-Grey
![alt text](https://github.com/sundoa/Rofi-Color-Themes/blob/main/Purple-Grey1.png?raw=true)
## Size comparision 
Here is a screenshot to compare the size of the menu with the relative screen :
![alt text](https://github.com/sundoa/Rofi-Color-Themes/blob/main/size.png?raw=true)
## Rofi wallpaper switcher
Now if you are interested in learning on how to make a wallpaper switcher through Rofi, here is a short guide -
### Stuff Needed
1. A wallpaper daemon i.e swww, hyprpaper etc.
2. A folder with all your wallpapers, preferably ~/Pictures/Wallpapers.

### Optional Stuff
1. Wallust - If you want to youse the wallpaper colors as your Rofi colors.

### How do I make it?
I will now tell you how you can make this. The script has been tested on Hyprland, so I don't know if it will work on other WMs. I have also included other things like waybar, swaync, swayosd into my script.
```bash
#!/bin/bash


cd /home/sundoa/Pictures/Wallpapers/ #Replace this with your directory

wall=$(find -type f | rofi -dmenu -p "Select Wallpaper")

[ -z "$wall" ] && exit

#Enable wallpaper (I am using swww)
swww img "$wall" --transition-type grow #Change to the transition you want

#Generate your color pallete (Copy the next few lines only if you want to)
wallust run "$wall"

#Reload waybar
killall -9 waybar
waybar

#Reload swayosd (Again, if you want to)
killall -9 swayosd
swayosd

#Swaync
killall -9 swaync
killall -9 swaync
killall -9 swaync
killall -9 swaync
killall -9 swaync

#Reload Hyprland
hyprctl reload

```
Some of the things included here may not be present in your setup.

### Using wallust to generate Rofi theme
To use wallust to generate the rofi theme, its pretty simple :

First,
```bash
nvim ~/.config/wallust/wallust.toml
```
Then, there under the "[templates]" section add
```toml
rofi.template = "colors_rofi.rasi"
rofi.target = "~/.config/rofi/config.rasi"
```
After that, exit and then
```bash
nvim ~/.config/wallust/templates/colors_rofi.rasi
```
In that, paste this 
```rasi
/*
 * color-rofi theme,
 *  by sundoa.
 *
 */

configuration {
        show-icons:   true;
        sidebar-mode: false;
}



* {
        background-color: rgba(0, 0, 0,0.75);
        text-color: {{color9}};

    	accent-color: {{color13}};
    	accent2-color: {{color14}};
    	hover-color: {{color5}};
    	urgent-color: {{color9}};
    	window-color: {{color3}};

        selected-normal-foreground: @window-color;
        normal-foreground:          @text-color;
        selected-normal-background: @hover-color;
        normal-background:          @background-color;

        selected-urgent-foreground: @background-color;
        urgent-foreground:          @text-color;
        selected-urgent-background: @urgent-color;
        urgent-background:          @background-color;

        selected-active-foreground: @window-color;
        active-foreground:          @text-color;
        selected-active-background: @hover-color;
        active-background:          @accent-color;

        alpha: 200;
}

#window {
        anchor:   center;
        location: center;
        width:    384px; 
        height:   50%;
        border-radius: 16px;
}

#mainbox {
        children: [ entry, listview];
        border-radius: 16px;
        border: 0;
}

entry {
        expand: false;
        margin: 10px;
        border-radius: 9px;
        padding: 8px 12px;
        separator-color: @background-color;
}

element {
        padding: 10px;
}

element normal.normal {
        background-color: @normal-background;
        text-color:       @normal-foreground;
        border-radius: 12px;
}

element normal.urgent {
        background-color: @urgent-background;
        text-color:       @urgent-foreground;
        border-radius: 12px;
}

element normal.active {
        background-color: @active-background;
        text-color:       @active-foreground;
        border-radius: 12px;
}

element selected.normal {
        background-color: @selected-normal-background;
        text-color:       @selected-normal-foreground;
        border:           0 4px solid 0 0;
        border-color:     @accent2-color;
        border-radius: 12px;
}

element selected.urgent {
        background-color: @selected-urgent-background;
        text-color:       @selected-urgent-foreground;
        border-radius: 12px;
}

element selected.active {
        background-color: @selected-active-background;
        text-color:       @selected-active-foreground;
        border-radius: 12px;
}

element alternate.normal {
        background-color: @normal-background;
        text-color:       @normal-foreground;
        border-radius: 12px;
}

element alternate.urgent {
        background-color: @urgent-background;
        text-color:       @urgent-foreground;
        border-radius: 12px;
}

element alternate.active {
        background-color: @active-background;
        text-color:       @active-foreground;
        border-radius: 12px;
}

button {
        padding: 8px;
}

button selected {
        background-color: @active-background;
        text-color:       @background-color;
}

/* vim: ft=css
```
Then, if you bind your wallpaper script to a keybind, say
```
bind = SUPER SHIFT, W, exec, /path/to/your/script.sh
```
Save, and then execute the shortcut, it should open a Rofi menu with your wallpapers, and if you choose one, then it will:
1. Apply the wallpaper
2. Use wallust to generate colors
3. Reload waybar
4. Reload SwayNC
5. Reload SwayOSD
6. Reload Hyprland

## Questions
Feel free to ask me any questions or issues you have. :D
