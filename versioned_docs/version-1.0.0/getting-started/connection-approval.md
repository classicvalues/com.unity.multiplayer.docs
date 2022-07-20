---
id: connection-approval
title: Connection Approval
---

With every new connection,  Netcode for GameObjects (Netcode) performs a handshake in addition to handshakes done by the transport. This is to ensure that the `NetworkConfig`s match between the Client and Server. In the `NetworkConfig`, you can specify to enable `ConnectionApproval`. 

Connection approval allows you to decide on a per connection basis if the connection should be allowed. Connection approval also enables you to specify the player prefab to be created, allowing you to override the default behaviour on a per player basis.

## Callback for approval logic

When `ConnectionApproval` is `true`, you are also required to provide a callback where you put your approval logic inside. `ConnectionApprovalCallback` is called by the Client host.

Server-only example:

```csharp
using Unity.Netcode;
using Unity.Netcode.Spawning;

private void Setup() 
{
    NetworkManager.Singleton.ConnectionApprovalCallback += ApprovalCheck;
    NetworkManager.Singleton.StartHost();
}

private void ApprovalCheck(byte[] connectionData, ulong clientId, MLAPI.NetworkManager.ConnectionApprovedDelegate callback)
{
    //Your logic here
    bool approve = true;
    bool createPlayerObject = true;

    // The prefab hash. Use null to use the default player prefab
    // If using this hash, replace "MyPrefabHashGenerator" with the name of a prefab added to the NetworkPrefabs field of your NetworkManager object in the scene
    ulong? prefabHash = NetworkSpawnManager.GetPrefabHashFromGenerator("MyPrefabHashGenerator");
    
    //If approve is true, the connection gets added. If it's false. The client gets disconnected
    callback(createPlayerObject, prefabHash, approve, positionToSpawnAt, rotationToSpawnWith);
}
```

## Connection data

The `connectionData` parameter takes any custom data of your choice that the client should send to the server. Usually, this data should be some sort of ticket, room password, or similar that will decide if a connection should be approved or not. The `connectionData` is specified on the Client-side in the `NetworkingConfig` supplied when connecting.

Example:

```csharp
using Unity.Netcode;

NetworkManager.Singleton.NetworkConfig.ConnectionData = System.Text.Encoding.ASCII.GetBytes("room password");
NetworkManager.Singleton.StartClient();
```

The `ConnectionData` will then be passed to the server and it will decide if the client will be approved or not.

## Timeout

Netcode uses a callback system in order to allow for external validation. For example, you might have a steam authentication ticket sent as the `ConnectionData` that you want to validate against steams servers. This can take some time. If you don't call the callback method within the time specified in the `ClientConnectionBufferTimeout` configuration the connection will be dropped. This time starts counting when the transport has told  Netcode about the connection. This means that you cannot attack  Netcode by never sending the buffer, it will still time you out.

## Security

If connection approval is enabled. Any messages sent before a connection is setup are silently ignored.

### Connection data security

The connection data is not encrypted or authenticated. 

:::important
A man in the middle attack can be done. It is strongly suggested to not send authentication tokens such as steam tickets or user passwords over connection approval.
:::