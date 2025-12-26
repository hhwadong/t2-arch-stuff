mkdir -p ~/.config/i3/scripts
cat <<'EOF' > ~/.config/i3/scripts/osd_handler.sh
#!/bin/bash

# --- SETTINGAN HARDCODE ---
KBD_DEVICE=":white:kbd_backlight"
SCREEN_DEVICE="intel_backlight"

# Function Kirim Notif (Ada Persen)
send_notif() {
    # $1=Tag, $2=Value, $3=Title
    dunstify -h string:x-dunst-stack-tag:$1 -h int:value:$2 "$3: $2%" -t 1500
}

case $1 in
    # VOLUME
    vol_up) pamixer -i 5; val=$(pamixer --get-volume); send_notif "audio" "$val" "Volume" ;;
    vol_down) pamixer -d 5; val=$(pamixer --get-volume); send_notif "audio" "$val" "Volume" ;;
    vol_mute) pamixer -t; dunstify -h string:x-dunst-stack-tag:audio "Muted" -t 1500 ;;

    # SCREEN (Fix Brightness %)
    screen_up) 
        brightnessctl -c backlight set +5%
        val=$(brightnessctl -c backlight -m | cut -d, -f4 | tr -d %)
        send_notif "screen" "$val" "Brightness" 
        ;;
    screen_down) 
        brightnessctl -c backlight set 5%-
        val=$(brightnessctl -c backlight -m | cut -d, -f4 | tr -d %)
        send_notif "screen" "$val" "Brightness" 
        ;;

    # KEYBOARD (HARDCODED :white:kbd_backlight)
    kbd_up) 
        brightnessctl -d "$KBD_DEVICE" set +10%
        val=$(brightnessctl -d "$KBD_DEVICE" -m | cut -d, -f4 | tr -d %)
        send_notif "kbd" "$val" "Keyboard" 
        ;;
    kbd_down) 
        brightnessctl -d "$KBD_DEVICE" set 10%-
        val=$(brightnessctl -d "$KBD_DEVICE" -m | cut -d, -f4 | tr -d %)
        send_notif "kbd" "$val" "Keyboard" 
        ;;
esac
EOF




sed -i '/bindsym XF86/d' ~/.config/i3/config



# --- MEDIA & OSD (CLEAN & WORKING) ---
bindsym XF86AudioRaiseVolume exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh vol_up
bindsym XF86AudioLowerVolume exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh vol_down
bindsym XF86AudioMute exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh vol_mute

bindsym XF86MonBrightnessUp exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh screen_up
bindsym XF86MonBrightnessDown exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh screen_down

bindsym XF86KbdBrightnessUp exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh kbd_up
bindsym XF86KbdBrightnessDown exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh kbd_down

