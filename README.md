# InPynamoDB

[![Build Status](https://travis-ci.org/sunghyun-lee/InPynamoDB.svg?branch=master)](https://travis-ci.org/sunghyun-lee/InPynamoDB)
[![Coverage Status](https://coveralls.io/repos/github/sunghyun-lee/InPynamoDB/badge.svg?branch=4.1.0)](https://coveralls.io/github/sunghyun-lee/InPynamoDB?branch=master)

This transforms [PynamoDB](https://github.com/pynamodb/PynamoDB)'s basic methods working asynchronously used [aiobotocore](https://github.com/aio-libs/aiobotocore).

This library may be merged into PynamoDB as a feature of it, but for the time being, you can use this library if you need to run any operation on DynamoDB asynchronously. 

### From introduction of [PynamoDB](https://github.com/pynamodb/PynamoDB):
A Pythonic interface for Amazon's DynamoDB that supports Python 2 and 3. (InPynamoDB supports from Python 3.6 because this uses async/await.)

DynamoDB is a great NoSQL service provided by Amazon, but the API is verbose. PynamoDB presents you with a simple, elegant API.
 
# Requirements
- Python 3.6 and above for this library is using `async/await` keyword.

# Installation
$ pip install InPynamoDB

# Basic Usage

This library is not well-documented. If you know how to use asyncio with async/await syntax, you will know where to change
from PynamoDB syntax since it is very intuitive to use if you know how to use PynamoDB and asyncio.

Detailed document will be available, soon. (Please bear with me) 

For the time being, please refer to [PynamoDB documentation](https://pynamodb.readthedocs.io/).


### Defining model
```python
from inpynamodb.models import Model
from inpynamodb.attributes import UnicodeAttribute

class UserModel(Model):
    """
    A DynamoDB User
    """
    class Meta:
        table_name = "dynamodb-user"
    email = UnicodeAttribute(null=True)
    first_name = UnicodeAttribute(range_key=True)
    last_name = UnicodeAttribute(hash_key=True)


# you can declare model:
user = UserModel(email="hgd@testing.com", first_name="gildong", last_name="hong")

```

### Basic Manipulation

```python
# GET
user = await UserModel.get(hash_key="John", range_key="Doe")

# BATCH_GET
async for user in UserModel.batch_get(keys):  # `keys` argument should be list.
    print(user.id)
    # ...
```

- UPDATE

```python
await user.update(actions=[UserModel.first_name.set("new_first_name")])
```

# Contribution
Any form of contribution is always welcome! This library uses `poetry` as package manager, so you have to install [poetry](https://python-poetry.org/) to install required packages.

Please leave issues in any form, I will check ASAP.
