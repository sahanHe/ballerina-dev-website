---
title: 'Securely interact with internal/external services'
description: Ballerina backends can securely call services with the necessary security features such as client-side OAuth2, mutual TLS, and JWT-encapsulated user data.
url: 'https://github.com/SasinduDilshara/BFF-Samples/tree/dev/ballerina_microservices_jwt_asgardio'
---
```
service /logistics on new http:Listener(9090) {
    resource function post cargos(Cargo cargo) returns Cargo|error {
        cargoTable.add(cargo);
        http:Client serviceClient = check new ("http://localhost:9094", auth = [{
                    tokenUrl: issuer,
                    clientId: audience,
                    clientSecret: clientSecret,
                    scopes: ["cargo_read"]
                }],
            secureSocket = {
                key: {
                    certFile: "../resource/path/to/public.crt",
                    keyFile: "../resource/path/to/private.key"
                },
                cert: "./resources/public.cer"
            }
        );
        http:Response res = check serviceClient->post("/shipments", cargo);
        return cargo;
    }
}
```