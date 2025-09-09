# Minimal-HMAC-SHA256-Commitment-Verification-Skeleton-Python-


#!/usr/bin/env python3
# Author: Rayan Reza O’ghabian (2025)

import hmac, hashlib, os

def seal(message: str, key: bytes) -> str:
    return hmac.new(key, message.encode(), hashlib.sha256).hexdigest()

def verify(message: str, key: bytes, commitment: str) -> bool:
    return seal(message, key) == commitment

if __name__ == "__main__":
    key = os.urandom(32)  # secret key
    hidden_word = "example"  # replace with any word

    commitment = seal(hidden_word, key)
    print("Commitment:", commitment)

    ok = verify(hidden_word, key, commitment)
    print("Verification:", ok)

