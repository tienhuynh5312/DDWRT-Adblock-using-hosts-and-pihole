# DDWRT-Adblock-using-hosts-and-pihole

## Create a mega host file for ad block
Credit: @m-parashar
https://gist.github.com/m-parashar/ee38454c27f7a4f4e4ab28249a834ccc
File name: adbhostgen.sh

## Instruction
Please enable support JFFS2 or use your own USB Drive attached to your router.

`DDWRT router homepage > Administration > Management > JFFS2 Support > Enable`

*Optional: you can tick clean up at start up to clean everything*

Use WinSCP to copy adbhostgen.sh to /jffs or make new file with its content.

Use Putty run this line to make adbhostgen.sh runable.

`chmod +x /jffs/adbhostgen.sh`

Then, run this line to make a host file. Wait until the process finished.

`sh /jffs/adbhostgen.sh`

On the same page, enable Cron schedule, and add this line into the textbox.
`0 6 * * 1 root /jffs/dnsmasq/adbhostgen.sh`

Now, we need to make some changes in DNSMasq setting.
`DDWRT router homepage > Services > Services > DNSMasq`
  DNSMasq: Enable
  Local DNS: Enable
  No DNS Rebind: Enable
  Inside the "Additional DNSMasq Options" add these lines:
    `addn-hosts=/jffs/dnsmasq/mphosts
    dhcp-option=6, 176.103.130.130, 176.103.130.131`
    
Reboot the router.
