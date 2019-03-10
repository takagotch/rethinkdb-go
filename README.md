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

r.Expr([]interface{}{1, 2, 3, 4, 5}).Run(session)

r.Expr(map[string]interface{}{"a": 1, "b": 2, "c": 3}).Run(session)
r.DB("database").Table("table").Get("GUID").Run(session)

r.Expr([]interface{}{1, 2, 3, 4, 5}).Map(func (row Term) interface{} {
  return row.Add(1)
}).Run(session)

r.Expr([]interface{}{1, 2, 3, 4, 5}).Map(r.Row.Add(1)).Run(session)

r.DB("database").Table("table").Between(1, 10 r.BetweenOpts{
  Index: "num",
  RightBound: "closed",
}).Run(session)

r.Table("test").Insert(doc, r.InsertOpts{
  Conflict: func(id, oldDoc, newDoc r.Term) interface{} {
    return newDoc.Merge(map[string]interface{}{
      "count": oldDoc.Add(newDoc.Field("count")),
    })
  }
})

res, err := r.DB("database").Table("tablename").Get(key).Run(session)
if err != nil {
}
defer res.Close()


var row interface{}
for res.Next(&row) {
}
if res.Err() != nil {
}


var row interface{}
err := res.All(&row)
if err != nil {
}

var row interface{}
err := res.One(&row)
if err == r.ErrEmptyResult{
}
if err != nil {
}

Field int `rethinkdb:"-"`
Field int `rethinkdb:"myName"`
Field int `rethinkdb:"myName,omitempty"`
Field int `rethinkdb:",omitemtpy"`
Field int `rethinkdb:"myName[0]"`
Field int `rethinkdb:"myName[1]"`

type Book struct {
  AuthorID string `rethinkdb:"id[0]"`
  Name string `rethinkdb:"id[1]"`
}

{"id": [AUTHORID, NAME]}

type Author struct {
  ID string `rethinkdb:"id,omitempty"`
  Name string `rethinkdb:"name"`
}

type Book struct {
  ID string `rethinkdb:"id,omitempty"`
  Title string `title`
  Author Author `"author_id,reference" rethinkdb_ref:"id"`
}

r.Table("books").Get("1").Merge(func(p r Term) interface{} {
  return map[string]interface{}{
    "author_id": r.Table("authors").Get(p Field("author_id")),
  }
}).Run(session)

type Book struct {
  ID string `rethinkdb:"id,omitempty"`
  Title string `rethinkdb:"title"`
  Author []Author `rethinkdb:"author_ids,reference" rethinkdb_ref:"id"`
}

r.Table().Get().Merge(func(p r.Term) interface{} {
  return map[string]interface{}{
    "author_ids": r.Table("authors").GetAll(r.Args(p.Field("author_ids"))).CoerceTo("array"),
  }
})

r.Log.Out = os.Stderr
r.Log.Out = ioutil.Discard


func TestSometing(t *testing.T) {
  mock := r.NewMock()
  mock.On(r.Table("people")).Return([]interface{}{
    map[]interface{}{"id": 1, "name":"John Smith"},
    map[]interface{}{"id": 2, "name":"Jane Smith"},
  }, nil)
  
  cursor, err := r.Table("people").Run(mock)
  if err != nil {
    t.Errorf("err is: %v", err)
  }
  
  var rows []interface{}
  err = cursor.All(&rows)
  if err != nil {
    t.Errorf("err is: %v", err)
  }
  
  mock.AssertExpectations(t)
}
```

```
go get gopkg.in/rethinkdb/rethinkdb-go.v5
```

```
{
  "author_id": "author_1",
  "id": "book_1",
  "title": "The Hobbit"
}


{
  "author_ids": ["author_1", "author_2"],
  "id": "book_1",
  "title": "The Hobbit"
}

```


