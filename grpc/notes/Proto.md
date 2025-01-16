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
             A[Metadata Section] --> B[Wire Type: 000 Varint]
             A --> C[Field Number: Binary Representation]
             B --> D[Type: int]
             C --> E[Remaining Bits for Field Value]
    
             F[Data Section] --> G[MSB: Continuation Bit]
             G --> H{More Bytes?}
             H -->|No| I[End of Data]
             H -->|Yes| J[Additional Bytes Follow]
    
             F --> K[Data Value: Remaining Bits]
          ```


  * **MSB**

    * The concept of the Most Significant Bit (MSB) in the context of Protocol Buffers (protobuf)
      encoding, particularly for variable-length integers (varints), is crucial for understanding
      how data is serialized efficiently. Here’s a detailed breakdown of how the MSB is utilized
      in encoding, especially when dealing with values greater than 127.

    * Varint encoding is a method used by Protocol Buffers to serialize integers in a space-efficient
      manner. The key features of varint encoding include:

      * **Variable Length**: The number of bytes used to encode an integer can vary based on its size.
      * **Base-128 Encoding**: Each byte can store 7 bits of data, with the 8th bit (the MSB) used as
        a continuation flag.

    * **Role of the Most Significant Bit (MSB)**

      * **Continuation Indicator** :

        * The MSB indicates whether more bytes follow the current byte in the encoded integer.
        * If the MSB is 1, it signifies that there are additional bytes to come.
        * If the MSB is 0, it indicates that this is the last byte of the encoded integer.

      * **Encoding Process** :

        * When encoding an integer, the number is split into 7-bit segments.
        * Each segment is stored in a byte, with the MSB set according to whether more segments exist.


      ```mermaid
      graph TD;
          A[Decimal Value: 21567] --> B[Binary Value: 101010000111111]
          B --> C[Split into Seven-Bit Blocks]
          C --> D[Block 1: 0000001]
          C --> E[Block 2: 0101000]
          C --> F[Block 3: 0111111]
          D --> G[Add MSB: 1]
          E --> H[Add MSB: 1]
          F --> I[Add MSB: 0]
          G --> J[Reverse Order]
          H --> J
          I --> J
          J --> K[Final Order: 0111111, 0101000, 0000001]
      ```

  * **Wire's Types**

     * First three digits are the wire types and these types are used to encode the data

| **Wire Type ID** | **Binary Notation** | **Name**          | **Used For**                                                                 |
|------------------|---------------------|-------------------|------------------------------------------------------------------------------|
| 0                | `000`               | Varint            | Encodes variable-length integers, including `int32`, `int64`, `uint32`, `uint64`, `sint32`, `sint64`, `bool`, and `enum`. This type is efficient for small integers. |
| 1                | `001`               | Fixed64           | Used for fixed-length 64-bit values, such as `fixed64`, `sfixed64`, and `double`. This type is suitable when the exact size is known and fixed. |
| 2                | `010`               | Length Delimited   | Encodes length-prefixed data, including `string`, `bytes`, embedded messages, and packed repeated fields. This allows for variable-length data to be efficiently serialized. |
| 3                | `011`               | Start Group       | A deprecated wire type that was used to indicate the start of a group. It is not supported in current implementations. |
| 4                | `100`               | End Group         | A deprecated wire type that was used to indicate the end of a group. It is not supported in current implementations. |
| 5                | `101`               | Fixed32           | Used for fixed-length 32-bit values, such as `fixed32`, `sfixed32`, and `float`. This type is appropriate when the exact size is known and fixed. |
