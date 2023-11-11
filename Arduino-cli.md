```bash
# easiest install method
#   install am (best appimage manager)
wget https://raw.githubusercontent.com/ivan-hc/AM-application-manager/main/INSTALL && chmod a+x ./INSTALL && sudo ./INSTALL
#   install arduino-cli
am -i arduino-cli
# add current user to group of serial communication 
sudo usermod -a -G dialout $USER
# completions
arduino-cli completion zsh > _arduino-cli
# list connected boards
arduino-cli board list
# list core modules
arduino-cli core list
# attach arduino nano old cpu to cwd sketch "."
arduino-cli board attach -p /dev/ttyUSB0 -b arduino:avr:nano:cpu=atmega328old .
# compile and upload sketch project to the attached board
arduino-cli compile -u ./project.ino
```
## Neovim setup
https://github.com/stevearc/vim-arduino