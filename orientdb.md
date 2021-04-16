
```
# CONNECT remote:localhost/test root toto
#    tree:
#        command:
#            - /orientdb/bin/server.sh
#            - -Dstorage.diskCache.bufferSize=1024
#        env_file:
#            - .env
#        environment:
#            - ORIENTDB_ROOT_PASSWORD=toto
#        image: orientdb:3.1.6
#        networks:
#            lupusmic:
#                aliases:
#                    - db
#                ipv4_address: 172.29.0.41
#        restart: 'always'
#        volumes:
#            - ${PWD}/data:/data
```

```
set echo on
CONNECT remote:localhost root toto

create database remote:localhost/test root toto

create class site extends v
create property site.title string

create class page extends v
create property page.title string
create property page.created datetime
create property page.last_modified datetime

create class node extends v

create class path extends e
create property path.title string (mandatory true, min 1, max 255)

create class leaf extends e
create property leaf.kind


script sql
let site = create vertex site set title='Lupus Michaelis'
let site_root = create vertex node
let page = create vertex page content {'title': 'Acceuil', 'created': sysdate(), 'last_modified': sysdate()}
let page404 = create vertex page content {'title': 'Page inconnue', 'created': sysdate(), 'last_modified': sysdate()}

create edge path from ($site) to ($site_root) content {'title': '/'}
create edge leaf from ($site) to ($page)

end -- script sql
```
