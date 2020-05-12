
From the TCP or UDP point of view, the packet does not contain IP addresses. (IP being the layer beneath them.)

Thus, to do a proper checksum, a "pseudo header" is included. It's "pseudo", because it is not actaully part of the UDP datagram. It contains the most important parts of the IP header, that is, source and destination address, protocol number and data length.

This is to ensure that the UDP checksum takes into account these fields.
