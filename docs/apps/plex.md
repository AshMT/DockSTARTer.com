### Plex is telling me to login and then not directing me to the server I just set up, why?
Upon starting up Plex for the first time, it's very likely you'll need to follow these steps:

Edit `~/.docker/compose/.env` and set `PLEX_NETWORK_MODE=host`. After claiming your server set `PLEX_NETWORK_MODE=` (back to blank).

### After installing Plex through DockSTARTer and banging your head on the table because you keep getting the error "Plex server not found". Run the following commands. (Remove {})
```
docker exec -it {Docker Container Name} /bin/bash

wget https://github.com/uglymagoo/plex-claim-server/raw/master/plex-claim-server.sh

curl -L -o plex-claim-server.sh https://github.com/uglymagoo/plex-claim-server/raw/master/plex-claim-server.sh

chmod +x plex-claim-server.sh

./plex-claim-server.sh "{Plex Claim Code}"            ### plex.tv/claim (Requires the "") ###

chown {username}:{username} "/config/Library/Application Support/Plex Media Server/Preferences.xml" 
###{Username} most likely root###

exit
```

Then restart container.

### Everything's gone to crap, and I need to re-make my server. What do I do?
Thankfully, some of this information is well documented (but not easily found) over on Plex's website here!
1. Moving an installation to another system: [https://support.plex.tv/articles/201370363-move-an-install-to-another-system/](https://support.plex.tv/articles/201370363-move-an-install-to-another-system/)
2. Where is the Plex Media Server data directory? [https://support.plex.tv/articles/202915258-where-is-the-plex-media-server-data-directory-located/](https://support.plex.tv/articles/202915258-where-is-the-plex-media-server-data-directory-located/)

If you would like to have Plex use a GPU that is attached to your DockSTARTer host, you can do this using an override like so:
```
devices:
     - /dev/dri:/dev/dri
```
Refer to this forum post for details: [Using Hardware Acceleration in Docker](https://forums.plex.tv/t/using-hardware-acceleration-in-docker/229702/3)
