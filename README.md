slow
====

This bash script offers quick shortcuts to simulate slower network connections.  It is useful when you need to simulate a wireless network on a Linux network server, especially when you are using a virtual machine guest on your local machine or in the cloud.

    slow 3G                   # Slow network on default eth0 down to 3G wireless speeds
    slow reset                # Reset connection for default eth0 to normal
    slow vsat                 # Simulate satellite internet  with a high latency
    slow dsl -b 1mbps         # Simulate DSL with a slower speed than the default
    slow modem-56k -d eth1    # Simulate a 56k modem on the eth1 device. eth0 is unchanged.
    slow -b 100000 -l 100ms   # Simulate network with a 100k bandwidth and 100ms latency
    slow T1 -p 0.1%           # Simulate T1 line with 1 in 1000 packet loss
    slow T3 -c 0.1%           # Simulate T3 line with 1 in 1000 packet corruption

If you assign more than one network interface to a virtual guest, you could run slow on one of the interfaces, so that it you can switch between fast and slow connections by switching the IP address endpoint.

Slow requires Linux and the 'tc' suite of traffic control tools.

See the [Cisco Global Cloud Index Supplement](http://www.cisco.com/c/en/us/solutions/collateral/service-provider/global-cloud-index-gci/CloudIndex_Supplement.html) for statistics on bandwidth and latency for countries all over the world.

Usage
=====

The available built-in targets simulate many common network scenarios. They start out
without assuming clear transmissions without extra delays, corruptions, or duplications.


Target                  | Description
------------------------|-------------------------------------------------
AMPS                    | 1G cell phone data
EDGE / 2.5G / GPRS          | 2G cell phone data
3G                      | 3G cell phone data
4G                      | 4G cell phone data
modem-0.1k / modem-110    | 110 baud modem, circa 1970s
modem-0.3k/ modem-300    | 300 baud modem, circa 1970s
modem-1.2k / modem-1200   | 1200 baud modem, circa 1980s
modem-2.4k/ modem-2400   | 2400 baud modem, circa 1980s
modem-9.6k / modem-9600   | 9600 baud modem, circa 1980s
modem-14.4k / modem-14400 | 14.4k modem, circa 1990s
modem-28.8k / modem-28800 | 28.8k modem, circa 1990s
modem-56k / modem-56000   | 56k modem, circa 2000
56k                     | 56k leased line (low latency)
T1 / t1                   | T1 line (1500Mbps, low latency)
T3 / t3                   | T3 line (45Mbps, low latency)
DSL / dsl                 | Consumer DSL
cablemodem              | Consumer cable modem
wifi-a / wifi-g           | 45Mbps WIFI
wifi-b                  | 11Mbps WIFI
wifi-n                  | 150Mbps WIFI
vsat                    | 5Mbps, high latency satellite terminal

By adding extra command line parameters you can tweak the behavior of the
network interface further, adding precise bandwidth and latency tweaks, or
add packet loss or corruption.

Parameter          |  Description
-------------------|---------------------------------------------------
-h / --help       |  Get help. Default behavior if no parameters given.
-v / --version    |  Version info
-d / --device     |  Set device name
-b / --bandwidth  |  Bandwidth, use bytes, kbps, mbps
-l / --latency    |  Latency, in ms, e.g. "20ms"
-p / --packetloss |  Packet loss in percent, e.g. "0.3%"
-c / --corruption |  Corrupt random bits, in percent, e.g. "0.01%"
-q / --quiet      |  Make output quiet

Testing
=======
This project is set up with [Vagrant](http://www.vagrantup.com/) to make it convenient
to test, even if you are not running Linux as your host operating system. 

Install Vagrant and [Virtualbox](http://www.virtualbox.org/) and issue the command `vagrant up` and then you can experiment with the different commands, for example:

    vagrant up
    vagrant ssh 
    # wait for vagrant prompt 
    sudo /vagrant/slow 56k

Credits
=======
Richard Bullington-McGuire <richard@moduscreate.com> wrote the script inspired by a UI suggestion from Mike Schwartz <mike@moduscreate.com>. [Tyler Knappe](https://github.com/knappe) and [Adrian Silva](https://github.com/skiold) helped clean up the script.

Stack Overflow and Superuser questions that helped:
* http://stackoverflow.com/questions/402377/using-getopts-in-bash-shell-script-to-get-long-and-short-command-line-options/7680682#7680682
* http://superuser.com/questions/147156/simulating-a-low-bandwidth-high-latency-network-connection-on-linux

An [Aptivate blog post](https://web.archive.org/web/20111129155657/http://blog.aptivate.org/2010/01/23/make-sure-your-apps-work-in-the-field) lent some inspiration, as did [this script](https://web.archive.org/web/20130928002236/http://atmail.com/kb/2009/throttling-bandwidth) for throttling bandwidth.

Future Development
==================

It would be nice to expand the options that this took more options, such as adjusting for random fluctuations in speed, packet reordering, and smarter packet dropping. Reading up on the [Linux Advanced Routing and Traffic Control HOWTO](http://www.lartc.org/lartc.html) should provide food for thought.
