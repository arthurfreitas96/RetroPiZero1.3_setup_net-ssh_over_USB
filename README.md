# RetroPiZero1.3_overclock_setup_net-ssh_over_USB

I recently bought a Raspberry Pi Zero 1.3 and flashed a RetroPie 4.6 image to it's SD card. Testing some emulators using the stock settings, I noticed some expected issues. For example, testing snes9x_2002 (standard emulator for SNES on RPI Zero), I noticed that SuperFX games ran poorly. Some of the other more graphics demanding games, such as Donkey Kong Country 3, suffered with major fps drops and poor audio.

To solve this problem I followed this conservative overclock setup: https://www.reddit.com/r/RetroPie/comments/bs0a0i/snes_performance_benchmarks_on_pi_zero_and_how_to/. According to the link, with the recommended settings, you can achieve a increase of 30% in the RPi performance emulating SNES.

Then I wanted to install an optional SNES emulator to it, PiSnes, which was developed to run in the RPi Zero. However, since there's no built-in wifi in this board, I had no connection to the Internet. Solving this second problem required following the instructions presented on this link: https://www.slideshare.net/GSHCO/raspberry-zero-usb-in-linux (attention: remember to change the interface names of the commands presented on the slide #15 by your interface names). That way, you can connect the RPi Zero to your Linux PC using only a USB cable, access it via SSH and you can share Internet from your PC to the RPi Zero using only the instructions presented. To access RetroPie with SSH you can run the command 'ssh pi@retropie.local'.

To autoconnect to my RPi every time i plugged it in my PC. I edited the PC's /etc/network/interfaces file and included script to bind a static ip to the interface, enps020u3 in my case. So I included the following lines at the end of the file:

auto enp0s20u3
iface enp0s20u3 inet static
        address 192.168.7.1
        netmask 255.255.255.0
        network 192.168.7.0
        broadcast 192.168.7.255
        gateway 192.168.7.1


After some research, I found out that lr-gpsp is broken on RetroPie 4.6, but there is a known work around that requires replacing the gpsp_libretro.so with the previous version of the core (4.5), according to the user juchong in https://retropie.org.uk/forum/topic/25111/lr-gpsp-giving-illegal-instruction-on-raspberry-pi-models-0w-3b-and-4/22. Following this method didn't solve my problem and I couldn't make lr-gpsp to work on RetroPie 4.6, so I downgraded to 4.5.1, but kept my overclocking configuration. Now I have gba at full speed in all games i tested until now, with nice sound too, using lr-gpsp.
