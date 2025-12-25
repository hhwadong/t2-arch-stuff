sed -i '/exec_always --no-startup-id picom/a exec --no-startup-id dunst' ~/.config/i3/config

# 1. Hapus baris error sebelumnya dari config (biar ga duplikat)
sed -i '/bindsym XF86/d' ~/.config/i3/config

# 2. Masukkan Config yang SUDAH DIPERBAIKI (Pake sh -c)
cat <<'EOF' >> ~/.config/i3/config

# --- FIXED MEDIA KEYS & NOTIFICATIONS ---

# Volume (Pake sh -c biar command chain jalan)
bindsym XF86AudioRaiseVolume exec --no-startup-id sh -c "pamixer -i 5 && dunstify -h string:x-dunst-stack-tag:audio -h int:value:$(pamixer --get-volume) 'Volume: $(pamixer --get-volume)%'"
bindsym XF86AudioLowerVolume exec --no-startup-id sh -c "pamixer -d 5 && dunstify -h string:x-dunst-stack-tag:audio -h int:value:$(pamixer --get-volume) 'Volume: $(pamixer --get-volume)%'"
bindsym XF86AudioMute exec --no-startup-id sh -c "pamixer -t && dunstify -h string:x-dunst-stack-tag:audio 'Volume: Mute Toggle'"

# Screen Brightness
bindsym XF86MonBrightnessUp exec --no-startup-id sh -c "brightnessctl s +5% && dunstify -h string:x-dunst-stack-tag:screen -h int:value:$(brightnessctl g | awk '{print int(\$1/960*100)}') 'Brightness Up'"
bindsym XF86MonBrightnessDown exec --no-startup-id sh -c "brightnessctl s 5%- && dunstify -h string:x-dunst-stack-tag:screen 'Brightness Down'"

# Keyboard Backlight (Wildcard device)
bindsym XF86KbdBrightnessUp exec --no-startup-id sh -c "brightnessctl --device='*::kbd_backlight' s +10% && dunstify -h string:x-dunst-stack-tag:kbd 'Keyboard Light Up'"
bindsym XF86KbdBrightnessDown exec --no-startup-id sh -c "brightnessctl --device='*::kbd_backlight' s 10%- && dunstify -h string:x-dunst-stack-tag:kbd 'Keyboard Light Down'"
EOF
