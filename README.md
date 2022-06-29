# gRPC Errors - A handy guide to gRPC errors.

This repository contains code examples in different languages which demonstrate handling errors in gRPC.

Check the [`hello.proto`](hello.proto) file to see the gRPC method definitions. It has two methods `SayHello` and `SayHelloStrict`:

    func SayHello(name) {
        return "Hey, (name)!"
    }

`SayHelloStrict` is similar, but throws an error if the length of name is more than 10 characters.

Each language directories have instructions to generate gRPC methods in respective languages. I assume that you have done the basic [tutorials](http://www.grpc.io/docs/quickstart/).

## Guide

Check this page for quick guide and examples of all languages - [gRPC Errors](http://avi.im/grpc-errors)

## System Requirements
    
- [gRPC](https://github.com/grpc/grpc/blob/master/INSTALL.md)
- [protobuf compiler](https://github.com/google/protobuf)

## License

The mighty MIT license. Please check `LICENSE` for more details.


===


$ grpcurl -vv -plaintext -d '{"Name": "sssssssssssssssssss"}' --proto hello.proto 127.0.0.1:50051 hello.HelloService/SayHelloStrict

Resolved method descriptor:
// Strict Version responds only to requests which have `Name` length
// less than 10 characters
rpc SayHelloStrict ( .hello.HelloReq ) returns ( .hello.HelloResp );

Request metadata to send:
(empty)

Response headers received:
(empty)

Response trailers received:
content-type: application/grpc
Sent 1 request and received 0 responses
ERROR:
Code: InvalidArgument
Message: Length of `Name` cannot be more than 10 characters

---

$ grpcurl -vv -plaintext -d '{"Name": "sssssssssssssssssss"}' --proto hello.proto 127.0.0.1:50051 hello.HelloService/SayHelloCustomErr

Resolved method descriptor:
rpc SayHelloCustomErr ( .hello.HelloReq ) returns ( .hello.HelloResp );

Request metadata to send:
(empty)

Response headers received:
(empty)

Response trailers received:
content-type: application/grpc
Sent 1 request and received 0 responses
ERROR:
Code: Code(88)
Message: CUSTOM_ERROR

---
in node (use grpc)
$ node client.js
(node:17577) DeprecationWarning: grpc.load: Use the @grpc/proto-loader module with grpc.loadPackageDefinition instead
88 undefined: CUSTOM_ERROR
88

---

in node2 (use @grpc/grpc-js)

$ node client.js
2 UNKNOWN: CUSTOM_ERROR
2
