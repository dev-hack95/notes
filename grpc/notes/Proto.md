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

  * **NOTE** :  1, 2 and 3 are unique identifier

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

  * **FILED NUMBERS**

    * Each field in a protocl buffers message gas a unique identifer know as field number, which is
      crucial for identifying the field in the binary message format

    * **Reserving Field Numbers**

      * Each fiels has a unique identifier in the message to identify the field in the binary message
        foramt.

      * Field numbers are unique idetifer for the fields, those numbers shouldn't be changed for backward
        compactibilty

      ```bash
      message User {     // initial message
        string name = 1;
        int32 age = 2;
      }

      // Addition of another varible to the User message
      message User {
        string name = 1;
        int32 age = 2;
        string email = 3; // added  new field name email
      }

      // Removal of a field
      message User {
        reserved 3; // reserving 3 to maintain the backward compactibility
        string name = 1;
        int32 age = 2;
      }
      ```        
  * **Protocol Buffer Encoding**

    * The main goal of protocol buffer encoding is to convert .proto file content into binary format
      to send over a wire. The protocol buffer compiler used a set of rules to convert message into
      binary format

      * Example

        ```bash
        // .proto file
        message ConsumerRequest {
          int64 consumer_id = 1;
        }

        // .go file conversion
        request := ConsumerRequest {
          ConsumerId : 443
        }
        ```

        * The request objext is marshalled by the protocl buffer into []byte to be able to sent
          the data over wire

        * These []byte contain the metadata and data itself.

          * **Encoding**

            * **Metadata Section**

              * Size : 1byte(8bits)

              * Purpose: Contains information about the data type and filed number.

              * Structure:

                 * First Three Bits(Wire Type)

                    * These bits denote the wire type. For example `000` represnts Variant(type 0)

                    * Remaining Five Bits:

                       * These bits contain the field number or value

            * **Data Section**

              * MSB(Most Significant Bit)

                * The first bit indicates if there are additional bytes to follow

                  * Value `0`: No additional bytes

                  * Value `1`: More bytes follow

              * Remaining Seven Bits

                * These bits are used to encode acutal data.


          ```bash
          Metadata:
          | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | (Field Number and Type)

          Data:
          | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | (MSB + Data)
          ```

          ```mermaid
          graph TD
             A[Metadata Section] --> B[Wire Type: 000 (Varint)]
             A --> C[Field Number: Binary Representation]
             B --> D[Type: int]
             C --> E[Remaining Bits for Field Value]
    
             F[Data Section] --> G[MSB: Continuation Bit]
             G --> H{More Bytes?}
             H -->|No| I[End of Data]
             H -->|Yes| J[Additional Bytes Follow]
    
             F --> K[Data Value: Remaining Bits]
          ```
