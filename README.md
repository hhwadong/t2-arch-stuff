cat <<EOF >> ~/.config/i3/config

# --- MEDIA CONTROLS (VIA SCRIPT) ---
bindsym XF86AudioRaiseVolume exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh vol_up
bindsym XF86AudioLowerVolume exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh vol_down
bindsym XF86AudioMute exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh vol_mute

bindsym XF86MonBrightnessUp exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh screen_up
bindsym XF86MonBrightnessDown exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh screen_down

bindsym XF86KbdBrightnessUp exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh kbd_up
bindsym XF86KbdBrightnessDown exec --no-startup-id ~/.config/i3/scripts/osd_handler.sh kbd_down
EOF
