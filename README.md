# Xbot_BBB
This is the code that runs on the BeagleBone Black to control a robot.

## Overview
Essentially this code establishes socket (UDP) connection with another device
(BASE) and waits for commands. The commands are either of the form of
directives or queries. An example directive is setting the PWM values of the
motors. An example query is getting IR sensor values.

## Installation
Clone the repo into home directory:

	$ cd ~
	$ git clone https://bitbucket.org/rowoflo/quickbot_bbb.git
    # or
    $ git clone https://github.com/o-botics/quickbot_bbb.git

## Running
Check IP address of BASE and ROBOT (run command on both systems and look for IP
address):

	ifconfig

Example output from BBB:

	ra0       Link encap:Ethernet  HWaddr 00:0C:43:00:14:F8
	          inet addr:192.168.1.101  Bcast:192.168.1.255  Mask:255.255.255.0
	          inet6 addr: fe80::20c:43ff:fe00:14f8/64 Scope:Link
	          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
	          RX packets:315687 errors:1113 dropped:1 overruns:0 frame:0
	          TX packets:12321 errors:0 dropped:0 overruns:0 carrier:0
	          collisions:0 txqueuelen:1000
	          RX bytes:66840454 (63.7 MiB)  TX bytes:1878384 (1.7 MiB)

Here the IP address for the robot is 192.168.1.101. Let's assume the IP address
for the BASE is 192.168.1.100.

Change into working directory:

	$ cd ~/quickbot_bbb

Quick run with given ips:

    $ python run.py -i 192.168.1.100 -r 192.168.1.101

All commands:

    $ python run.py --help
    usage: run.py [-h] [--ip IP] [--rip RIP] [--rtype RTYPE]

    optional arguments:
      -h, --help            show this help message and exit
      --ip IP, -i IP        Computer ip (base ip)
      --rip RIP, -r RIP     BBB ip (robot ip)
      --rtype RTYPE, -t RTYPE
                            Type of robot (quick|ultra)

## Command Set

* Check that the bot is up and running:
  * Command

		"$CHECK*\n"

  * Response

		"Hello from [Quick|Ultra]Bot\n"


* Get PWM values:
  * Command

		"$PWM?*\n"

  * Example response

		"[50, -50]\n"


* Set PWM values:
  * Command

		"$PWM=[-100,100]*\n"


* Get IR values:
  * Command

		"$IRVAL?*\n"

  * Example response

		"[800, 810, 820, 830, 840]\n"

* Get Ultra values:
  * Command

		"$ULTRAVAL?*\n"

  * Example response

		"[80.0, 251.0, 234.1, 12.1, 21.3]\n"

* Get encoder position:
  * Command

		"$ENVAL?*\n"

  * Example response

		"[200, -200]\n"


* Get encoder velocity (tick velocity -- 16 ticks per rotation):
  * Command

		"$ENVEL?*\n"

  * Example response

		"[20.0, -20.0]\n"


* Reset encoder position to zero:
  * Command

		"$RESET*\n"


* End program
  * Command:

 		"$END*\n"

