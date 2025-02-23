# RClone RC GUI 2 (GuiTwo pour les intimes)
This is 'rclone rc gui' forked to support rclone '--rc-baseurl' (subdir as /rclone).

It's forked from : https://github.com/retifrav/rclone-rc-web-gui

## Fork ChangeList
- Added support for URL subdirectory (rclone rcd ... --rc-baseurl <subdirectory>) :
    The subdirectory can be changed by editing the 'rcloneDir' variable in js/settings.js.

- UI Themed, and added some more informations from rclone api (RunningTime, MediumSpeed, ErrorCount, ...)
    
![rclone-rc-web-gui](/screenshot.png?raw=true)

## RClone RC WebUI behind reverse proxy   
Exemple: webui behind a reverse proxy with /rclone subdir :
    
- edit js/settings.js :

        var rcloneHost = "https://your.publicadresswebsite.com";
        var rclonePort = "443";
        var rcloneUser = "YOUR-USERNAME";
        var rclonePass = "YOUR-PASSWORD";
        var rcloneDir = "/rclone";

- Setup your reverse proxy (nginx example) :
   
         location /rclone/ {
            proxy_pass http://192.168.1.111:5572;
         }
    
- start rclone with :
   
         /usr/bin/rclone rcd --rc-web-gui --rc-web-gui-no-open-browser --rc-user=YOUR-USERNAME --rc-pass=YOUR-PASSWORD --config=/config/rclone.conf --rc-addr=:5572 --rc-serve --rc-allow-origin https://your.publicadresswebsite.com --rc-baseurl rclone --transfers 1 /config/web-ui/
    
    
