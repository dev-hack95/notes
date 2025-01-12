# Protobuf

  * Protocol buffers allow you to serialize structured data to be transmitted over a wire.

  * **Defining Message type**

  ```bash
  syntax = "proto3"; // <- protocol version
  message CreateOrderRequest {
    int64 user_id = 1; // <- owner of this order
    repeated Item items  = 2; // <- List of items for the order
    float amount = 3; // <- Total amount of odrder that should be paid 
  }
  ```

  * **FIELD RULE**

    * **singlar** : A structured message that can store only one value

    * **repeated** : A structured messsage that can store multiple values

  * **FIELD TYPES**

| **Data Type** | **Description** |
|---------------|-----------------|
| **double**    | A double-precision floating-point number. |
| **float**     | A single-precision floating-point number. |
| **int32**     | Uses variable-length encoding. Inefficient for negative numbers; use `sint32` for better efficiency with negatives. |
| **int64**     | Uses variable-length encoding. Inefficient for negative numbers; use `sint64` for better efficiency with negatives. |
| **uint32**    | Uses variable-length encoding for unsigned integers. |
| **uint64**    | Uses variable-length encoding for unsigned integers. |
| **sint32**    | Uses variable-length encoding. Signed integer value that efficiently encodes negative numbers compared to `int32`. |
| **sint64**    | Uses variable-length encoding. Signed integer value that efficiently encodes negative numbers compared to `int64`. |
| **fixed32**   | Always four bytes. More efficient than `uint32` if values are often greater than 2^28. |
| **fixed64**   | Always eight bytes. More efficient than `uint64` if values are often greater than 2^56. |
| **sfixed32**  | Always four bytes for signed fixed integers. |
| **sfixed64**  | Always eight bytes for signed fixed integers. |
| **bool**      | Represents a boolean value (true or false). |
| **string**    | A UTF-8 encoded or 7-bit ASCII text string, cannot exceed \(2^{32}\) characters in length. |
| **bytes**     | May contain any arbitrary sequence of bytes, cannot exceed \(2^{32}\) in length. |

