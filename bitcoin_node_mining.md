To learning  about working of bitcoin follow these instruction targetted to rpi based board. Install the lean server headless version to avoid unnessessary packages.
- Setup the [node, wallet like Sparrow](https://raspibolt.org/) software etc.

  To mine bitcoin one need order of TH/s. With RPI you can expect up 15 MH/s but can be intresting to learn about mining
  Can use [BFGminor](https://github.com/luke-jr/bfgminer)
  Basic quick steps
  - git clone  https://github.com/luke-jr/bfgminer.git
  - sudo apt-get update
  - sudo apt install 	build-essential autoconf automake libtool pkg-config yasm libcurl4-gnutls-dev libjansson-dev uthash-dev libncursesw5-dev libudev-dev libusb-1.0-0-dev libevent-dev libmicrohttpd-dev libhidapi-dev
  - autogen.sh
  - ./configure --enable-cpumining
  - make
 
    if minor is on different rpi board use following commands to start
    ./bfgminer --url=http://ip or hostname:8332 --userpass=rpcuser:rpcname --generate-to=address to receive btc

    Setup proper firewall rule(using **ufw**) on bitcoin node. Installing tmux on mining node can be handy. Also Additionally, you need to enable "lingering" so that the tmux process can persist even if no active user session.
    **loginctl enable-linger**
    
  
