---
description: Python Coding Standards (Formatting, Typing, Style)
---

# Skill: Python Coding Standard

**Goal**: Write Python code that is readable, maintainable, and robust.

## 1. Type Hinting (Non-Negotiable)

Every function signature must be typed.

### ✅ Good
```python
def calculate_total(price: float, quantity: int, discount: float = 0.0) -> float:
    """Calculate total price after discount."""
    return (price * quantity) * (1 - discount)
```

### ❌ Bad
```python
def calculate_total(price, qty, disc):
    return (price * qty) * (1 - disc)
```

## 2. Naming Conventions (PEP 8)

| Element          | Convention      | Example                    |
|------------------|-----------------|----------------------------|
| Functions        | `snake_case`    | `calculate_risk_score()`   |
| Variables        | `snake_case`    | `total_volume`             |
| Classes          | `PascalCase`    | `RiskAnalyzer`             |
| Constants        | `UPPER_CASE`    | `MAX_RETRY_COUNT`          |
| Private members  | `_leading`      | `_internal_cache`          |
| Files            | `snake_case`    | `risk_calculator.py`       |

**Rules**:
*   Use descriptive names (`get_user_balance` not `get_ub`).
*   Boolean variables should be questions (`is_active`, `has_permission`).

## 3. File Organization

Structure your files logically. Imports **MUST** be sorted: Standard -> Third Party -> Local.

```python
"""
module_name.py
Description of the module's purpose.
"""

# 1. Imports (Standard)
import logging
import os
from typing import Optional

# 2. Imports (Third Party)
import pandas as pd
from pydantic import BaseModel

# 3. Imports (Local)
from src.models import Trade
from src.utils import config

# 4. Constants
MAX_RETRIES = 3

# 5. Classes / Functions
class Calculator:
    ...
```

## 4. Complexity Guardrails

*   **File Size**: < 300 lines (Hard limit). Partition if larger.
*   **Function Size**: < 30 lines. Single responsibility.
*   **Indentation**: Max 3 levels deep.
*   **Early Return**: Avoid `else` blocks.

```python
# Bad
if user:
    if user.is_active:
        perform_action()

# Good
if not user or not user.is_active:
    return
perform_action()
```

## 5. Error Handling & Logging

*   **Log, Don't Print**: Use `logging` module.
*   **No Bare Except**: Never use `except:` without capturing context.

```python
import logging
logger = logging.getLogger(__name__)

def fetch_data(url: str):
    logger.debug("Fetching %s", url)
    try:
        data = request.get(url)
    except RequestError as e:
        logger.error("Failed to fetch %s: %s", url, e)
        raise  # Re-raise or wrap in domain exception
```

## 6. Docstrings (Google Style)

Mandatory for all public functions/classes.

```python
def fetch_data(symbol: str, limit: int = 100) -> pd.DataFrame:
    """
    Fetch historical data for a symbol.

    Args:
        symbol: The trading pair (e.g., 'BTCUSDT').
        limit: Number of rows to return.

    Returns:
        pd.DataFrame: OHLCV data.

    Raises:
        ConnectionError: If API is unreachable.
    """
```
