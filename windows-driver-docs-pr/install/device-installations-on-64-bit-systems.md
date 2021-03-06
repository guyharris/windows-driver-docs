---
title: Device Installations on 64-Bit Systems
description: Device Installations on 64-Bit Systems
ms.assetid: 76d9bff7-6429-4d20-9790-a41ed2cb1bdd
keywords:
- 64-bit WDK device installations
- device installations WDK , 64-bit systems
ms.date: 04/20/2017
ms.localizationpriority: medium
---

# Device Installations on 64-Bit Systems





If your device will be installed on both 32-bit platforms and 64-bit platforms, you must follow these steps when you create a [driver package](driver-packages.md):

-   Provide both 32-bit and 64-bit compilations of all kernel-mode drivers, *device installation application*, *class installers*, and *co-installers*. For more information, see [Porting Your Driver to 64-Bit Windows](https://docs.microsoft.com/windows-hardware/drivers/kernel/porting-your-driver-to-64-bit-windows).

-   Provide one or more cross-platform INF files that use *decorated INF sections* to control platform-specific installation behavior.

If you are [writing a device installation application](writing-a-device-installation-application.md), the 32-bit version must be the default version. That is, the 32-bit version should be invoked by Autorun (described in the Microsoft Windows SDK documentation), so that it starts automatically when a user inserts your distribution disk.

The 32-bit version of the application must check the value returned by [**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa). If the return value is ERROR_IN_WOW64, the 32-bit application is executing on a 64-bit platform and cannot update inbox drivers. Instead, it must call [**CreateProcess**](https://docs.microsoft.com/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa) (described in the Windows SDK documentation) to start the 64-bit version of the application. The 64-bit version can then call **UpdateDriverForPlugAndPlayDevices**, specifying a *FullInfPath* parameter that identifies the location of the 64-bit versions of all files.

 

 





