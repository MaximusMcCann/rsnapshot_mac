##Setup rsnapshot on your mac

rsnapshot will take snapshots of any folders you specify.  The default config file uses these most recent intervals:

- 48 hourly
- 15 daily
- 4 weekly 
- 5 monthly

###Overview
1. Install rsnapshot
2. Setup rsnapshot
3. Create background services
4. Run background services

Runs all services under the user (not root)


####Install rsnapshot
1. `brew install rsnapshot`

####Setup rsnapshot
1. `cp /usr/local/Cellar/rsnapshot/<VERSION>/etc/rsnapshot.conf.default /usr/local/Cellar/rsnapshot/<VERSION>/etc/rsnapshot.conf`
2. Edit the `rsnapshot.conf` file 
	1. Simple setup: copy the sample file
		1. line 23: set backup location 
			- `snapshot_root /Volumes/TimeMachine/backups # UPDATE ME` line
		2. line 127: set the `<USER>` value
		3. line 226: set what to backup starting 
			- `backup  /Users/<USER>/CODE/    localhost/ #UPDATE ME`
3. test the config file with `rsnapshot configtest`
4. fake snapshot with `rsnapshot -t hourly`
5. run your first snapshot with `rsnapshot hourly` and make sure no errors arise

####Create background services
1. copy `com.maximusmccann.rsnapshot.hourly.plist` to `/Library/LaunchAgents/`
1. copy `com.maximusmccann.rsnapshot.daily.plist` to `/Library/LaunchAgents/`
1. copy `com.maximusmccann.rsnapshot.weekly.plist` to `/Library/LaunchAgents/`
1. copy `com.maximusmccann.rsnapshot.monthly.plist` to `/Library/LaunchAgents/`

####Run background services
1. run `launchctl load com.maximusmccann.rsnapshot.hourly.plist`
2. run `launchctl load com.maximusmccann.rsnapshot.daily.plist`
3. run `launchctl load com.maximusmccann.rsnapshot.weekly.plist`
4. run `launchctl load com.maximusmccann.rsnapshot.monthly.plist`


####Other
1. To disable: `launchctl unload com.maximusmccann.rsnapshot.*.plist`


####Resources
- http://rsnapshot.org/rsnapshot/docs/docbook/rest.html
- https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html