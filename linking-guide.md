# Link Matrix to your ATProto identity manually

Venoom can link your Matrix account to your ATProto identity for you, but this requires the `identity:*` permission.

You do not have to give Venoom this permission. If you prefer, you can create the link yourself.

## 1. Add your Matrix account to your ATProto DID

Find your Matrix ID:

    @alice:example.com

Add it to your DID document's `alsoKnownAs` as:

    matrix:u/alice:example.com

For example:

    "alsoKnownAs": [
      "at://alice.example.com",
      "matrix:u/alice:example.com"
    ]

Keep any existing `alsoKnownAs` entries.

How you update the DID depends on how your ATProto identity is managed. If your PDS manages your `did:plc`, use its identity/PLC tooling. If you manage your DID yourself, update it through your normal DID management process.

## 2. Add your ATProto DID to Matrix

The link needs to exist on the Matrix side as well.

Add your ATProto DID to the appropriate Matey extended-profile field on your Matrix profile:

    did:plc:xxxxxxxxxxxxxxxxxxxxxxxx

You can do this with a Matrix client that supports the Matey/extended-profile field, or directly through the Matrix Client-Server API.

## 3. Done

Once both sides are set, Venoom can verify the link:

- your ATProto DID lists your Matrix account
- your Matrix profile lists your ATProto DID

Venoom does not need `identity:*` to verify this. That permission is only needed if you want Venoom to update your ATProto DID for you.
