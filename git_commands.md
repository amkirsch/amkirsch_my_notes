# Random & Useful

Use the following to show the 4th last commit version of the file
```shell
git show HEAD~4:/path/to/file
```
To transfer one or more files to and from machines quickly [ssh]
```shell
rsync -Pvar0 /path/to/files/*  user@example.com:/path/to/dir/
```

Commands to find ports in use
```shell
sudo lsof -i -P -n | grep LISTEN
sudo netstat -tulpn | grep LISTEN
sudo nmap -sTU -O IP-address-Here
```

