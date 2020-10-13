[How to test the SPI bus]

(1) Check whether the devices are successfully installed in /dev:

root@s5p6818-bitminer-ref:~# ls -al /dev/spi*
crw-------    1 root     root      153,   0 Oct 13 01:27 /dev/spidev0.0
crw-------    1 root     root      153,   1 Oct 13 01:27 /dev/spidev2.0

(2) Run spidevtest
The default device is /dev/spidev1.1. Select the correct device to use.

root@s5p6818-bitminer-ref:~# spidevtest -D /dev/spidev0.0 -v
spi mode:  0x0
bits per word: 8
max speed: 500000 Hz (500 KHz)
TX | FF FF FF FF FF FF 40 00 00 00 00 95 FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0 0D  |
RX | FF FF FF FF FF FF 40 00 00 00 00 95 FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0 0D  |
root@s5p6818-bitminer-ref:~# spidevtest -D /dev/spidev2.0 -v
spi mode:  0x0
bits per word: 8
max speed: 500000 Hz (500 KHz)
TX | FF FF FF FF FF FF 40 00 00 00 00 95 FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0 0D  |
RX | FF FF FF FF FF FF 40 00 00 00 00 95 FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0 0D  |

[Trouble Shooting]

If the received data is all zero as below, it implies the pins MOSI and MISO are not connected.

root@s5p6818-bitminer-ref:~# spidevtest -D /dev/spidev0.0 -v
spi mode:  0x0
bits per word: 8
max speed: 500000 Hz (500 KHz)
TX | FF FF FF FF FF FF 40 00 00 00 00 95 FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0 0D  |
RX | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |
root@s5p6818-bitminer-ref:~# spidevtest -D /dev/spidev2.0 -v
spi mode:  0x0
bits per word: 8
max speed: 500000 Hz (500 KHz)
TX | FF FF FF FF FF FF 40 00 00 00 00 95 FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0 0D  |
RX | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |

