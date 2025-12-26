cat <<'EOF' >> ~/.config/i3/config

# --- MEDIA & OSD (INLINE & CLEAN) ---

# VOLUME (Pamixer)
bindsym XF86AudioRaiseVolume exec --no-startup-id sh -c 'pamixer -i 5 && dunstify -h string:x-dunst-stack-tag:audio -h int:value:$(pamixer --get-volume) "VOL: $(pamixer --get-volume)%"'
bindsym XF86AudioLowerVolume exec --no-startup-id sh -c 'pamixer -d 5 && dunstify -h string:x-dunst-stack-tag:audio -h int:value:$(pamixer --get-volume) "VOL: $(pamixer --get-volume)%"'
bindsym XF86AudioMute exec --no-startup-id sh -c 'pamixer -t && dunstify -h string:x-dunst-stack-tag:audio "MUTED"'

# SCREEN BRIGHTNESS (Cut command buat ambil angka bersih)
bindsym XF86MonBrightnessUp exec --no-startup-id sh -c 'brightnessctl -c backlight set +5% && dunstify -h string:x-dunst-stack-tag:screen -h int:value:$(brightnessctl -c backlight -m | cut -d, -f4 | tr -d %) "BRIGHTNESS: $(brightnessctl -c backlight -m | cut -d, -f4)"'
bindsym XF86MonBrightnessDown exec --no-startup-id sh -c 'brightnessctl -c backlight set 5%- && dunstify -h string:x-dunst-stack-tag:screen -h int:value:$(brightnessctl -c backlight -m | cut -d, -f4 | tr -d %) "BRIGHTNESS: $(brightnessctl -c backlight -m | cut -d, -f4)"'

# KEYBOARD BACKLIGHT (Pake device *kbd_backlight)
bindsym XF86KbdBrightnessUp exec --no-startup-id sh -c 'brightnessctl --device="*kbd_backlight" set +10% && dunstify -h string:x-dunst-stack-tag:kbd -h int:value:$(brightnessctl --device="*kbd_backlight" -m | cut -d, -f4 | tr -d %) "KBD: $(brightnessctl --device="*kbd_backlight" -m | cut -d, -f4)"'
bindsym XF86KbdBrightnessDown exec --no-startup-id sh -c 'brightnessctl --device="*kbd_backlight" set 10%- && dunstify -h string:x-dunst-stack-tag:kbd -h int:value:$(brightnessctl --device="*kbd_backlight" -m | cut -d, -f4 | tr -d %) "KBD: $(brightnessctl --device="*kbd_backlight" -m | cut -d, -f4)"'
EOF
