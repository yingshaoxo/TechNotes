# Funny Python Dict Feature/Bug

I found that for python, if we have an object with number key, if we use JSON module to dump it, it will convert the number key to string key,  which will make a lot of error later if you use number as key to operate it:

source: `{1: 0, 2: 0}`

after using  `json.loads(json.dumps())`

we get: `{'1': 0, '2': 0}`

Meanwhile, Javascript handles it fine. 

Javascript will get `{1: 0, 2: 0}` after using `JSON.parse(JSON.stringify())`