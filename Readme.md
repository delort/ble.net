# ble.net ![Build status](https://img.shields.io/vso/build/nexussays/ebc6aafa-2931-41dc-b030-7f1eff5a28e5/7.svg?style=flat-square) [![NuGet](https://img.shields.io/nuget/v/ble.net.svg?style=flat-square)](https://www.nuget.org/packages/ble.net) [![MPLv2 License](https://img.shields.io/badge/license-MPLv2-blue.svg?style=flat-square)](https://www.mozilla.org/MPL/2.0/)

`ble.net` is a Bluetooth Low Energy (aka BLE, aka Bluetooth LE, aka Bluetooth Smart) PCL to enable simple development of BLE clients on Android, iOS, and Windows 10 (advertising only at the moment, the underlying UWP connection API is pretty bad).

Currently only client operations are supported. Server operations will be added in the future if there is significant enough interest.

## Getting Started

### Install NuGet packages

Include `ble.net` in your shared project
```powershell
Install-Package ble.net
```

In each platform project, install the relevant package:
```powershell
Install-Package ble.net-android
```
```powershell
Install-Package ble.net-ios
```
```powershell
Install-Package ble.net-uwp
```

> Note that there are two packages for Android, `ble.net-android` and `ble.net-android21`; the API 21+ package is not materially different for client operations but will be needed if/when server operations are implemented. You should probably just use `ble.net-android` unless you have a specific reason not to do so.

### Obtain a reference to `BluetoothLowEnergyAdapter`

Each platform project has a class `BluetoothLowEnergyAdapter` with a static method `BluetoothLowEnergyAdapter.ObtainDefaultAdapter(/*possible arguments depending on platform*/)`. Obtain this reference and then provide it to your application code using whatever dependency injector or manual reference passing you are using in your project.

#### android

If you want to be able to enable/disable the adapter, in your `Activity.OnCreate()` call:
```csharp
BluetoothLowEnergyAdapter.InitActivity( this );
```

If you want `IBluetoothLowEnergyAdapter.OnStateChanged` to be hooked up, in your calling `Activity`:
```csharp
protected sealed override void OnActivityResult( Int32 requestCode, Result resultCode, Intent data )
{
   BluetoothLowEnergyAdapter.OnActivityResult( requestCode, resultCode, data );
}
```
