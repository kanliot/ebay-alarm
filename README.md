get help on update-refget help on update-refget help on update-ref# ebay-alarm
Set your alarm for any time that can be read by the date command.   Run any program on the command line. 

If `at` did what you wanted, you wouldn't be here, reading this page.    
##### Does this look easy to you?: 
`sleep 60s; mpv ~/lowbeep.ogg`    
##### What about this? 
`ebay-alarm 13:00 -c notify-send 'late for lunch?'`

##### The goal of `ebay-alarm` is to make a simple alarm-clock, that accepts a wide array of time descriptions, and works even after your pc suspends.

    Usage: ebay-alarm [options]... time string -c ALARM-COMMAND [command options and arguments]... 
    	ebay-alarm is a single script that simply watches the clock until your ALARM.
    	ebay-alarm will run any COMMAND, at any date provided by the time string.
    
    
    Here's a typical ebay-alarm example:
     $ ebay-alarm 13:00 -c notify-send 'late for lunch?'
    
    In the example above, the shell runs ebay-alarm in the foreground.
    Add a & after the command to run in the background.   If your command requires a
    terminal, ebay-alarm will not create one.  Use tmux or screen to run ebay-alarm 
    
    	ebay-alarm calls the linux date command to parse the date and time of the alarm.
    		See https://www.gnu.org/software/coreutils/manual/html_node/Examples-of-date.html
    	ebay-alarm then sleeps at intervals until that time, then runs the COMMAND and exits.
    	ebay-alarm uses a second process to monitor time zone changes and other changes in the sys time
    	ebay-alarm runs in the foreground.  use '&' to run in the background.
    	ebay-alarm does not provide a countdown, or a progress indicator.
    	ebay-alarm does not calculate seconds to sleep. It sleeps for 1-59 secs, then calls system time
    
    Program arguments must include a valid time. 
    If no command to run is given, the program simply exits at the proper time.
    The alarm command can be any length, but must follow '-c' or '--' 
    
    	-q		Quiet mode. 
    			ebay-alarm normally starts by printing the hours until the alarm.
    
    	-p 		ebay-alarm normally considers times in the past to be an error.
    			-p means the alarm should be run, even if the given time was in the past.
    
    	-c		Must not be before -q or -p 
    			Must not be before the time string
    	
    	--		Same as -c 
    
    	--time-zone 	Turns on 'time zone' awareness.   ebay-alarm will use a second
                process to monitor changes in the system time-zone.  This is an extra feature
                because other programs do not monitor time-zone changes when laptops 
                change their clocks to automatically match the time zone they have moved into.
                It's off by default because it uses more cpu when not sleeping.
    
    Five examples: 
     $ ebay-alarm now + 1 day + 1 min  -c mpv ~/'music/Clawhammer-Dogma.mp3'
     $ ebay-alarm 0:00 next day -c speak-ng 'witch hour'  # 'tomorrow' also works 
     $ ebay-alarm -q 2 sec; echo "it's two seconds later"
     $ sudo ~/bin/ebay-alarm 12am next day -- pm-suspend
     $ sudo ~/bin/ebay-alarm 2 am next day -c btrfs scrub start -B /dev/sdd
    
### Installation:
Download the ebay-alarm script and run it with Perl.    
`--time-zone` mode requires gawk (GNU awk) 
