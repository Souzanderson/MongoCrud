# Python Package for MongoDB CRUD

## For use:
- Install package with PIP;
- Import from mongocrud Mongocrud;
- Configure database settings (location, collection, port...);
- Call object CRUD operations;

## Example:

* For INSERT operation in database:

```python
from mongocrud import MongoCRUD, ObjectId
from datetime import datetime

dbclients = MongoCRUD("mongodb://localhost","mongoteste1")

dbclients.insert("clients", {"_id": "12345", "name":"Anderson 1", "dtupdate": datetime.now()})
dbclients.insert("clients", {"_id": 15 , "name":"Anderson 2", "dtupdate": datetime.now()})
dbclients.insert("clients", {"name":"Anderson 3", "dtupdate": datetime.now()})
dbclients.insert("clients", {"name":"Anderson 4", "dtupdate": datetime.now()})
dbclients.insert("clients", {"name":"Anderson 5", "dtupdate": datetime.now()})
#12 bits/24 bits info as _id
dbclients.insert("clients", {"_id": ObjectId(b'000000000001'), "name":"Anderson 6", "dtupdate": datetime.now()})
```

* For SELECT operation on database (using orderby and direction for sort information):

```python
from mongocrud import MongoCRUD
from datetime import datetime

dbclients = MongoCRUD("mongodb://localhost","mongoteste1")
clients_ordered = dbclients.select("clients", orderby="dtupdate", direction=1)

for client in clients_ordered: print(client)
```

* For SELECT BY _id (select if using ObjectId on _id):

```python
from mongocrud import MongoCRUD
from datetime import datetime

dbclients = MongoCRUD("mongodb://localhost","mongoteste1")

clients = dbclients.select_by_id("clients", "12345", is_objectid=False)
print(clients)
clients = dbclients.select_by_id("clients", 15, is_objectid=False)
print(clients)
clients = dbclients.select_by_id("clients", "64495d9c140992e498f5fcb2", is_objectid=True)
print(clients)
```

* For DELETE query in database:

```python
from mongocrud import MongoCRUD
from datetime import datetime

dbclients = MongoCRUD("mongodb://localhost","mongoteste1")

items = dbclients.delete("clients", {"name": "Anderson 2"})
print("QTD items deleted => ", items)
```

* For DELETE BY _id:

```python
from mongocrud import MongoCRUD, ObjectId
from datetime import datetime

dbclients = MongoCRUD("mongodb://localhost","mongoteste1")

items = dbclients.delete_by_id("clients", "12345", is_objectid=False)
print("QTD items deleted => ", items)

items = dbclients.delete_by_id("clients", "64495d9c140992e498f5fcb1", is_objectid=True)
print("QTD items deleted => ", items)

items = dbclients.delete_by_id("clients", ObjectId(b"000000000001"), is_objectid=False)
print("QTD items deleted => ", items)
```

* for UPDATE row:

```python
from mongocrud import MongoCRUD
from datetime import datetime

dbclients = MongoCRUD("mongodb://localhost","mongoteste1")

dbclients.update_one("clients", "12345", {"name": "teste1", "dtupdate": datetime.now()}, is_objectid=False)
dbclients.update_one("clients", "64496373fe1ef021a556b446", {"name": "teste2", "dtupdate": datetime.now()}, is_objectid=True)
```


