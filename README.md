slow
====

This bash script offers quick shortcuts to simulate slower network connections.  It is useful when you need to simulate a wireless network on a Linux network server, especially when you are using a virtual machine guest on your local machine or in the cloud.

    slow 3G                   # Slow network on default eth0 down to 3G wireless speeds
    slow reset                # Reset connection for default eth0 to normal
    slow vsat --latency=500ms # Simulate satellite internet  with a high latency
    slow dsl -b 1mbps         # Simulate DSL with a slower speed than the default
    slow modem-56k -d eth1    # Simulate a 56k modem on the eth1 device. eth0 is unchanged.

If you assign more than one network interface to a virtual guest, you could run slow on one of the interfaces, so that it you can switch between fast and slow connections by switching the IP address endpoint.

Slow requires Linux and the 'tc' suite of traffic control tools.

Credits
=======
Richard Bullington-McGuire <richard@moduscreate.com> wrote the script inspired by a UI suggestion from Mike Schwartz <mike@moduscreate.com>.

Stack Overflow and Superuser questions that helped:
* http://stackoverflow.com/questions/402377/using-getopts-in-bash-shell-script-to-get-long-and-short-command-line-options/7680682#7680682
* http://superuser.com/questions/147156/simulating-a-low-bandwidth-high-latency-network-connection-on-linux

An [Aptivate blog post](http://blog.aptivate.org/2010/01/23/make-sure-your-apps-work-in-the-field/) lent some inspiration, as did [this script](http://atmail.com/kb/2009/throttling-bandwidth/) for throttling bandwidth. 

Future Development
==================

It would be nice to expand the options that this took more options, such as adjusting for random fluctuations in speed, packet reordering, and packet dropping. Reading up on the [Linux Advanced Routing and Traffic Control HOWTO](http://www.lartc.org/lartc.html) should provide food for thought.
