# Second Reverse Proxy Method

Checking with an if statement and then editing, rather than rewriting the file each time.

## Code

``` 
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
else
    # reverse proxy not configured yet
    echo "configuring reverse proxy..."
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
fi
```

If the proxypass statement is in the 000-default.conf file...<br>
- Do nothing<br>

If the proxypass statement is not in the 000-default.conf file...<br>
- Add the ProxyPreserveHost, ProxyPass, and ProxyPassReverse statements after the DocumentRoot statement inside the 000-default.conf file

## Testing method

- install, start and enable apache, add the two modules, restart apache
- cd /etc/apache2/sites-available/ (cd into folder with 000-default.conf file)
- cp 000-default.conf 000-default.conf.bk (copy file to create a backup)
- Test the file editing line (sed) manually
  - Every forwardslash in a string must have a backslash in front of it
- Test the if statement with a file with the ProxyPass statement and a file without it manually