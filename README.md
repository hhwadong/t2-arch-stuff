cat <<EOF > ~/.config/polybar/launch.sh
#!/bin/bash

# 1. Matikan Polybar dengan paksa (SIGKILL)
killall -9 polybar

# 2. Tunggu sampai beneran mati (Double Check)
while pgrep -u \$UID -x polybar >/dev/null; do sleep 1; done

# 3. Jalankan Polybar baru
# (Kasih delay dikit 0.5 detik biar i3 siap dulu)
sleep 0.5
polybar main 2>&1 | tee -a /tmp/polybar.log & disown

echo "Polybar launched..."
EOF

chmod +x ~/.config/polybar/launch.sh
