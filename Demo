"""
UltraToken Decoder Demo
----------------------

A simple decoder for compact, shareable UltraToken strings (zlib + urlsafe base64),
with a showcase of diverse test cases.

Usage:
    python ultratoken_demo.py         # Decodes and prints all sample tokens
    python ultratoken_demo.py TOKEN   # Decodes and prints your custom token

You may use or adapt this file as you wish.
"""

import base64
import zlib
import json
import sys

def decode_ultratoken(token: str) -> dict:
    """
    Decodes an UltraToken string (zlib + urlsafe base64, no padding).
    Returns the original Python dict/object.
    """
    padded_token = token + "=" * (-len(token) % 4)
    compressed_bytes = base64.urlsafe_b64decode(padded_token)
    json_bytes = zlib.decompress(compressed_bytes)
    return json.loads(json_bytes.decode())

SAMPLES = [
    # Each entry: (label, token, expected output as comment)
    ("Short plain text",
     "eNorzUssKcrMS1fISaxQ0lEqTgUAeFsGHQ==",
     # {'msg': 'hello world'}
    ),
    ("Numbers and booleans",
     "eNorzUssKcrMS1fISaxQ0lEqzszPyM8FyAIAyXkHRw==",
     # {'a': 123, 'b': True, 'c': None}
    ),
    ("List of values",
     "eNorzUssKcrMS1fISaxQ0lEqy0xRSEksyczPz0vNT1EoSi0CAHYPCnA=",
     # {'items': [1, 2, 3, 4, 5, "end"]}
    ),
    ("Nested dictionary",
     "eNorzUssKcrMS1fISaxQ0lEqLMlM0TU1szQyNjU3AwCH2QvB",
     # {'user': {'id': 9, 'info': {'active': True, 'score': 99}}}
    ),
    ("Long text / full sentence",
     "eNorzUssKcrMS1fISaxQ0lEqzs/TS8xJ8dQzXHUISU1LLUnMS6xOLMnMTS1RKE4sSsxJLEkFAMF+CGI=",
     # {'sentence': 'UltraToken compresses and shares this sentence.'}
    ),
    ("Special characters & emoji",
     "eNorzUssKcrMS1fISaxQ0lEqy0vOT8vVSM3Lz0yxLzEv1VfIz03NzwUAxyQJGA==",
     # {'fun': 'Try symbols! @#%🚀'}
    ),
    ("Multi-field object",
     "eNorzUssKcrMS1fISaxQ0lEqSk3Mzk7XUkgpzCspzA0syiwoySspzMsFAKUCBwI=",
     # {'x': 12, 'y': -8, 'z': 0, 'status': 'ok'}
    ),
    ("Large array (short demo)",
     "eNrLT8vMUbJSKE5NBQAA2AIG",
     # {'arr': [0,1,2,3,4,5,6,7,8,9]}
    ),
    ("Original test case",
     "eNqrVsrLL0lVslIKSS0uycxLVwjNKSlKDMnPTs1TSM1L0S3J1wVSSjpKeaW5SlbmtQCdCRB0",
     # {'note': 'Testing UltraToken end-to-end', 'num': 7}
    ),
]

def main():
    if len(sys.argv) == 2:
        # Decode user-supplied token
        token = sys.argv[1]
        try:
            result = decode_ultratoken(token)
            print(f"Decoded token:\n{json.dumps(result, indent=2, ensure_ascii=False)}")
        except Exception as e:
            print(f"Failed to decode token: {e}")
    else:
        # Demo: decode all samples
        print("UltraToken Decoder Demo\n" + "-"*26)
        for label, token, *_ in SAMPLES:
            print(f"\n{label}:\nToken: {token}")
            try:
                result = decode_ultratoken(token)
                print("Decoded:", json.dumps(result, ensure_ascii=False))
            except Exception as e:
                print("Error decoding:", e)

if __name__ == "__main__":
    main()
