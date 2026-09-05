# Link Matrix to your ATProto identity manually

Venoom can link your Matrix and ATProto identities for you, but doing that requires the ATProto `identity:*` permission. That permission allows changes to your DID document and is broader than what is strictly needed just to add a Matrix account.

You don't have to give Venoom this permission.

If you manage your ATProto identity yourself, you can create the link manually.

## 1. Add Matrix to your ATProto DID

Find your Matrix user ID:

    @alice:example.com

Convert it to a Matrix URI:

    matrix:u/alice:example.com

Add that URI to `alsoKnownAs` in your ATProto DID document, while keeping your existing ATProto handle:

    "alsoKnownAs": [
      "at://alice.example.com",
      "matrix:u/alice:example.com"
    ]

How you publish this change depends on your DID:

- `did:web`: edit and publish your DID document yourself.
- Self-managed `did:plc`: publish a PLC operation using your rotation key.
- PDS-managed `did:plc`: use your PDS's identity/PLC tooling to make the change.

The end result should be:

    Your ATProto DID
           │
           └── alsoKnownAs
                 └── matrix:u/alice:example.com

## 2. Add your ATProto DID to Matrix

The link also needs to point the other way.

On your Matrix profile, set the Matey/extended-profile field used for your ATProto identity to your DID:

    did:plc:xxxxxxxxxxxxxxxxxxxxxxxx

This can be done with any Matrix client/tool that supports editing the required extended profile field, or directly through the Matrix Client-Server API.

The result is:

    Matrix @alice:example.com
           │
           └── ATProto DID
                 └── did:plc:xxxxxxxxxxxxxxxxxxxxxxxx

## 3. Verification

Venoom can now verify the relationship instead of having to trust either side on its own:

    ATProto DID
        │
        └── says → matrix:u/alice:example.com
                         ↑
                         │
    Matrix profile ──────┘
        says → did:plc:xxxxxxxxxxxxxxxxxxxxxxxx

If both sides point to each other, the identities are linked.

Venoom does not need your `identity:*` permission to verify an existing link. That permission is only needed if you want Venoom to make the ATProto DID change for you.
