# How to do custom jwt auth in GRPC with Rust and Flutter

## Rust service
https://github.com/hyperium/tonic/blob/master/examples/src/interceptor/server.rs

```rust
/// This function will get called on each inbound request, if a `Status`
/// is returned, it will cancel the request and return that status to the
/// client.
fn intercept(mut req: Request<()>) -> Result<Request<()>, Status> {
    println!("Intercepting request: {:?}", req);

    let metadata = req.metadata();
    let jwt: &str = metadata.get("jwt").unwrap().to_str().unwrap().into();
    println!("The JWT is: {:?}", jwt);

    // Set an extension that can be retrieved by `say_hello`
    req.extensions_mut().insert(MyExtension {
        // we can do a parse to get the email from the request
        // then sent it to other rpcs in this file
        email: "bababa".to_string(),
    });

    return Ok(req);
    // return Err(Status::invalid_argument("jwt is invalid"));
}

struct MyExtension {
    jwt: String,
}

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let address_string = "0.0.0.0:40051";
    let addr = address_string.parse()?;

    let current_users = Arc::new(Mutex::new(Vec::new()));

    let greeter = MyGreeter {};

    // See examples/src/interceptor/client.rs for an example of how to create a
    // named interceptor that can be returned from functions or stored in
    // structs.
    let svc = GreeterServer::with_interceptor(greeter, intercept);

    println!("Server is running on http://{} ...", address_string);

    Server::builder().add_service(svc).serve(addr).await?;

    Ok(())
}
```

## Flutter client

https://github.com/grpc/grpc-dart/blob/master/example/metadata/lib/src/client.dart

```dart
class JWTGrpcControllr extends GetxController {
  ClientChannel channel = ClientChannel(
    hostIPAddress,
    port: portNumber,
    options: const ChannelOptions(credentials: ChannelCredentials.insecure()),
  );

  String jwt = "a fake jwt";

  CallOptions getJWTCallOptionsForGRPC() {
    return CallOptions(
      metadata: <String, String>{
        'jwt': jwt,
      },
    );
  }

  void recreateChannel() {
    channel = ClientChannel(
      hostIPAddress,
      port: portNumber,
      options: const ChannelOptions(credentials: ChannelCredentials.insecure()),
    );
  }

  Future<void> test() async {
    recreateChannel();

    try {
      final stub = GreeterClient(channel);
      final response = await stub.sayHello(HelloRequest()..name = 'you',
          options: getJWTCallOptionsForGRPC());
      print('Greeter client received: ${response.message}');
      await channel.shutdown();
    } catch (e) {
      print(e);
    }
  }
}
```