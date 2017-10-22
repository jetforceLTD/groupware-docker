# exampe and testing configuration for an internal imap server with sogo 

## Description

Example-/testing configuration for an internal imap server with sogo UI.

## Services

### traefik

* traefik/service/traefik.toml # Domain

### syslog

* syslog/service/rsyslog.conf

### imap

see https://github.com/unimock/imap-docker

### sogo

see https://github.com/unimock/imap-docker

## Installation and Setup

See "control" script for futher information.

```
git clone https://github.com/unimock/groupware-docker ./groupware
cd groupware
cp groupware.env-template groupware.env
#vi groupware.env
./control install
./control setup
./control up|down
./control uninstall
```

## Configuration

* see https://github.com/unimock/imap-docker
* see https://github.com/unimock/sogo-docker

## Tests
```
SERVER=127.0.0.1
MUSER=hugo@domain.local
MPASS=hugo30
```

### smtp
```
PORT=25
PORT=587
echo "prima" | sendemail -s ${SERVER}:$PORT  -f root@test.com -t ${MUSER} -u test -o tls=no
echo "prima" | sendemail -s ${SERVER}:$PORT  -f root@test.com -t ${MUSER} -u test -o tls=yes
echo "prima" | sendemail -s ${SERVER}:$PORT  -f root@test.com -t ${MUSER} -u test -o tls=yes -o username=${MUSER}  -o password=${MPASS}
```

###  imap
```
telnet ${SERVER} 143
 & LOGIN ${MUSER} ${MPASS}
 & LIST "" "*"
 & LOGOUT
```

### sieve
```
telnet ${SERVER} 4190
```


