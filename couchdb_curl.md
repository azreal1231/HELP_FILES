* ##   Install CouchDB
    *  [Install CouchDB](https://linuxhint.com/install_couchdb_ubuntu/)



* ##   view all the DB's
```
curl -X GET http://127.0.0.1:5984/_all_dbs
```

* ##  add a DB
```
curl -X PUT http://admin:admin@127.0.0.1:5984/curlTestDB
```

* ##  set a var
```
SET SERVER=http://admin:admin@127.0.0.1:5984
```

*  ## See a var
```
ECHO %SERVER%
```

* ##  GET DB's using a var

```
curl -X GET %SERVER%/_all_dbs
```

* ##  view data using a **view**
```
curl -X GET %SERVER%/mycompany/_design/view3/_view/new-view
```

* ##  will generate an ID
```
curl -X GET %SERVER%/_uuids
```
* ##  adding a new client
```
curl -X PUT %SERVER%/mycompany/f23fa30cd7ffbfd9871bca23cb00fbbf -d "{\"name\":\"client3\",\"email\":\"client3@gmail.com\"}"
```