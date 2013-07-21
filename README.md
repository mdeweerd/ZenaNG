ZenaNG Linux - a command line utility to interact with the Microchip
Technologies ZENA 2.5GHz 802.15.4 packet sniffer.
This tool support both bersion sniffer
* Old hardware based on CC2420 chip.
* Next gen hardware based on MRF24J40 chip 

This project is based on Zena Linux project hosted at
http://code.google.com/p/microchip-zena/

Special thanks to Joshua Wright who did much of the initial reverse 
engineering work on the Microchip ZENA. See this post for details:
http://www.willhackforsushi.com/?p=198

Special thanks to Joe Desbonnet for the first versions of this nice tool
Related post:
http://jdesbonnet.blogspot.co.uk/2011/02/using-microchip-zena-zigbee802154.html

Zena - Version 0.1 (16 Feb 2011)
First release. Used libusb 0.1.

Zena - Version 0.2 (19 Feb 2011) 
Identical in functionality to verion 0.1 except that it
uses libusb version 1.0 API (the previous version used libusb v0.1). 

Zena - Version 0.3 (25 Feb 2011)  (CVS file version 1.52)
* Add 802.15.4 channel to usbhex records as the second item in the
record after the packet timestamp (in hex). This ensure that all
packet data and metadata (reception, channel, timestamp) is
recorded. 
* If ZENA is bound to a kernel driver, it will attempt to detach
it from the kernel driver. Up do now this had to be done manually
prior to running this utility.
* Use host timestamp in pcap file instead of ZENA timestamp.
* -s <t> switch to scan through 802.15.4 channels, where t = channel
time slice in ms.

Zena - Version 0.4 (1 Mar 2011)  (CVS file version 1.61)
* Add signal handler for graceful exit.
* Buffer entire 802.15.4 packet and check if suitable for outputting
to pcap file. Drop corrupted packets by default. Use -b to override.
* Use -q to suppress warning messages.
 *
Zena - Version 0.4.1 (20 Mar 2011) (CVS file version 1.63)
* Remove call to zena_get_packet() just before the output format switch
statement in the main loop. This was unnecessary and would have resulted
in lost packets.

Zena - Version 0.4.2 (2 Feb 2012) (CVS file version 1.68)
Change way packets with bad FCS are handled when writing PCAP. There was 
bug where the packet written to the PCAP file was two bytes shorter than 
that declared in the header when FCS was bad and 'drop bad packets' flag
was disabled.

Zena - Version 0.4.3 (16 Feb 2012) (CVS file version 1.70)
Check zena_packet.packet_len is a sane value. Occasionally getting crazy
lengths which causes SEGV when accessing the zena_packet.packet[] buffer.

ZenaNG - Version 0.5.0 (21 Jul 2013)
Next hardware generation (based on MRF24J40 chip) support

TODO: 
* Option to use ZENA or host timestamp 

Requires libusb-1.0 (to run) and libusb-1.0-dev (to compile) packages. 

Known issue: can cause Ubuntu 10.x running Linux 2.6.32-* to kernel crash! 
Cause unknown. A fresh Ubuntu 10.10 installed from CD running 2.6.35-22 
does not seem to have this problem. Suggest running in a virtual machine.