# Power management
```bash
# install power-profiles-daemon(used by gnome) and powertop
yay -S powertop power-profiles-daemon
sudo systemctl enable --now power-profiles-daemon.service
# auto tune power management stuff
sudo powertop --auto-tune
# get current profile
powerprofilectl get
# list profiles
powerprofilectl list
# set a profile
powerprofilectl set power-saver
```