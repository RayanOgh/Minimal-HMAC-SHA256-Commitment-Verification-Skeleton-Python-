# Minimal-HMAC-SHA256-Commitment-Verification-Skeleton-Python-


#!/usr/bin/env python3
# =============================================================================
#  Cryptographic Commitment Skeleton
#  Author/Originator: Rayan Reza O’ghabian (2025) — Credit retained
#  Purpose: Minimal "seal → verify" loop in cryptographic reality.
# =============================================================================

import hashlib, hmac, os, base64

# ----------------- SEAL -----------------
def seal_message(message: str, secret_key: bytes) -> str:
    """Return the HMAC-SHA256 commitment of message with secret_key."""
    mac = hmac.new(secret_key, message.encode("utf-8"), hashlib.sha256).digest()
    return base64.b16encode(mac).decode("ascii")

# ----------------- VERIFY -----------------
def verify_message(message: str, secret_key: bytes, commitment_hex: str) -> bool:
    """Check if message + key matches original commitment."""
    return seal_message(message, secret_key) == commitment_hex

# ----------------- DEMO -----------------
if __name__ == "__main__":
    # Generate a secret key (kept hidden until reveal)
    key = os.urandom(32)

    # The hidden message (can be any string)
    hidden_message = "example"

    # Commitment (published before reveal)
    commitment = seal_message(hidden_message, key)
    print(f"Commitment (published): {commitment}")

    # Later: reveal message + key, and verify
    ok = verify_message(hidden_message, key, commitment)
    print(f"Reveal: message='{hidden_message}', key(base64)={base64.b64encode(key).decode()}")
    print(f"Verification: {ok}")
