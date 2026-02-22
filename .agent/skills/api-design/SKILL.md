---
description: Design RESTful APIs using FastAPI and Pydantic (Few-Shot Examples)
---

# Skill: API Design

**Goal**: Build consistent, type-safe, and self-documenting REST APIs.

## The Gold Standard (Canonical Example)

Use this pattern for ALL endpoints.

```python
"""api/v1/users.py: User management endpoints."""
from fastapi import APIRouter, Depends, HTTPException, status
from pydantic import BaseModel, Field

# 1. API Router (Always versioned)
router = APIRouter(prefix="/users", tags=["users"])

# 2. Schemas (Request vs Response)
class UserCreate(BaseModel):
    """Schema for creating a user."""
    username: str = Field(..., min_length=3, description="Unique username")
    email: str = Field(..., description="Valid email address")

class UserResponse(BaseModel):
    """Schema for user response (Public data only)."""
    id: int
    username: str
    email: str
    class Config:
        from_attributes = True  # ORM compatibility

# 3. Dependency Injection (Service Layer)
def get_user_service():
    # ... import logic ...
    pass

# 4. The Endpoint (Thin Controller)
@router.post(
    "/",
    response_model=UserResponse,
    status_code=status.HTTP_201_CREATED,
    summary="Create a new user"
)
async def create_user(
    user_in: UserCreate,
    service: UserService = Depends(get_user_service)
):
    """
    Create a new user in the system.

    - **user_in**: The user data (username, email)
    - **Returns**: The created user with ID
    """
    try:
        # Delegate logic to Service
        return service.create(user_in)
    except ValueError as e:
        # Map Domain Errors to HTTP Errors
        raise HTTPException(
            status_code=status.HTTP_400_BAD_REQUEST,
            detail=str(e)
        )
```

## Anti-Patterns (What NOT to do)

### ❌ 1. Logic in Controller
```python
@router.post("/")
async def create_user(user: UserCreate):
    # BAD: Direct DB access in route
    db.execute("INSERT INTO users ...")
    return {"status": "ok"}
```
> **Correction**: Move all DB logic to `services/user_service.py`.

### ❌ 2. Mixed Schemas
```python
# BAD: Using DB Model as Schema
def get_user(id: int) -> UserModel:
    return db.get(id)
```
> **Correction**: Always return Pydantic `Response` models to prevent leaking internal fields (like password hashes).

### ❌ 3. Vague Errors
```python
except Exception:
    return {"error": "Something went wrong"} # BAD
```
> **Correction**: Raise specific `HTTPException` with status codes (404, 400, 403).

## URL Convention
*   **Collection**: `GET /api/v1/users`
*   **Resource**: `GET /api/v1/users/{id}`
*   **Action**: `POST /api/v1/users/{id}/activate` (Use verbs only for non-CRUD actions)
