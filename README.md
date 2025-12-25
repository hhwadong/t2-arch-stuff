cat <<EOF > ~/.config/kitty/kitty.conf
# --- KITTY TOKYO NIGHT STORM ---

font_family      JetBrainsMono Nerd Font
bold_font        auto
italic_font      auto
bold_italic_font auto
font_size 11.0

# BACKGROUND ABU-ABU (STORM)
background #24283b
foreground #c0caf5

# SETTING WINDOW
window_padding_width 10
background_opacity 0.95
hide_window_decorations yes

# CURSOR
cursor #c0caf5
cursor_text_color #1a1b26

# WARNA PALETTE (TOKYO NIGHT)
color0  #1d202f
color1  #f7768e
color2  #9ece6a
color3  #e0af68
color4  #7aa2f7
color5  #bb9af7
color6  #7dcfff
color7  #a9b1d6

color8  #414868
color9  #f7768e
color10 #9ece6a
color11 #e0af68
color12 #7aa2f7
color13 #bb9af7
color14 #7dcfff
color15 #c0caf5
EOF






mkdir -p ~/.config/dunst
cat <<EOF > ~/.config/dunst/dunstrc
[global]
    width = 300
    height = 60
    origin = bottom-center
    offset = 10x50
    scale = 0
    notification_limit = 3

    # TAMPILAN
    font = JetBrainsMono Nerd Font 10
    frame_width = 2
    frame_color = "#7aa2f7"
    corner_radius = 10
    separator_color = frame
    padding = 10
    horizontal_padding = 10
    text_icon_padding = 0
    icon_position = left

    # FORMAT
    format = "<b>%s</b>\n%b"
    markup = full
    show_age_threshold = 60
    word_wrap = yes
    ignore_newline = no
    stack_duplicates = true
    hide_duplicate_count = false

[urgency_low]
    background = "#1a1b26"
    foreground = "#c0caf5"
    timeout = 4

[urgency_normal]
    background = "#24283b"
    foreground = "#c0caf5"
    timeout = 4

[urgency_critical]
    background = "#f7768e"
    foreground = "#1a1b26"
    frame_color = "#ff0000"
    timeout = 0
EOF



cat <<'EOF' >> ~/.config/i3/config

# --- OSD NOTIFICATIONS & KEYBOARD BACKLIGHT ---

# 1. VOLUME (Pake pamixer + Dunstify)
# Tag 'audio' biar notifnya ga numpuk banyak, tapi replace yang lama
bindsym XF86AudioRaiseVolume exec "pamixer -i 5; dunstify -h string:x-dunst-stack-tag:audio -h int:value:$(pamixer --get-volume) 'Volume: $(pamixer --get-volume)%'"
bindsym XF86AudioLowerVolume exec "pamixer -d 5; dunstify -h string:x-dunst-stack-tag:audio -h int:value:$(pamixer --get-volume) 'Volume: $(pamixer --get-volume)%'"
bindsym XF86AudioMute exec "pamixer -t; dunstify -h string:x-dunst-stack-tag:audio 'Volume: Mute Toggle'"

# 2. SCREEN BRIGHTNESS (Pake brightnessctl + Dunstify)
bindsym XF86MonBrightnessUp exec "brightnessctl s +5%; dunstify -h string:x-dunst-stack-tag:screen 'Brightness: Up'"
bindsym XF86MonBrightnessDown exec "brightnessctl s 5%-; dunstify -h string:x-dunst-stack-tag:screen 'Brightness: Down'"

# 3. KEYBOARD BACKLIGHT (MacBook)
# Device biasanya namanya '*kbd_backlight'
bindsym XF86KbdBrightnessUp exec "brightnessctl --device='*::kbd_backlight' s +10%; dunstify -h string:x-dunst-stack-tag:kbd 'Keyboard Light: Up'"
bindsym XF86KbdBrightnessDown exec "brightnessctl --device='*::kbd_backlight' s 10%-; dunstify -h string:x-dunst-stack-tag:kbd 'Keyboard Light: Down'"
EOF


