# Example-/Test-Configuration for an internal imap server with sogo UI 

## Description

Example-/Test-Configuration for an internal imap server with sogo UI 

## Services

### traefik

### syslog

### imap

see https://github.com/unimock/imap-docker

### sogo

see https://github.com/unimock/sogo-docker

## Installation and Setup

See "control" script for futher information.

### establish and run a test environment
```
git clone https://github.com/unimock/groupware-docker ./groupware
cd groupware
#vi groupware.env-template
./control install
./control info
./control test
./control up|down
./control uninstall
```
### prepare and start runtime environment 
```
  # set global data
  cp groupware.env-template groupware.env
  vi groupware.env
  #
  cd imap
  cp docker-compose.yml-template docker-compose.yml
  vi docker-compose.yml
  docker-compose up -d
  docker-compose logs -f
  # 
  cd sogo
  cp docker-compose.yml-template docker-compose.yml
  vi docker-compose.yml
  docker-compose up -d
  docker-compose logs -f
```

## Configuration

* see https://github.com/unimock/imap-docker
* see https://github.com/unimock/sogo-docker

## further tests:
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


