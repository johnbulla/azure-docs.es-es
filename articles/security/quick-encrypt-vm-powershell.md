---
title: 'Guía de inicio rápido: cifrado de una máquina virtual IaaS Windows con Azure PowerShell | Microsoft Docs'
description: En este inicio rápido, aprenderá a usar Azure PowerShell para cifrar una máquina virtual IaaS Windows en Azure.
services: security
documentationcenter: na
author: mestew
manager: MBaldwin
ms.assetid: c8abd340-5ed4-42ec-b83f-4d679b61494d
ms.service: security
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/29/2018
ms.author: mstewart
ms.custom: seodec18
ms.openlocfilehash: ee2a4be97b2b56f9c659639a34e821e37c188828
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53087871"
---
# <a name="quickstart-encrypt-a-windows-iaas-vm-with-azure-powershell"></a>Inicio rápido: Cifrado de una máquina virtual IaaS Windows con Azure PowerShell

Azure Disk Encryption le ayuda a cifrar discos de las máquinas virtuales IaaS con Windows y Linux. La solución se integra con Azure Key Vault para ayudarle a controlar y administrar los secretos y las claves del cifrado de discos. Si usa Azure Disk Encryption, puede tener la certeza de que las máquinas virtuales se protegen en reposo mediante una tecnología de cifrado estándar del sector. En este tutorial, creará una máquina virtual de Windows Server 2016 y cifrará el disco del sistema operativo.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

- Windows PowerShell ISE
- Instalación o actualización a la [versión más reciente de Azure PowerShell](/powershell/azure/install-azurerm-ps)
    - La versión del módulo AzureRM debe ser la 6.0.0, o cualquier versión posterior. `Get-Module AzureRM -ListAvailable | Select-Object -Property Name,Version,Path`
- Una copia del [script de requisitos previos de Azure Disk Encryption](https://raw.githubusercontent.com/Azure/azure-powershell/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
    - Si ya tiene este script, descargue una copia nueva, ya que ha cambiado recientemente. 
    - Use **CTRL-A** para seleccionar todo el texto y, después, use **CTRL-C** para copiarlo en el Bloc de notas.
    - Guarde el archivo como **ADEPrereqScript.ps1**


## <a name="sign-in-to-azure"></a>Inicio de sesión en Azure

1. Haga clic con el botón derecho en **Windows PowerShell ISE** y haga clic en **Ejecutar como administrador**.
1. En la ventana **Administrador: Windows PowerShell ISE**, haga clic en **Ver** y, a continuación, en **Mostrar panel de scripts**.
1. En el panel de scripts, escriba el siguiente cmdlet: 

     ```azurepowershell
      Connect-AzureRMAccount
     ```

1. Haga clic en la flecha verde de **Ejecutar script** o presione F5. 
2. Use el inicio de sesión interactivo para terminar la conexión a su cuenta de Azure.
3. Copie el **identificador de suscripción** que se devuelve para usarlo al ejecutar el siguiente script de PowerShell. 

## <a name="bkmk_PrereqScript"></a> Ejecución del script de requisitos previos de Azure Disk Encryption
 **ADEPrereqScript.ps1** creará un grupo de recursos, un almacén de claves y establecerá la directiva de acceso del almacén de claves. El script también crea un bloqueo de recursos en el almacén de claves para protegerlo contra la eliminación accidental.  

1. En la ventana **Administrador: Windows PowerShell ISE**, haga clic en **Archivo** y, después, en **Abrir**. Vaya al archivo **ADEPrereqScript.ps1** y haga doble clic en él. El script se abrirá en el panel de scripts.
2. Haga clic en la flecha verde de **Ejecutar script** o use F5 para ejecutar el script. 
3. Escriba los nombres de un **grupo de recursos** nuevo y un **almacén de claves** nuevo. No use un grupo de recursos o un almacén de claves existente en esta guía de inicio rápido, ya que el grupo de recursos se eliminará más adelante. 
4. Escriba la ubicación en la que desea crear los recursos, como **EastUS**. Obtenga una lista de ubicaciones con `Get-AzureRMLocation`.
5. Copie el **identificador de la suscripción**. El identificador de la suscripción se puede obtener con `Get-AzureRMSubscription`.  
6. Haga clic en la flecha verde de **Ejecutar script**. 
7. Copie los valores devueltos **DiskEncryptionKeyVaultUrl** y **DiskEncryptionKeyVaultId** para usarlos más adelante.

![Ejecución del script de requisitos previos de Azure Disk Encryption en PowerShell ISE](media/azure-security-disk-encryption/ade-prereq-script.PNG)


## <a name="create-a-virtual-machine"></a>de una máquina virtual 
Ahora debe crear una máquina virtual para poder cifrar su disco. El script que va a usar crea una máquina virtual con Windows Server 2016 con 8 GB de RAM y un disco de sistema operativo de 30 GB. 

1. Copie el script en el panel de scripts **Administrador: Windows PowerShell ISE** y cambie las tres primeras variables. El grupo de recursos y la ubicación deben ser los mismo que usó para el [script de requisitos previos](#bkmk_PrereqScript).  

   ```azurepowershell
    # Variables for common values
    $resourceGroup = "MySecureRG"
    $location = "EastUS"
    $vmName = "MySecureVM"
    
    # Create user object
    $cred = Get-Credential -Message "Enter a username and password for the virtual machine."
    
    # Create a resource group
    #New-AzureRmResourceGroup -Name $resourceGroup -Location $location
    
    # Create a subnet configuration
    $subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
    
    # Create a virtual network
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Location $location `
      -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig
    
    # Create a public IP address and specify a DNS name
    $pip = New-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup -Location $location `
      -Name "mypublicdns$(Get-Random)" -AllocationMethod Static -IdleTimeoutInMinutes 4
    
    # Create an inbound network security group rule for port 3389
    $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
      -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
      -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
      -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP
    
    # Create a virtual network card and associate with public IP address and NSG
    $nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName $resourceGroup -Location $location `
      -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
    
    # Create a virtual machine configuration
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D2_v3 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName $vmName -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter-smalldisk -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $nic.Id
    
    # Create a virtual machine
    New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig
   ```

2. Haga clic en la flecha verde de **Ejecutar script** para compilar la máquina virtual.  


## <a name="encrypt-the-disk-of-the-vm"></a>Cifrado del disco de la máquina virtual
Una vez creados y configurados un almacén de claves y una máquina virtual, se puede cifrar el disco con el cmdlet **Set-AzureRmVmDiskEncryptionExtension**. 
 
1. Ejecute el siguiente cmdlet para cifrar el disco de la máquina virtual:

    ```azurepowershell
     Set-AzureRmVmDiskEncryptionExtension -ResourceGroupName "MySecureRG" -VMName "MySecureVM" `
     -DiskEncryptionKeyVaultId "<Returned by the prerequisites script>" -DiskEncryptionKeyVaultUrl "<Returned by the prerequisites script>"
     ```


1. Cuando finalice el cifrado, puede comprobar que el disco está cifrado con el siguiente cmdlet: 

     ```azurepowershell
     Get-AzureRmVmDiskEncryptionStatus -ResourceGroupName "MySecureRG" -VMName "MySecureVM"
     ```
    ![Salida de Get-AzureRmVmDiskEncryptionStatus](media/azure-security-disk-encryption/ade-get-encryption-status.PNG)
    
## <a name="clean-up-resources"></a>Limpieza de recursos
 **ADEPrereqScript.ps1** crea un bloqueo de recursos en el almacén de claves. Para limpiar los recursos de esta guía de inicio rápido, es preciso quitar antes el bloqueo de recursos y, después, elimine el grupo de recursos. 

1. Eliminación del bloqueo de recursos del almacén de claves

     ```azurepowershell
     $LockId =(Get-AzureRMResourceLock -ResourceGroupName "MySecureRG" -ResourceName "MySecureVault" -ResourceType "Microsoft.KeyVault/vaults").LockID 
     Remove-AzureRmResourceLock -LockID $LockId
      ```
    
2. Quite el grupo de recursos. Esta acción también eliminará todos los recursos del grupo. 
     ```azurepowershell
      Remove-AzureRmResourceGroup -Name "MySecureRG"
      ```

## <a name="next-steps"></a>Pasos siguientes
En el artículo siguiente obtendrá más información acerca de los requisitos previos de Azure Disk Encryption para máquinas virtuales IaaS.

> [!div class="nextstepaction"]
> [Requisitos previos de Azure Disk Encryption](azure-security-disk-encryption-prerequisites.md)