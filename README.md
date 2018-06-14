slow
====

This bash script offers quick shortcuts to simulate slower network connections.  It is useful when you need to simulate a wireless network on a Linux network server, especially when you are using a virtual machine guest on your local machine or in the cloud.

    slow 3G                   # Slow network on default eth0 down to 3G wireless speeds
    slow 3G -l 600ms -p 10%   # slow network on eth0 and setup latency to 600ms packetloss to 10%
    slow reset                # Reset connection for default eth0 to normal
    slow vsat --latency=500ms # Simulate satellite internet  with a high latency
    slow dsl -b 1mbps         # Simulate DSL with a slower speed than the default
    slow modem-56k -d eth0    # Simulate a 56k modem on the eth1 device. eth0 is unchanged.

Usage
=====

    slow <network-type> [-d device] [-b bandwidth] [-l latency] [-p %drop] [-u %duplication] [-c %corruption] [-r %reordering] [-s self_reset_delay_s]
    slow reset
    slow status

Use the `-s` to  to trigger `slow reset` automatically after the timeout. Useful when experimenting with dangerous settings (such as 90% packet loss) and you want to recover the device without rebooting. Also useful for scripting into a test.

    slow edge -s 60 &
    SLOWPID=$!
    ping 8.8.8.8 -c 60
    wait $SLOWPID


Credits
=======
* v0.5 @sunapi386 implements reset after timeout; to recover device without a reboot
* v0.4 @sunapi386 implements packet duplication, corruption, reordering
* v0.3 @sunapi386 implements the active device selected by default
* v0.2 @aloysius implements packet loss
* v0.1 first version

Richard Bullington-McGuire <richard@moduscreate.com> wrote the script inspired by a UI suggestion from Mike Schwartz <mike@moduscreate.com>.

Stack Overflow and Superuser questions that helped:
* http://stackoverflow.com/questions/402377/using-getopts-in-bash-shell-script-to-get-long-and-short-command-line-options/7680682#7680682
* http://superuser.com/questions/147156/simulating-a-low-bandwidth-high-latency-network-connection-on-linux

An [Aptivate blog post](http://blog.aptivate.org/2010/01/23/make-sure-your-apps-work-in-the-field/) lent some inspiration, as did [this script](http://atmail.com/kb/2009/throttling-bandwidth/) for throttling bandwidth.

