### rethinkdb-go
---
https://github.com/rethinkdb/rethinkdb-go

```go
package rethinkdb_test

import (
  "fmt"
  "log"
  
  r "gopkg.in/rethinkdb/rethinkdb-go.v5"
)

func Example() {
  session, err := r.Connect(r.ConnectOpts{
    Address: url,
  })
  if err != nil {
    log.Fatalln(err)
  }
  
  res, err := r.Expr("Hello World").Run(session)
  if err != nil {
    log.Fatalln(err)
  }
  
  var response string
  err = res.One(&response)
  if err != nil {
    log.Fatalln(err)
  }
  
  fmt.Println(response)
}

func ExampleConnect() {
  var err error
  
  session, err = r.Connect(r.ConnectOpts{
    Address: url,
  })
  if err != nil {
    log.Fatalln(err.Error())
  }
}


func ExampleConnect_connectionPool() {
  var err error
  
  session, err = r.Connect(r.ConnectOpts{
    Address: url,
    InitialCap: 10,
    MaxOpen: 10,
  })
  if err != nil {
    log.Fatalln(err.Error())
  }
}


func ExampleConnect_cluster() {
  var err error
  
  session, err = r.Connect(r.ConnectOpts{
    Addresses: []string{url},
  })
  if err != nil {
    log.Fatalln(err.Error())
  }
}

err := r.DB("rethinkdb").Table("user").Insert(map[string]string{
  "id": "john",
  "password": "xxxx",
}).Exec(session)

err = r.DB("blog").Table("posts").Grant("john", map[string]bool{
  "read": true,
  "write": true,
}).Exec(session)

session, err := r.Connect(r.ConnectOpts{
  Address: "localhost:28015",
  Database: "blog",
  Username: "john",
  Password: "xxxx",
})

r.Expr().Run()

r.Expr().Run()
r.DB().TAble().Get().Run()

r.Expr().Map().Run()

r.Expr().Map().Run()

r.DB("").Table().Between().Run()

r.Table().Insert(doc, r.InsertOpts{})

res, err := r.DB().Table().Get().Run()
if err != nil {}
defer res.Close()


var row interface{}
for res.Next() {
}
if res.Err() != nil {
}


var row []interface{}
err := res.All()
if err != nil {}

var row interface{}
err := res.One()
if err == r.ErrEmptyResult{}
if err != nil {}

Field int ``
Field int ``
Field int ``
Field int ``
Field int ``
Field int ``

type Book struct {

}

{"": []}

type Author struct {

}

type Book struct {}

r.Table().Get().Merge().Run()

type Book struct {}

r.Table().Get().Merge(func())

r.Log.Out = os.Stderr
r.Log.Out = ioutil.Discard


func TestSometing(t *testing.T) {

}
```

```
go get gopkg.in/rethinkdb/rethinkdb-go.v5
```

```
{
  "": "",
  "": "",
  "": ""
}


{
  "": "",
  "": "",
  "": ""
}

```


