---
layout: post
title: "Python Path Management"
date: 2025-11-04T00:00:00Z
authors: ["SG Lee"]
categories: ["Development"]
description: "Python Path Management"
thumbnail: "/assets/images/gen/blog/blog-5-thumbnail.webp"
image: "/assets/images/gen/blog/blog-5-large.webp"
---

# Python Package: 상대 경로 vs 절대 경로 완벽 가이드

**작성일:** 2025-11-04  
**Copyright:** VCANUS  
**버전:** 1.0

---

## 목차

1. [개요](#1-개요)
2. [상대 경로 (Relative Imports)](#2-상대-경로-relative-imports)
3. [절대 경로 (Absolute Imports)](#3-절대-경로-absolute-imports)
4. [비교표](#4-비교표)
5. [사용 시나리오별 권장사항](#5-사용-시나리오별-권장사항)
6. [실전 예시](#6-실전-예시)
7. [흔한 실수와 해결방법](#7-흔한-실수와-해결방법)
8. [베스트 프랙티스](#8-베스트-프랙티스)

---

## 1. 개요

Python에서 모듈을 import하는 방식은 크게 두 가지입니다:

- **상대 경로 (Relative Imports)**: 현재 모듈의 위치를 기준으로 import
- **절대 경로 (Absolute Imports)**: 프로젝트 루트부터 전체 경로로 import

### 1.1 기본 문법

```python
# 상대 경로
from .module import Class          # 같은 디렉토리
from ..module import Class         # 상위 디렉토리
from .subpackage.module import Class  # 하위 패키지

# 절대 경로
from mypackage.module import Class
from mypackage.subpackage.module import Class
```

### 1.2 예제 패키지 구조

이 가이드에서 사용할 예제 구조:

```
mypackage/
├── __init__.py
├── models/
│   ├── __init__.py
│   ├── user.py
│   └── product.py
├── services/
│   ├── __init__.py
│   ├── user_service.py
│   └── product_service.py
└── utils/
    ├── __init__.py
    ├── validators.py
    └── formatters.py
```

---

## 2. 상대 경로 (Relative Imports)

### 2.1 기본 개념

상대 경로는 **점(.)** 을 사용하여 현재 모듈의 위치를 기준으로 import합니다.

```python
from .module import Class      # 현재 패키지의 module
from ..module import Class     # 상위 패키지의 module
from ...module import Class    # 상위의 상위 패키지의 module
```

### 2.2 상대 경로 패턴

#### 패턴 1: 같은 디렉토리

```python
# mypackage/models/user.py

from .product import Product  # 같은 models 디렉토리의 product.py
```

**디렉토리 구조:**
```
models/
├── user.py      ← 여기서
└── product.py   ← 이것을 import
```

#### 패턴 2: 상위 디렉토리

```python
# mypackage/services/user_service.py

from ..models import User  # 상위(mypackage)의 models 패키지
```

**디렉토리 구조:**
```
mypackage/
├── models/
│   └── user.py     ← 이것을 import
└── services/
    └── user_service.py  ← 여기서
```

#### 패턴 3: 형제 패키지

```python
# mypackage/services/user_service.py

from ..utils.validators import validate_email  # 형제 패키지
```

**디렉토리 구조:**
```
mypackage/
├── services/
│   └── user_service.py  ← 여기서
└── utils/
    └── validators.py    ← 이것을 import
```

#### 패턴 4: 복잡한 경로

```python
# mypackage/api/v1/endpoints/users.py

from ....models import User  # 4단계 상위의 models
from ...services import UserService  # 3단계 상위의 services
from ..auth import authenticate  # 1단계 상위의 auth
```

**디렉토리 구조:**
```
mypackage/
├── models/
│   └── user.py
├── services/
│   └── user_service.py
└── api/
    └── v1/
        ├── auth.py
        └── endpoints/
            └── users.py  ← 여기서
```

### 2.3 상대 경로의 장점 ✅

#### 1. 패키지명 변경 용이

```python
# mypackage/__init__.py → yourpackage/__init__.py
# 패키지명을 바꿔도 내부 import는 수정 불필요

# ✅ 상대 경로 (수정 불필요)
from .models import User
from .services import UserService

# ❌ 절대 경로 (모두 수정 필요)
from mypackage.models import User  # yourpackage로 변경 필요
from mypackage.services import UserService  # yourpackage로 변경 필요
```

#### 2. 패키지 재사용 및 이식성

```python
# other_project에 mypackage 폴더를 복사
# ✅ 상대 경로: 그대로 작동
# ❌ 절대 경로: 모든 import 수정 필요
```

#### 3. 패키지 구조 명확성

```python
# mypackage/services/user_service.py

from ..models import User  # ← 상위 패키지의 models라는 것이 명확
from .auth_service import AuthService  # ← 같은 services 패키지라는 것이 명확
```

#### 4. 순환 참조 감지 용이

```python
# 상대 경로는 순환 참조를 더 명확하게 보여줌
# mypackage/models/user.py
from ..services import UserService  # models → services

# mypackage/services/user_service.py
from ..models import User  # services → models
# ← 순환 참조 명확!
```

### 2.4 상대 경로의 단점 ⚠️

#### 1. 스크립트로 직접 실행 불가

```python
# mypackage/models/user.py
from .product import Product

# ❌ 직접 실행 시 에러
# python mypackage/models/user.py
# ValueError: attempted relative import beyond top-level package
```

**해결방법:**
```bash
# ✅ 모듈로 실행
python -m mypackage.models.user
```

#### 2. 깊은 중첩 시 가독성 저하

```python
# 너무 많은 점은 헷갈림
from ....models.user import User
from .....utils.validators import validate
```

#### 3. IDE 자동완성 제한

일부 IDE에서는 상대 경로의 자동완성 지원이 약할 수 있습니다.

---

## 3. 절대 경로 (Absolute Imports)

### 3.1 기본 개념

절대 경로는 **프로젝트 루트부터 전체 경로**를 명시합니다.

```python
from mypackage.models.user import User
from mypackage.services.user_service import UserService
```

### 3.2 절대 경로 패턴

#### 패턴 1: 전체 경로 명시

```python
# mypackage/services/user_service.py

from mypackage.models.user import User
from mypackage.utils.validators import validate_email
```

#### 패턴 2: 패키지 레벨 import

```python
# mypackage/services/user_service.py

from mypackage import models
from mypackage import utils

user = models.User()
```

#### 패턴 3: 선택적 import

```python
from mypackage.models import User, Product, Category
from mypackage.services import (
    UserService,
    ProductService,
    CategoryService,
)
```

### 3.3 절대 경로의 장점 ✅

#### 1. 명확성

```python
# 어느 패키지에서 가져오는지 명확
from mypackage.models.user import User
# ← mypackage의 models 패키지의 user 모듈이라는 것이 분명
```

#### 2. IDE 지원 우수

```python
# 대부분의 IDE에서 자동완성, 리팩토링, 코드 탐색 지원 우수
from mypackage.models.user import User  # ← Ctrl+Click으로 이동 가능
```

#### 3. 스크립트 직접 실행 가능

```python
# mypackage/services/user_service.py
from mypackage.models.user import User

# ✅ 직접 실행 가능
# python mypackage/services/user_service.py
```

#### 4. 프로젝트 전체 구조 파악 용이

```python
# import 문만 봐도 전체 프로젝트 구조 이해 가능
from mypackage.api.v1.endpoints.users import UserEndpoint
from mypackage.database.repositories.user_repository import UserRepository
from mypackage.services.auth.jwt_service import JWTService
```

### 3.4 절대 경로의 단점 ⚠️

#### 1. 패키지명 의존성

```python
# mypackage → yourpackage로 변경 시
# 모든 절대 경로 import를 수정해야 함

# ❌ 수정 전
from mypackage.models import User

# ✅ 수정 후
from yourpackage.models import User
```

#### 2. 패키지 이식성 저하

```python
# 다른 프로젝트에 복사 시 모든 import 수정 필요
from mypackage.models import User  # 패키지명이 hard-coded됨
```

#### 3. 타이핑 양 증가

```python
# 상대 경로
from .models import User

# 절대 경로 (더 김)
from mypackage.models.user import User
```

---

## 4. 비교표

### 4.1 종합 비교

| 측면 | 상대 경로 | 절대 경로 |
|------|----------|----------|
| **재사용성** | ✅ 우수 (패키지명 독립) | ❌ 나쁨 (패키지명 의존) |
| **이식성** | ✅ 우수 (복사만 하면 됨) | ❌ 나쁨 (import 수정 필요) |
| **명확성** | ⚠️ 상대적 위치 파악 필요 | ✅ 우수 (전체 경로 명시) |
| **IDE 지원** | ⚠️ 제한적 | ✅ 우수 (자동완성, 탐색) |
| **직접 실행** | ❌ 불가 | ✅ 가능 |
| **순환 참조 감지** | ✅ 명확 | ⚠️ 어려움 |
| **타이핑 양** | ✅ 짧음 | ⚠️ 김 |
| **유지보수** | ✅ 우수 (구조 변경 용이) | ⚠️ 보통 |
| **가독성 (얕은 구조)** | ✅ 우수 | ✅ 우수 |
| **가독성 (깊은 구조)** | ⚠️ 나쁨 (`....`) | ✅ 우수 |
| **프로젝트 구조 파악** | ⚠️ 어려움 | ✅ 쉬움 |
| **성능** | 동일 | 동일 |

### 4.2 사용 위치별 권장

| 위치 | 권장 방식 | 이유 |
|------|----------|------|
| `__init__.py` | ⭐ 상대 경로 | 패키지 내부 구조, 재사용성 |
| 개별 모듈 (같은 패키지) | ⚠️ 상대 경로 | 패키지 내부 응집도 |
| 개별 모듈 (다른 패키지) | ⭐ 절대 경로 | 명확성, IDE 지원 |
| 테스트 코드 | ⭐ 절대 경로 | 명확성, 직접 실행 |
| 스크립트/CLI | ⭐ 절대 경로 | 직접 실행 가능 |
| 라이브러리 내부 | ⭐ 상대 경로 | 재사용성, 이식성 |
| 애플리케이션 코드 | ⭐ 절대 경로 | 명확성, 유지보수 |

---

## 5. 사용 시나리오별 권장사항

### 5.1 시나리오 1: `__init__.py` 파일 ⭐

**권장: 상대 경로**

```python
# mypackage/__init__.py

# ✅ 권장: 상대 경로
from .models import User, Product
from .services import UserService, ProductService
from .utils import format_date, validate_email

# ❌ 비권장: 절대 경로
from mypackage.models import User, Product
from mypackage.services import UserService, ProductService
```

**이유:**
- 패키지명 변경 시 수정 불필요
- 패키지 재사용 용이
- 내부 구조가 명확

### 5.2 시나리오 2: 같은 패키지 내 모듈

**권장: 상대 경로 또는 절대 경로 (팀 컨벤션 따름)**

```python
# mypackage/models/user.py

# ✅ 옵션 1: 상대 경로 (짧고 간결)
from .product import Product
from .category import Category

# ✅ 옵션 2: 절대 경로 (명확함)
from mypackage.models.product import Product
from mypackage.models.category import Category
```

**선택 기준:**
- 라이브러리/패키지 개발: 상대 경로
- 애플리케이션 개발: 절대 경로
- 팀 컨벤션 따르기

### 5.3 시나리오 3: 다른 패키지의 모듈 ⭐

**권장: 절대 경로**

```python
# mypackage/services/user_service.py

# ✅ 권장: 절대 경로
from mypackage.models.user import User
from mypackage.utils.validators import validate_email
from mypackage.database.repositories import UserRepository

# ⚠️ 비권장: 상대 경로 (헷갈림)
from ..models.user import User
from ..utils.validators import validate_email
from ..database.repositories import UserRepository
```

**이유:**
- 어느 패키지인지 명확
- IDE 지원 우수
- 리팩토링 시 안전

### 5.4 시나리오 4: 테스트 코드 ⭐

**권장: 절대 경로**

```python
# tests/test_user_service.py

# ✅ 권장: 절대 경로
from mypackage.services.user_service import UserService
from mypackage.models.user import User

def test_create_user():
    service = UserService()
    user = User("John")
    # ...

# ❌ 비권장: 상대 경로 (테스트는 패키지 외부)
from ..mypackage.services.user_service import UserService  # 에러!
```

**이유:**
- 테스트는 패키지 외부에 위치
- 직접 실행 가능해야 함
- 명확성 중요

### 5.5 시나리오 5: CLI/스크립트 ⭐

**권장: 절대 경로**

```python
# scripts/migrate_data.py

# ✅ 권장: 절대 경로
from mypackage.database import Database
from mypackage.models import User, Product

def main():
    db = Database()
    # ...

if __name__ == "__main__":
    main()
```

**이유:**
- 스크립트는 직접 실행됨
- 상대 경로는 작동 안함

### 5.6 시나리오 6: 라이브러리 개발 ⭐

**권장: 상대 경로 (내부), 절대 경로 (외부 의존성)**

```python
# mylib/core/processor.py

# ✅ 내부 모듈: 상대 경로
from .validator import Validator
from ..utils.helpers import format_output

# ✅ 외부 라이브러리: 절대 경로 (당연)
import pandas as pd
from typing import List
```

**이유:**
- 라이브러리는 다른 프로젝트에서 재사용
- 내부 구조는 독립적이어야 함

### 5.7 시나리오 7: Django/Flask 애플리케이션 ⭐

**권장: 절대 경로**

```python
# myapp/views/user_views.py

# ✅ 권장: 절대 경로
from myapp.models import User
from myapp.services.user_service import UserService
from myapp.forms import UserForm

# ⚠️ 비권장: 상대 경로
from ..models import User
from ..services.user_service import UserService
```

**이유:**
- 애플리케이션은 명확성이 중요
- 프로젝트 구조를 한눈에 파악
- 팀 협업 시 이해 쉬움

---

## 6. 실전 예시

### 6.1 예시 1: 라이브러리 패키지 (상대 경로 중심)

```python
# mathlib/
# ├── __init__.py
# ├── core/
# │   ├── __init__.py
# │   ├── algebra.py
# │   └── calculus.py
# └── utils/
#     ├── __init__.py
#     └── helpers.py

# ============= mathlib/__init__.py =============
"""MathLib - 재사용 가능한 수학 라이브러리"""

__version__ = "1.0.0"

# ✅ 상대 경로 (패키지 내부)
from .core import Algebra, Calculus
from .utils import format_result

__all__ = ["Algebra", "Calculus", "format_result"]


# ============= mathlib/core/__init__.py =============
# ✅ 상대 경로
from .algebra import Algebra
from .calculus import Calculus

__all__ = ["Algebra", "Calculus"]


# ============= mathlib/core/algebra.py =============
# ✅ 상대 경로 (같은 패키지)
from .calculus import derivative

# ✅ 상대 경로 (상위 패키지)
from ..utils.helpers import format_result


class Algebra:
    def solve(self, x):
        result = derivative(x)
        return format_result(result)
```

**장점:**
- 패키지명 `mathlib` → `mathlib2`로 변경해도 내부 수정 불필요
- 다른 프로젝트에 복사해도 그대로 작동
- 내부 구조 변경 용이

### 6.2 예시 2: 웹 애플리케이션 (절대 경로 중심)

```python
# myapp/
# ├── __init__.py
# ├── models/
# │   ├── __init__.py
# │   └── user.py
# ├── views/
# │   ├── __init__.py
# │   └── user_views.py
# ├── services/
# │   ├── __init__.py
# │   └── user_service.py
# └── utils/
#     ├── __init__.py
#     └── validators.py

# ============= myapp/__init__.py =============
"""MyApp - 웹 애플리케이션"""

__version__ = "1.0.0"

# ✅ 상대 경로 (최상위 __init__.py)
from .models import User
from .views import UserView

__all__ = ["User", "UserView"]


# ============= myapp/views/user_views.py =============
# ✅ 절대 경로 (명확성 우선)
from myapp.models.user import User
from myapp.services.user_service import UserService
from myapp.utils.validators import validate_email


class UserView:
    def __init__(self):
        self.service = UserService()
    
    def create_user(self, name: str, email: str):
        if not validate_email(email):
            raise ValueError("Invalid email")
        
        user = User(name, email)
        return self.service.save(user)


# ============= myapp/services/user_service.py =============
# ✅ 절대 경로
from myapp.models.user import User
from myapp.database import Database


class UserService:
    def __init__(self):
        self.db = Database()
    
    def save(self, user: User):
        return self.db.save(user)
```

**장점:**
- 코드 한눈에 이해 가능
- IDE 지원 우수
- 리팩토링 안전

### 6.3 예시 3: 하이브리드 접근 (실용적)

```python
# myproject/
# ├── __init__.py
# ├── core/
# │   ├── __init__.py
# │   ├── base.py
# │   └── config.py
# ├── features/
# │   ├── __init__.py
# │   ├── auth/
# │   │   ├── __init__.py
# │   │   ├── models.py
# │   │   └── services.py
# │   └── users/
# │       ├── __init__.py
# │       ├── models.py
# │       └── services.py
# └── utils/
#     ├── __init__.py
#     └── helpers.py

# ============= myproject/__init__.py =============
# ✅ 상대 경로 (패키지 루트)
from .core import Config
from .utils import helpers

__all__ = ["Config", "helpers"]


# ============= myproject/features/auth/__init__.py =============
# ✅ 상대 경로 (피처 패키지 내부)
from .models import AuthUser
from .services import AuthService

__all__ = ["AuthUser", "AuthService"]


# ============= myproject/features/auth/services.py =============
# ✅ 상대 경로 (같은 피처)
from .models import AuthUser

# ✅ 절대 경로 (다른 피처/모듈)
from myproject.core.base import BaseService
from myproject.utils.helpers import hash_password
from myproject.features.users.models import User


class AuthService(BaseService):
    def authenticate(self, username: str, password: str):
        hashed = hash_password(password)
        # ...
```

**규칙:**
- `__init__.py`: 상대 경로
- 같은 피처/모듈 내: 상대 경로
- 다른 피처/모듈: 절대 경로
- 공통 유틸리티: 절대 경로

---

## 7. 흔한 실수와 해결방법

### 7.1 실수 1: `__init__.py`에서 절대 경로 사용

#### ❌ 나쁜 예

```python
# mypackage/__init__.py

from mypackage.models import User  # ❌ 절대 경로
from mypackage.services import UserService
```

**문제:**
- 패키지명 변경 시 수정 필요
- 재사용성 저하

#### ✅ 좋은 예

```python
# mypackage/__init__.py

from .models import User  # ✅ 상대 경로
from .services import UserService
```

### 7.2 실수 2: 스크립트에서 상대 경로 사용

#### ❌ 나쁜 예

```python
# scripts/migrate.py

from ..mypackage.models import User  # ❌ 에러!
```

**에러:**
```
ValueError: attempted relative import beyond top-level package
```

#### ✅ 좋은 예

```python
# scripts/migrate.py

from mypackage.models import User  # ✅ 절대 경로

# 또는 sys.path 조정
import sys
from pathlib import Path
sys.path.insert(0, str(Path(__file__).parent.parent))

from mypackage.models import User
```

### 7.3 실수 3: 너무 많은 점 사용

#### ❌ 나쁜 예

```python
# mypackage/api/v1/endpoints/users/create.py

from ......models.user import User  # ❌ 6개의 점!
from .....services.user_service import UserService
```

**문제:**
- 가독성 극악
- 유지보수 어려움

#### ✅ 좋은 예

```python
# mypackage/api/v1/endpoints/users/create.py

from mypackage.models.user import User  # ✅ 절대 경로로
from mypackage.services.user_service import UserService
```

**규칙:** 3개 이상의 점이면 절대 경로로 전환 고려

### 7.4 실수 4: 혼용으로 인한 혼란

#### ❌ 나쁜 예

```python
# 파일 내에서 일관성 없이 혼용
from .models import User  # 상대 경로
from mypackage.services import UserService  # 절대 경로
from ..utils import helpers  # 상대 경로
```

#### ✅ 좋은 예

```python
# 일관성 있게 사용
from mypackage.models import User
from mypackage.services import UserService
from mypackage.utils import helpers
```

### 7.5 실수 5: 순환 참조 미감지

#### ❌ 나쁜 예

```python
# mypackage/models.py
from mypackage.services import validate  # (1)

class User:
    pass

# mypackage/services.py
from mypackage.models import User  # (2)

def validate(user: User):
    pass
```

**문제:** `ImportError: cannot import name ...`

#### ✅ 해결 방법 1: 지연 import

```python
# mypackage/models.py
class User:
    def validate(self):
        from mypackage.services import validate  # 함수 내부로
        return validate(self)
```

#### ✅ 해결 방법 2: TYPE_CHECKING

```python
# mypackage/services.py
from typing import TYPE_CHECKING

if TYPE_CHECKING:
    from mypackage.models import User  # 타입 체크용만

def validate(user: "User"):  # 문자열로 타입 힌트
    pass
```

#### ✅ 해결 방법 3: 구조 개선

```python
# 공통 인터페이스를 별도 모듈로
# mypackage/interfaces.py
from typing import Protocol

class UserProtocol(Protocol):
    name: str
    email: str

# mypackage/services.py
from mypackage.interfaces import UserProtocol

def validate(user: UserProtocol):
    pass
```

---

## 8. 베스트 프랙티스

### 8.1 Golden Rules (황금 규칙)

#### 규칙 1: `__init__.py`는 항상 상대 경로 ⭐

```python
# ✅ ALWAYS
from .module import Class

# ❌ NEVER
from package.module import Class
```

#### 규칙 2: 같은 패키지 내는 상대 경로 또는 절대 경로 (팀 컨벤션)

```python
# ✅ 옵션 1: 상대 경로
from .other_module import Class

# ✅ 옵션 2: 절대 경로
from package.subpackage.other_module import Class
```

#### 규칙 3: 다른 패키지는 절대 경로 ⭐

```python
# ✅ ALWAYS
from package.other_package.module import Class

# ⚠️ 가능하지만 비권장
from ..other_package.module import Class
```

#### 규칙 4: 테스트/스크립트는 절대 경로 ⭐

```python
# ✅ ALWAYS
from package.module import Class
```

#### 규칙 5: 3개 이상의 점이면 절대 경로로

```python
# ❌ 나쁜 예
from ....module import Class

# ✅ 좋은 예
from package.module import Class
```

### 8.2 팀 컨벤션 예시

#### 컨벤션 A: 라이브러리 스타일

```python
# 규칙:
# - __init__.py: 상대 경로
# - 모든 내부 모듈: 상대 경로
# - 외부 라이브러리만 절대 경로

# mylib/__init__.py
from .core import Engine
from .utils import helpers

# mylib/core/processor.py
from .validator import Validator
from ..utils.helpers import format_output
```

#### 컨벤션 B: 애플리케이션 스타일

```python
# 규칙:
# - __init__.py: 상대 경로
# - 모든 애플리케이션 코드: 절대 경로
# - 명확성 우선

# myapp/__init__.py
from .models import User

# myapp/views/user_views.py
from myapp.models.user import User
from myapp.services.user_service import UserService
```

#### 컨벤션 C: 하이브리드 스타일 (추천)

```python
# 규칙:
# - __init__.py: 상대 경로
# - 같은 서브패키지: 상대 경로
# - 다른 서브패키지: 절대 경로

# myapp/__init__.py
from .core import Config

# myapp/features/auth/services.py
from .models import AuthUser  # 같은 auth 패키지
from myapp.core.base import BaseService  # 다른 패키지
from myapp.utils.helpers import hash_password
```

### 8.3 체크리스트

#### 새 패키지 작성 시

- [ ] `__init__.py`에서 상대 경로 사용했는가?
- [ ] `__all__`을 정의했는가?
- [ ] import 스타일이 일관성 있는가?
- [ ] 순환 참조가 없는가?
- [ ] 테스트 코드에서 절대 경로를 사용했는가?

#### 코드 리뷰 시

- [ ] `__init__.py`에서 절대 경로 사용했는가? (❌)
- [ ] 3개 이상의 점을 사용했는가? (❌)
- [ ] 같은 파일에서 혼용했는가? (❌)
- [ ] 스크립트에서 상대 경로 사용했는가? (❌)

---

## 9. 요약

### 9.1 간단 요약

| 상황 | 사용 방식 |
|------|----------|
| `__init__.py` | ⭐ 상대 경로 |
| 같은 패키지 내 | 상대 경로 또는 절대 경로 |
| 다른 패키지 | ⭐ 절대 경로 |
| 테스트/스크립트 | ⭐ 절대 경로 |
| 라이브러리 개발 | 상대 경로 중심 |
| 애플리케이션 개발 | 절대 경로 중심 |

### 9.2 핵심 원칙

1. **`__init__.py`는 항상 상대 경로**
2. **외부로 나갈 때는 절대 경로**
3. **일관성 유지가 가장 중요**
4. **팀 컨벤션을 따르기**
5. **3개 이상 점이면 절대 경로로**

### 9.3 최종 권장사항

**라이브러리 개발:**
```python
# ✅ 상대 경로 중심 (재사용성)
from .module import Class
```

**애플리케이션 개발:**
```python
# ✅ 절대 경로 중심 (명확성)
from myapp.module import Class
```

**하이브리드 (실용적):**
```python
# __init__.py: 상대 경로
from .module import Class

# 개별 모듈: 절대 경로 (다른 패키지)
from myapp.other_package import Class
```

---

## 10. 참고 자료

### 공식 문서
- [PEP 328 - Imports: Multi-Line and Absolute/Relative](https://www.python.org/dev/peps/pep-0328/)
- [Python Modules Documentation](https://docs.python.org/3/tutorial/modules.html)
- [Real Python - Absolute vs Relative Imports](https://realpython.com/absolute-vs-relative-python-imports/)

### 관련 PEPs
- **PEP 8**: Style Guide for Python Code
- **PEP 328**: Imports: Multi-Line and Absolute/Relative
- **PEP 366**: Main Module Explicit Relative Imports

---

**이 문서가 도움이 되셨나요? 피드백을 환영합니다!**

Copyright (c) 2024 VCANUS. All rights reserved.

