---  
id: Unity.Networking.Transport.INetworkInterface  
title: Unity.Networking.Transport.INetworkInterface  
---

<div class="markdown level0 summary">

Interface for implementing a low-level networking interface see
BaselibNetworkInterface as an example

</div>

<div class="markdown level0 conceptual">

</div>

<div class="inheritedMembers">

##### Inherited Members

<div>

IDisposable.Dispose()

</div>

</div>

##### **Namespace**: System.Dynamic.ExpandoObject

##### **Assembly**: transport.dll

##### Syntax

``` lang-csharp
public interface INetworkInterface : IDisposable
```

## 

### LocalEndPoint

<div class="markdown level1 summary">

Gets the value of the local end point

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
NetworkInterfaceEndPoint LocalEndPoint { get; }
```

#### Property Value

| Type                     | Description |
|--------------------------|-------------|
| NetworkInterfaceEndPoint |             |

## 

### Bind(NetworkInterfaceEndPoint)

<div class="markdown level1 summary">

Binds the medium to a specific endpoint.

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
int Bind(NetworkInterfaceEndPoint endpoint)
```

#### Parameters

| Type                     | Name     | Description                       |
|--------------------------|----------|-----------------------------------|
| NetworkInterfaceEndPoint | endpoint | A valid NetworkInterfaceEndPoint. |

#### Returns

| Type         | Description  |
|--------------|--------------|
| System.Int32 | 0 on Success |

### CreateInterfaceEndPoint(NetworkEndPoint, out NetworkInterfaceEndPoint)

<div class="markdown level1 summary">

Creates the interface end point using the specified address

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
int CreateInterfaceEndPoint(NetworkEndPoint address, out NetworkInterfaceEndPoint endpoint)
```

#### Parameters

| Type                     | Name     | Description  |
|--------------------------|----------|--------------|
| NetworkEndPoint          | address  | The address  |
| NetworkInterfaceEndPoint | endpoint | The endpoint |

#### Returns

| Type         | Description |
|--------------|-------------|
| System.Int32 | The int     |

### CreateSendInterface()

<div class="markdown level1 summary">

Creates the send interface

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
NetworkSendInterface CreateSendInterface()
```

#### Returns

| Type                 | Description                |
|----------------------|----------------------------|
| NetworkSendInterface | The network send interface |

### GetGenericEndPoint(NetworkInterfaceEndPoint)

<div class="markdown level1 summary">

Gets the generic end point using the specified endpoint

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
NetworkEndPoint GetGenericEndPoint(NetworkInterfaceEndPoint endpoint)
```

#### Parameters

| Type                     | Name     | Description  |
|--------------------------|----------|--------------|
| NetworkInterfaceEndPoint | endpoint | The endpoint |

#### Returns

| Type            | Description           |
|-----------------|-----------------------|
| NetworkEndPoint | The network end point |

### Initialize(INetworkParameter\[\])

<div class="markdown level1 summary">

Initializes the interfacing passing in optional INetworkParameter

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
int Initialize(params INetworkParameter[] param)
```

#### Parameters

| Type                  | Name  | Description |
|-----------------------|-------|-------------|
| INetworkParameter\[\] | param | The param   |

#### Returns

| Type         | Description |
|--------------|-------------|
| System.Int32 | The int     |

### Listen()

<div class="markdown level1 summary">

Start listening for incoming connections. This is normally a no-op for
real UDP sockets.

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
int Listen()
```

#### Returns

| Type         | Description  |
|--------------|--------------|
| System.Int32 | 0 on Success |

### ScheduleReceive(NetworkPacketReceiver, JobHandle)

<div class="markdown level1 summary">

Schedule a ReceiveJob. This is used to read data from your supported
medium and pass it to the AppendData function supplied by NetworkDriver

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
JobHandle ScheduleReceive(NetworkPacketReceiver receiver, JobHandle dep)
```

#### Parameters

| Type                  | Name     | Description                                      |
|-----------------------|----------|--------------------------------------------------|
| NetworkPacketReceiver | receiver | A NetworkDriver used to parse the data received. |
| JobHandle             | dep      | A to any dependency we might have.               |

#### Returns

| Type      | Description                                 |
|-----------|---------------------------------------------|
| JobHandle | A to our newly created ScheduleReceive Job. |

### ScheduleSend(NativeQueue\&lt;QueuedSendMessage&gt;, JobHandle)

<div class="markdown level1 summary">

Schedule a SendJob. This is used to flush send queues to your supported
medium

</div>

<div class="markdown level1 conceptual">

</div>

#### Declaration

``` lang-csharp
JobHandle ScheduleSend(NativeQueue<QueuedSendMessage> sendQueue, JobHandle dep)
```

#### Parameters

| Type                             | Name      | Description                                                |
|----------------------------------|-----------|------------------------------------------------------------|
| NativeQueue\&lt;QueuedSendMessage&gt; | sendQueue | The send queue which can be used to emulate parallel send. |
| JobHandle                        | dep       | A to any dependency we might have.                         |

#### Returns

| Type      | Description                              |
|-----------|------------------------------------------|
| JobHandle | A to our newly created ScheduleSend Job. |

### See Also

<div class="seealso">

<div>

System.IDisposable

</div>

</div>
