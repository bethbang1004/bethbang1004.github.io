---
layout: post
title:  "Vue.js router 활용하기"
date:   2020-09-05 01:10:51 +0900
categories: Postgresql SSH Tunneling
---

# Postgresql pgAdmin4로 접속하기         
postgresql DB를 사용할 때, 터미널에서 직접 확인하며 db를 구성한다는 건 가독성도 떨어질 뿐 아니라,       
작업하기가 쉽지 않습니다. 그래서 pgAdmin4를 사용하여 Gui로 db를 연결하여 구성하는 방법을 소개 드립니다.   

그리고 요즘에는 클라우드 환경을 많이 사용하고 있습니다.   
보통 ssh 로그인을 할 때도 public key를 사용하여 로그인을 하는데요,   
이로 인해, pgAdmin4 툴에 연결할 때도 ssh Tunneling을 설정해 주어야 합니다.   
해당 방법을 소개 드립니다.               

### 기존 패키지 업데이트            
postgresql 설치를 위해 기존 패키지 파일들 모두 업데이트를 합니다.   
```   
sudo apt-get update   
```       

### postgresql 설치       
postgresql 기본 설치와 부가 기능 설치인 contrib을 설치합니다.      
```
sudo apt-get install postgresql postgresql-contrib -y     
```      

### postgresql 설치 확인     
postgresql 잘 설치되었는지, 버전은 몇인지 확인합니다.        
```   
sudo psql --version   
```        
### 허용할 ip 설정     
**Path: sudo vi /etc/postgresql/10/main/postgresql.conf**   
저는 설치된 버전이 10 이기 때문에 디렉토리가 10으로 되어있습니다.   
본인이 설치된 디렉토리로 이동하시면 됩니다.   
모든 아이피를 허용할 것이기 때문에 59번째 line에 **listen_addresses='*'** 로 설정하여 줍니다.   

```  
.
.
.
# - Connection Settings -

listen_addresses = '*'                  # what IP address(es) to listen on;
                                        # comma-separated list of addresses;
                                        # defaults to 'localhost'; use '*' for all
                                        # (change requires restart)
port = 5432                             # (change requires restart)
max_connections = 100                   # (change requires restart)
#superuser_reserved_connections = 3     # (change requires restart)
unix_socket_directories = '/var/run/postgresql' # comma-separated list of directories
.
.
.
```   

## 접속 ip 영역 및 보안 설정      
해당 파일에 두 가지 설정을 삽입합니다.   
85번째 line에 DB 로그인 시, 모든 IP 영역 허용을 위해 0.0.0.0/0 으로, md5로 설정하여 줍니다.    

```    
# Database administrative login by Unix domain socket
local   all             all                                     md5   
```    

마지막 line인 100번째에, 아래와 같이 추가하여 줍니다.   
본인의 ip 대역을 c 클래스 형식(예. 192.168.0.0/0) 으로 하셔도 됩니다.   
저는 모든 아이피 허용을 하겠습니다.   
```  
host    all             all             0.0.0.0/0               md5   
```     

## postgresql 재시작   
모든 설정을 저장하기 위해 서비스를 재시작 합니다.   
```   
sudo service postgresql restart   
```       

## DB 포트 열기   
보통 postgresql은 5432 포트를 사용합니다.   
해당 포트를 열어줍니다.   
```   
sudo ufw status
```     
```   
sudo ufw allow 5432   
```    


## postgresql 접속   
기본으로 제공하는 postgres로 계정 변환을 합니다.   
```   
sudo -i -u postgres   
```   
```   
psql      
```   

## postgres 비밀번호 설정(DB계정 비밀번호)     
기본 계정을 사용할 것이므로, 기본 계정인 postgres의 비밀번호를 설정합니다.    
```    
alter user postgres with encrypted password '설정할 비밀번호';   
```    

## DB 생성   
```   
CREATE DATABASE 생성할DB명;   
```    

## DB 접속 권한 설정   
postgres 계정에 모든 권한을 허용하도록 하였습니다.    
```   
GRANT ALL PRIVILEGES ON DATABASE 생성한DB명 TO postgres;   
```   
## 터미널에서 DB 접속 확인      
```   
psql -h localhost -U postgres -d 생성한DB명      
```   

## pgAdmin4 설정_1   
***   
pgAdmin4 다운로드:   
<https://www.pgadmin.org/download/>      
***   
이제 Gui 툴인 pgAdmin4에서 사용할 수 있도록 db 연결을 하겠습니다.   
**Add New Server**를 클릭합니다.      
![Alt text](/assets/AddServer.png "add_new_server")      

## pgAdmin4 설정_2   
pgAdmin에서 알아보기 쉬운 이름으로 설정합니다.     
**Gerneral 탭에서 name 설정**           
![Alt text](/assets/general.png "general")      

## pgAdmin4 설정_3      
설정한 db를 연결하는 항목입니다.   
사설 ip를 입력하는 부분인데, 저는 localhost로 접속할 것이기 때문에 host name/address 항목에 localhost를 입력하여 줍니다.     
| 항목 | 값 |
|---|:---:|---:|
| `Host name/address` | 사설ip (localhost) |   
| `Port` | 설정한 DB 포트 5432 |   
| `Maintenance database` | 설정한 db명 |   
| `Username` | 설정한 db 계정명 (기본 계정 postgres) |   
| `Password` | 설정한 db 계정의 비밀번호 |   

**Connection 탭 DB 연결 설정**           
![Alt text](/assets/connection.png "connection")    

## pgAdmin4 설정_4    
SSH Tunneling 설정 항목 입니다.   
ssh 로그인 시 public key로 연결을 하는 경우에는 외부에서 db를 연결할 때도 ssh Tunneling 설정을 하지 않으면, 연결이 되지 않습니다.   
내가 접속해도 되는 사용자라는 걸 증명하기 위해 ssh Tunneling을 해주어야 합니다.   
| 항목 | 값 |
|---|:---:|---:|
| `Use SSH tunneling` | Yes) |   
| `Tunnel Host` | 공인 IP (ssh 접속 IP) |   
| `Tunnel Port` | 22 (ssh 기본 포트) |   
| `Username` | SSH 접속 계정 |   
| `Authentication` | Identity file |    
| `Identity file` | public key 파일 삽입 |    

**SSH Tunneling 탭 SSH 연결 설정**           
![Alt text](/assets/sshTunneling.png "sshTunneling")     

이로써, 설정이 완료되었습니다 :)   
