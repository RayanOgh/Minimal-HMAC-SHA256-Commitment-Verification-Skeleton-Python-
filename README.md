# Minimal HMAC-SHA256 Commitment Verification Skeleton (Python)

A minimal demonstration of cryptographic sealing and verification using **HMAC-SHA256**.  
This simple skeleton shows how to:

1. **Seal** a message with a secret key (commitment).  
2. **Verify** the message and key against the original commitment.  

---

## Author
**Rayan Reza O’ghabian (2025)**

---

# Minimal HMAC-SHA256 Commitment

Author: Rayan Reza O’ghabian (2025)

---

## Code

```python
#!/usr/bin/env python3
import hmac, hashlib, os

ALGO = "HMAC-SHA256"
CONTEXT = b"commitment:v1"  # domain separation

def seal(message: str, key: bytes) -> str:
    data = CONTEXT + message.encode("utf-8")
    return hmac.new(key, data, hashlib.sha256).hexdigest()

def verify(message: str, key: bytes, commitment: str) -> bool:
    expected = seal(message, key)
    return hmac.compare_digest(expected, commitment)

if __name__ == "__main__":
    key = os.urandom(32)          # keep this secret until reveal
    hidden_word = "example"       # your committed message

    commitment = seal(hidden_word, key)
    print("Algorithm:", ALGO)
    print("Commitment:", commitment)

    # Later: reveal `hidden_word` and hex(key) (or base64)
    ok = verify(hidden_word, key, commitment)
    print("Verification:", ok)
