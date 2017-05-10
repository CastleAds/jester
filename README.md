# Jester

Convenience utilities for applications in Python 3.4+

## Get started

```
pip install jester
```

## Packages
### MySQL

```
import jester.mysql

db = jester.mysql.MySQLConnection(
    host="localhost"
    , user="username"
    , passowrd="password"
    , database="local_db"
    , port=3306
)

transactions = db.execute_raw("""
    SELECT * FROM transactions WHERE DATE_FORMAT(date, '%Y-%m-%d') = %s
""", ['2017-04-01'])

ids = map(lambda t: t['id'], transactions)

from jester.constants import JSON

query = jester.mysql.Query("""
    SELECT metadata
    FROM transactions
    WHERE id = %s
""", params=[ids[0]], schema={
    "metadata": JSON
})

transaction_data = db.execute(query)
print(transaction_data['vendor_detail_1'])
```

### Utils

```
from jester.utils import flatten

nested = [
    [1,2,3]
    , [4,5,6]
    , [7,8,9]
]

flatten(nested)

# [1,2,3,4,5,6,7,8,9]
```