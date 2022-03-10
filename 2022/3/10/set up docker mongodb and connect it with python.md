# set up docker mongodb and connect it with python

## set up docker
```bash
docker run -d \
      -p 27017:27017 \
      --name myMongo \
      -v ~/dataOfMongo:/data/db \
      -e MONGO_INITDB_ROOT_USERNAME=admin \
      -e MONGO_INITDB_ROOT_PASSWORD=password \
      mongo
```

## set up python
```bash
poetry add pymongo
```

## use python
```python
import pymongo


myclient = pymongo.MongoClient("mongodb://localhost:27017/",
                     username='admin',
                     password='password',
)

mydb = myclient["mydatabase"]

print(mydb.list_collection_names())

users = mydb["users"]
users.insert_one({"name": "John"})

for user in users.find():
    print(user)
```