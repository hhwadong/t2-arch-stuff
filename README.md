cat <<'EOF' > ~/.config/polybar/config.ini
; --- TOKYO NIGHT CYBER CONFIG (FULL WIDTH & RICH INFO) ---

[colors]
background = #1a1b26
background-alt = #24283b
foreground = #c0caf5
primary = #7aa2f7
secondary = #9ece6a
alert = #f7768e
warning = #e0af68
disabled = #565f89

[bar/main]
; --- DIMENSI MENTOK (FULL WIDTH) ---
width = 100%
height = 30pt
radius = 0
offset-x = 0
offset-y = 0

; Posisi modul biar rapi
fixed-center = true
bottom = false

background = ${colors.background}
foreground = ${colors.foreground}

line-size = 3pt
border-size = 0pt
border-color = #00000000

padding-left = 0
padding-right = 1
module-margin = 1

; FONT CONFIG
; Font 0: Standard Text (Size 10)
font-0 = "JetBrainsMono Nerd Font:style=Bold:size=10;2"
; Font 1: Icon Besar / Jam Besar (Size 12)
font-1 = "JetBrainsMono Nerd Font:style=Bold:size=12;3"

; --- SUSUNAN MODUL ---
modules-left = xworkspaces filesystem
modules-center = date
modules-right = wlan memory cpu backlight pulseaudio battery powermenu

cursor-click = pointer
cursor-scroll = ns-resize
enable-ipc = true

; --- MODULES ---

[module/xworkspaces]
type = internal/xworkspaces
label-active = %name%
label-active-background = ${colors.background-alt}
label-active-underline= ${colors.primary}
label-active-padding = 2
label-occupied = %name%
label-occupied-padding = 2
label-urgent = %name%
label-urgent-background = ${colors.alert}
label-urgent-padding = 2
label-empty = %name%
label-empty-foreground = ${colors.disabled}
label-empty-padding = 2

; --- JAM & TANGGAL (LEBIH LENGKAP & BESAR) ---
[module/date]
type = internal/date
interval = 1

; Format: JAM:MENIT:DETIK | HARI, TANGGAL BULAN
date = %H:%M:%S
date-alt = %A, %d %B %Y

format = <label>
format-prefix = " "
format-prefix-foreground = ${colors.primary}
format-background = ${colors.background-alt}
format-padding = 2

; Pake font-1 (Lebih besar dikit biar ga bland)
label = %date%
label-foreground = ${colors.foreground}
label-font = 2

; --- DISK INFO (STORAGE) ---
[module/filesystem]
type = internal/fs
interval = 25
mount-0 = /
format-mounted-prefix = " "
format-mounted-prefix-foreground = ${colors.primary}
label-mounted = %free%
label-unmounted = %mountpoint% not mounted
label-unmounted-foreground = ${colors.disabled}

; --- NETWORK (DENGAN SPEED) ---
[module/wlan]
type = internal/network
interface-type = wireless
interval = 1.0

; Format Connected: Icon + SSID + Download Speed
format-connected = <label-connected>
label-connected = "%{F#9ece6a}󰤨%{F-} %essid% %{F#565f89}⬇%downspeed%%{F-}"

format-disconnected = <label-disconnected>
label-disconnected = "%{F#f7768e}󰤮%{F-} Offline"

[module/pulseaudio]
type = internal/pulseaudio
format-volume = <ramp-volume> <label-volume>
label-volume = %percentage%%
label-muted = "󰝟 Muted"
label-muted-foreground = ${colors.disabled}
ramp-volume-0 = 󰕿
ramp-volume-1 = 󰖀
ramp-volume-2 = 󰕾
ramp-volume-foreground = ${colors.primary}

[module/memory]
type = internal/memory
interval = 2
format-prefix = "RAM "
format-prefix-foreground = ${colors.primary}
label = %percentage_used%%

[module/cpu]
type = internal/cpu
interval = 2
format-prefix = "CPU "
format-prefix-foreground = ${colors.primary}
label = %percentage%%

[module/battery]
type = internal/battery
full-at = 99
low-at = 15
battery = BAT0
adapter = ADP1
poll-interval = 5

format-charging = <animation-charging> <label-charging>
format-discharging = <ramp-capacity> <label-discharging>
label-charging = %percentage%%
label-discharging = %percentage%%
label-full = "󰁹 Full"
label-low = "󰂃 LOW"

ramp-capacity-0 = 󰁺
ramp-capacity-1 = 󰁼
ramp-capacity-2 = 󰁾
ramp-capacity-3 = 󰂀
ramp-capacity-4 = 󰁹
ramp-capacity-foreground = ${colors.primary}

animation-charging-0 = 󰢜
animation-charging-1 = 󰂆
animation-charging-2 = 󰂇
animation-charging-3 = 󰂈
animation-charging-4 = 󰢝
animation-charging-foreground = ${colors.secondary}
animation-charging-framerate = 750

[module/backlight]
type = internal/backlight
card = intel_backlight
use-ui-max = true
format = <ramp-screen> <label>
label = %percentage%%
ramp-screen-0 = 󰃞
ramp-screen-1 = 󰃝
ramp-screen-2 = 󰃟
ramp-screen-3 = 󰃠
ramp-screen-foreground = ${colors.warning}

[module/powermenu]
type = custom/menu
expand-right = true
format-spacing = 1
label-open = ""
label-open-foreground = ${colors.alert}
label-close = ""
label-close-foreground = ${colors.primary}
label-separator = |
label-separator-foreground = ${colors.disabled}

menu-0-0 = "Reboot"
menu-0-0-exec = reboot
menu-0-1 = "Power Off"
menu-0-1-exec = poweroff

[settings]
screenchange-reload = true
pseudo-transparency = true
EOF
