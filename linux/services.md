# services
### starting services
to start a service we use the following command:
```
sudo systemctl start http.service
```
change out the `http` for the desired service to restart

### enabling services at startup
```
sudo systemctl enable http.service
```
change out the `http` for the desired service to enable at boot

### showing service status
```
sudo systemctl status http.service -l
```
With this command we can see whether or not a service is started.
we can also see the last logs from this service so if something went wrong this is an easy place to start

For more information on errors we can also consult the log files.
The next command displays the log files
```
sudo journalctl -l
```
or in the folder
```
/var/log/
```
this file is way to big to find something so there are 2 ways to get around this.
The first one is filtering, this we can do with a pipe to the `grep` command:
```
sudo journalctl -l | grep dhcpd
```
with `grep` we can filter everything we get from the journals.

The other way is always looking at the bottom of the log files
```
sudo journalctl -l -f
```
will scroll the bottom of the log files, you can also filter this further with the `grep`command

```
sudo tail -f -l /var/log/*

sudo less /var/log/*
```
these 2 options will scroll the bottom of the log files found in the `/var/log/` folder, you can also replace the `*` with specific services to filter further.
