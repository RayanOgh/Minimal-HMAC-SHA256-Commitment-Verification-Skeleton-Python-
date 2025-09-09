# Minimal HMAC-SHA256 Commitment Verification Skeleton (Python)

A minimal demonstration of cryptographic sealing and verification using **HMAC-SHA256**.  
This simple skeleton shows how to:

1. **Seal** a message with a secret key (commitment).  
2. **Verify** the message and key against the original commitment.  

---

## Author
**Rayan Reza O’ghabian (2025)**

---

## Code

```python
#!/usr/bin/env python3
import hmac, hashlib, os

def seal(message: str, key: bytes) -> str:
    """Return the HMAC-SHA256 commitment of a message with secret key."""
    return hmac.new(key, message.encode(), hashlib.sha256).hexdigest()

def verify(message: str, key: bytes, commitment: str) -> bool:
    """Check if message + key matches the original commitment."""
    return seal(message, key) == commitment

if __name__ == "__main__":
    # Generate a random secret key
    key = os.urandom(32)

    # Hidden message (replace with any string)
    hidden_word = "example"

    # Commitment (published before reveal)
    commitment = seal(hidden_word, key)
    print("Commitment:", commitment)

    # Later: verify message + key
    ok = verify(hidden_word, key, commitment)
    print("Verification:", ok)
