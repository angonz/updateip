# updateip.sh

If you have a server behind an ISP without a fixed IP, the ISP may change its public IP anytime. Actually this may happen after a service outage or a modem reset.
There are some programs that detect this situation and can update the public IP address in the DNS accordingly.
However, if the server is behind a router, it will never know when the public address has changed.

This script detects when the public address has changed, even regardless the private IP address of the server. Then it updates the DYN record of the DNS server.

It works with Zoneedit DNS provider. However it can be easily modified to suite any other DNS service, provided it has a web service URL to change the record.

Installation
------------

This is a bash script tested in Ubuntu 14.04 LTS.

- Copy updateip.sh to a suitable folder for custom scripts (normally /usr/local/bin)
- Creat a crontab entry to execute the script periodically. Every 30 min show be fine. Not too fast, because the DNS server may block your updates and you may load the server unnecessarily.
In Ubuntu, a way to do this is:
	- sudo crontab-e
	In the editor window, append the following line to the end of the file:
	0,30 * * * * /usr/local/bin/updateip

Logfile
-------

updateip.sh will log events in a file, by default, /var/log/updateip.log. The logfile can be modified in the scrip by changing the LOGFILE variable at the beginning.


Notes
-----

Depending on where the logfile is located, updateip.sh needs to be executed as root.
