---
description: Testing Standards using Pytest (Patterns & Fixtures)
---

# Skill: Testing Standard

**Goal**: Verify behavior, prevent regressions, and document usage via tests.

## The AAA Pattern (Arrange, Act, Assert)

Structure every test using this pattern.

```python
def test_calculate_total_with_discount():
    # 1. Arrange (Setup)
    price = 100.0
    quantity = 2
    discount = 0.1

    # 2. Act (Execution)
    result = calculate_total(price, quantity, discount)

    # 3. Assert (Verification)
    assert result == 180.0
```

## Fixtures (Clean Setup)

Use `conftest.py` for shared resources.

```python
# tests/conftest.py
import pytest
from src.models import User

@pytest.fixture
def mock_user():
    return User(name="Test User", email="test@example.com")
```

## Mocking (Isolating Logic)

Use `unittest.mock` to fake external dependencies (APIs, DBs).

```python
from unittest.mock import Mock

def test_send_notification(mocker):
    # Arrange
    mock_api = Mock()
    service = NotificationService(api=mock_api)

    # Act
    service.send("user@example.com", "Hello!")

    # Assert
    mock_api.send_email.assert_called_once_with(
        to="user@example.com", body="Hello!"
    )
```

## Rules
1.  **Unit Tests**: Test one class/function in isolation. Fast (<10ms).
2.  **Integration Tests**: Test database/API interactions. Slow. Mark with `@pytest.mark.integration`.
3.  **No Logic in Tests**: Tests should be dumb. If a test has an `if` statement, it fails.
