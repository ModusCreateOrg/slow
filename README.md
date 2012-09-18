slow
====

This bash script offers quick shortcuts to simulate slower network connections.  It is useful when you need to simulate a wireless network on a Linux network server, especially when you are using a virtual machine guest on your local machine or in the cloud.

    slow 3G                   # Slow network on default eth0 down to 3G wireless speeds
    slow reset                # Reset connection
    slow vsat --latency=500ms # Simulate satellite internet  with a high latency
    slow dsl -b 1mbps         # Simulate DSL with a slower speed than the default
    slow modem-56k -d eth0    # Simulate a 56k modem on the eth1 device. eth0 is unchanged.


