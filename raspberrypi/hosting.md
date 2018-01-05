# Hosting Websites

1. Register domain on Namecheap.com.

2. Configure 'ufw' firewall to enable exceptions to your port.

3. Run this command to extract public IP address.
   ```bash
   curl ipinfo.io/ip
   ```

4. For Node.js, have the web server launch at boot up. See [Raspberry Pi
   instructions](https://github.com/ivanmanan/Linux-Tools/blob/master/raspberrypi.md).

5. Go to Namecheap.com and select 'Domain List'. Select 'Manage' to the
   corresponding domain you purchased. Then select 'Advanced DNS'.

6. Under host records, you want to insert two entries:
   1. Type: A Record | Host: www | Value: xxx.xx.xx.x | TTL: 30 min
   2. Type: URL Redirect Record | Host: @ | Value: http://xxx.xx.xx.x:PORt |
      Masked | Meta
