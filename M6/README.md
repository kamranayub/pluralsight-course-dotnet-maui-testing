# Distributing to iOS

## Prerequisites

### For Pair to Mac and Visual Studio 2022

- [Pair to Mac documentation](https://learn.microsoft.com/en-us/dotnet/maui/ios/pair-to-mac?view=net-maui-9.0)
- .NET 8 SDK
- .NET 9.0.102 SDK

> [!NOTE] Installing Rosetta 2 on macOS
> In the Terminal:
> 
> ```
> softwareupdate --install-rosetta
> ```
>
> ([Source](https://osxdaily.com/2020/12/04/how-install-rosetta-2-apple-silicon-mac/))

### Troubleshooting

## Error Starting Broker

Ran into this issue with "[Error starting broker](https://stackoverflow.com/questions/79267654/vs-2022-pair-to-mac-error-starting-broker)". The solution was to install .NET 8 LTS SDK and the latest .NET 9.0.102 SDK.

## Error Starting Remote Simulator

Sometimes either your Mac or Visual Studio gets into a bad state. I had to restart both several times to get things working.

If you receive a `SocketNetworkError` about permissions, you may need to modify your **Remote Login** settings to add your individual user account to the allow list. Once I did this, the simulator started.

## App Store Connect API Key Error

Trying to enter too long a name for a Team API Key will show a generic error. Shorten the API key name.

## Deploying to Remote Device Fails with codesign Build Chain Error

I received an error related to `codesign` failing to build the key chain for the Apple Dev certificate.

It looks like on my Mac M1 I was missing a Apple Developer certificate that Xcode did not install.

Source: https://stackoverflow.com/questions/48911289/warning-unable-to-build-chain-to-self-signed-root-for-signer-warning-in-xcode