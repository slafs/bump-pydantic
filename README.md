# Bump Pydantic ♻️

<!-- [![PyPI - Version](https://img.shields.io/pypi/v/bump-pydantic.svg)](https://pypi.org/project/bump-pydantic)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/bump-pydantic.svg)](https://pypi.org/project/bump-pydantic) -->

Utility to bump pydantic from V1 to V2.

-----

### Rules

#### BP001: Replace imports

- ✅ Replace `BaseSettings` from `pydantic` to `pydantic_settings`.
- ✅ Replace `Color` and `PaymentCardNumber` from `pydantic` to `pydantic_extra_types`.

#### BP002: Add default `None` to `Optional[T]`, `Union[T, None]` and `Any` fields

- ✅ Add default `None` to `Optional[T]` fields.

The following code will be transformed:

```py
class User(BaseModel):
    name: Optional[str]
```

Into:

```py
class User(BaseModel):
    name: Optional[str] = None
```

#### BP003: Replace `Config` class by `model_config`

- ✅ Replace `Config` class by `model_config = ConfigDict()`.

The following code will be transformed:

```py
class User(BaseModel):
    name: str

    class Config:
        extra = 'forbid'
```

Into:

```py
class User(BaseModel):
    name: str

    model_config = ConfigDict(extra='forbid')
```

#### BP004: Replace `BaseModel` methods


#### BP005: Replace `GenericModel` by `BaseModel`

- ✅ Replace `GenericModel` by `BaseModel`.

The following code will be transformed:

```py
from typing import Generic, TypeVar
from pydantic.generics import GenericModel

T = TypeVar('T')

class User(GenericModel, Generic[T]):
    name: str
```

Into:

```py
from typing import Generic, TypeVar
from pydantic.generics import GenericModel

T = TypeVar('T')

class User(BaseModel, Generic[T]):
    name: str
```
