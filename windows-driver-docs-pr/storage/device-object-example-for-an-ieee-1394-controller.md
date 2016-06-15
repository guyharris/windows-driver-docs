---
title: Device Object Example for an IEEE 1394 Controller
author: windows-driver-content
description: Device Object Example for an IEEE 1394 Controller
ms.assetid: 9a83786b-8821-43b7-bf86-c85f2dcb9749
keywords: ["storage drivers WDK , device objects", "device objects WDK storage", "IEEE 1394 controller example WDK storage", "PCI IEEE 1394 controller example WDK storage"]
---

# Device Object Example for an IEEE 1394 Controller


## <span id="ddk_device_object_example_for_an_ieee_1394_controller_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_AN_IEEE_1394_CONTROLLER_KG"></span>


The following figure shows the device objects that are created for system with a PCI IEEE 1394 controller with an IEEE 1394 CD-ROM attached. Device objects for devices attached to the SCSI adapter are described in [Device Object Example for a SCSI HBA](device-object-example-for-a-scsi-hba.md).

![](images/kg201-3.png)

Device Object Tree for a CD-ROM Device on an IEEE 1394 Controller

Starting from the bottom of the figure, the following describes each device object and its corresponding driver:

1.  For a description of the device tree from the storage bus FDO up to the adapter PDOs, see [Device Object Example for a SCSI HBA](device-object-example-for-a-scsi-hba.md).

2.  The highest driver in the IEEE 1394 driver stack creates an SBP2 disk device PDO. The IEEE 1394 driver stack ultimately issues SBP2 commands to the target CD-ROM device on the IEEE 1394 bus.

3.  The system-supplied IEEE 1394 storage port driver is implemented as a filter driver that creates a filter DO and attaches it to the SBP2 disk device PDO. The IEEE 1394 storage port driver translates SRBs from the CD-ROM class driver into SBP2 commands which are issued to the underlying IEEE 1394 driver stack. The interface this driver presents to next-lower storage drivers is identical to that presented by the SCSI port/miniport driver described in [Device Object Example for a SCSI HBA](device-object-example-for-a-scsi-hba.md).

4.  The CD-ROM class driver creates an FDO and attaches it to the next-lower device object, which is either the SBP2 port filter DO or another filter DO attached to the stack by an intervening filter driver. The class driver issues all subsequent requests to the device through the lower driver's device object.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[storage\storage]:%20Device%20Object%20Example%20for%20an%20IEEE%201394%20Controller%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

