# Protobuf

- [Protobuf](#protobuf)
  - [Basic Protobuf](#basic-protobuf)
    - [BuildPartial and partial messages](#buildpartial-and-partial-messages)

## Basic Protobuf

- Google's docs - <https://developers.google.com/protocol-buffers/docs/proto>

- message - like a class
- required
- optional
- repeated
- Map - can be made with a sub-message and then repeated
- enums - for enum entries should prefix by enum type name to ensure uniqueness (enum entries are like globals)

### BuildPartial and partial messages

- MessageLiteOrBuilder.isInitialized()
  - Checks if we have all required fields before building
  - Avoids a RUNTIME exception (UninitializedMessageException) if missing required fields.
- buildPartial() - builds a partial message, ignoring any missing required fields
