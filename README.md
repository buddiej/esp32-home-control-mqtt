# esp32-home-control-mqtt
with home control mqtt it is possible to work with infrared based controls and e.g. to control a television or something similar
# OTA update
For OTA update please follow the following changes to bring it to work

link:
https://arduino.stackexchange.com/questions/75198/why-doesnt-ota-work-with-the-ai-thinker-esp32-cam-board

The boards.txt file configures what can be configured in the Arduino IDE for each board.

On my installation, this is found at C:\Users\MyUser\AppData\Local\Arduino15\packages\esp32\hardware\esp32\1.0.4\boards.txt

I found the section esp32cam.name=AI Thinker ESP32-CAM and changed the lines:

esp32cam.upload.maximum_size=3145728
esp32cam.build.partitions=huge_app
to

esp32cam.upload.maximum_size=1966080
esp32cam.build.partitions=min_spiffs
The various options are detailed in the same file with keys named esp32.menu.PartitionScheme., and for some boards these options are configurable be the user. To add this, remove (or comment out with a # character) the two lines found above so they look like:

esp32cam.upload.maximum_size=3145728
esp32cam.build.partitions=huge_app
and add the required menu selections for your application- e.g.

esp32cam.menu.PartitionScheme.huge_app=Huge APP (3MB No OTA/1MB SPIFFS)
esp32cam.menu.PartitionScheme.huge_app.build.partitions=huge_app
esp32cam.menu.PartitionScheme.huge_app.upload.maximum_size=3145728
esp32cam.menu.PartitionScheme.min_spiffs=Minimal SPIFFS (Large APPS with OTA)
esp32cam.menu.PartitionScheme.min_spiffs.build.partitions=min_spiffs
esp32cam.menu.PartitionScheme.min_spiffs.upload.maximum_size=1966080
After making any changes to boards.txt, restart the Arduino IDE for the change to take effect. Note that these changes (and any changes to the installation) may be overwritten by any future upgrades or library updates, so note your changes so they can be easily reapplied.

Alternatively, add the menu lines to boards.local.txt, introduced in Arduino 1.6.6 so they should persist during updates. In this case, no change needs to be made to boards.txt, as the boards.local.txt entries override those in boards.txt. I haven't tested this, hopefully it works across library updates and IDE upgrades.
