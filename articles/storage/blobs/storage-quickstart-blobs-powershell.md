---
title: 'Guía de inicio rápido de Azure: Creación de un blob en el almacenamiento de objetos con Azure PowerShell | Microsoft Docs'
description: En esta guía de inicio rápido, utilizará Azure PowerShell en el almacenamiento de objetos (Blob). Después, puede usar PowerShell para cargar un blob en Azure Storage, descargar un blob o enumerar los blobs de un contenedor.
services: storage
author: roygara
ms.custom: mvc
ms.service: storage
ms.topic: quickstart
ms.date: 12/11/2018
ms.author: rogarana
ms.openlocfilehash: 700a4c22b7ae08449e2bb599b99cd7438e74ba6d
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2018
ms.locfileid: "53312007"
---
# <a name="quickstart-upload-download-and-list-blobs-by-using-azure-powershell"></a>Guía de inicio rápido: Carga, descarga y enumeración de blobs mediante Azure PowerShell

Use el módulo de Azure PowerShell para crear y administrar los recursos de Azure. La creación o administración de los recursos de Azure puede realizarse desde la línea de comandos de PowerShell o en scripts. En esta guía se detalla el uso de PowerShell para transferir archivos entre el disco local y Azure Blob Storage.

## <a name="prerequisites"></a>Requisitos previos

Para acceder a Azure Storage, necesitará una suscripción de Azure. Si todavía no tiene una suscripción, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

Para realizar los pasos de esta guía, se requiere la versión 3.6 del módulo Azure PowerShell, o cualquier versión posterior. Ejecute `Get-Module -ListAvailable AzureRM` para encontrar la versión. Si necesita instalarla o actualizarla, consulte el artículo sobre [cómo instalar el módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).

[!INCLUDE [storage-quickstart-tutorial-intro-include-powershell](../../../includes/storage-quickstart-tutorial-intro-include-powershell.md)]

## <a name="create-a-container"></a>Crear un contenedor

Los blobs siempre se cargan en un contenedor. Puede organizar los grupos de blobs de una forma similar a cómo organiza los archivos en carpetas en el equipo.

Establece el nombre del contenedor y, después, crea el contenedor mediante [New-AzureStorageContainer](/powershell/module/azure.storage/new-azurestoragecontainer). Establezca los permisos para `blob` de modo que se permita el acceso público de los archivos. El nombre del contenedor en este ejemplo es *quickstartblobs*.

```powershell
$containerName = "quickstartblobs"
New-AzureStorageContainer -Name $containerName -Context $ctx -Permission blob
```

## <a name="upload-blobs-to-the-container"></a>Carga de blobs al contenedor

Blob Storage admite blobs en bloques, blobs en anexos y blobs en páginas. Los archivos VHD utilizados para respaldar VM IaaS son blobs en páginas. Use los blobs en anexos para el registro, por ejemplo, cuando desea escribir en un archivo y luego sigue agregando más información. La mayoría de los archivos almacenados en Blob Storage son blobs en bloques. 

Para cargar un archivo en un blob en bloques, obtenga una referencia de contenedor y luego obtenga una referencia al blob en bloques en ese contenedor. Una vez que tenga la referencia de blob, puede cargar datos en él mediante [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent). De este modo, se creará el blob si no existe, o se sobrescribirá si ya existe.

Los ejemplos siguientes cargan *Image001.jpg* e *Image002.png* desde la carpeta *D:\\_TestImages* del disco local al contenedor que creó.

```powershell
# upload a file
Set-AzureStorageBlobContent -File "D:\_TestImages\Image001.jpg" `
  -Container $containerName `
  -Blob "Image001.jpg" `
  -Context $ctx 

# upload another file
Set-AzureStorageBlobContent -File "D:\_TestImages\Image002.png" `
  -Container $containerName `
  -Blob "Image002.png" `
  -Context $ctx
```

Cargue tantos archivos como desee antes de continuar.

## <a name="list-the-blobs-in-a-container"></a>Enumerar los blobs de un contenedor

Obtenga una lista de blobs del contenedor mediante [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob). Este ejemplo muestra solo los nombres de los blobs cargados.

```powershell
Get-AzureStorageBlob -Container $ContainerName -Context $ctx | select Name 
```

## <a name="download-blobs"></a>Descargar blobs

Descargue los blobs en el disco local. Para cada blob que desee descargar, establezca el nombre y la llame a [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) para descargar el blob.

Este ejemplo descarga los blobs a *D:\\_TestImages\Downloads* en el disco local. 

```powershell
# download first blob
Get-AzureStorageBlobContent -Blob "Image001.jpg" `
  -Container $containerName `
  -Destination "D:\_TestImages\Downloads\" `
  -Context $ctx 

# download another blob
Get-AzureStorageBlobContent -Blob "Image002.png" `
  -Container $containerName `
  -Destination "D:\_TestImages\Downloads\" `
  -Context $ctx 
```

## <a name="data-transfer-with-azcopy"></a>Transferencia de datos con AzCopy

La utilidad [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) es otra opción para la transferencia de datos que permite ejecutar scripts de alto rendimiento para Azure Storage. Use AzCopy para transferir datos a y desde Blob Storage, File Storage y Table Storage.

A modo de un ejemplo rápido, aquí está el comando de AzCopy para cargar un archivo denominado *myfile.txt* al contenedor *mystoragecontainer* desde dentro de una ventana de PowerShell.

```PowerShell
./AzCopy `
    /Source:C:\myfolder `
    /Dest:https://mystorageaccount.blob.core.windows.net/mystoragecontainer `
    /DestKey:<storage-account-access-key> `
    /Pattern:"myfile.txt"
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Quite todos los recursos que ha creado. La manera más fácil de quitar los recursos consiste en eliminar el grupo de recursos. Al quitar el grupo de recursos también se eliminan todos los recursos contenidos en él. En el ejemplo siguiente, al quitar el grupo de recursos, se quita la cuenta de almacenamiento y el propio grupo de recursos.

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En esta guía de inicio rápido, transfirió archivos entre un disco local y Azure Blob Storage. Para más información sobre cómo trabajar con Blob Storage mediante PowerShell, continúe con el tutorial sobre el uso de Azure PowerShell con Azure Storage.

> [!div class="nextstepaction"]
> [Usar Azure PowerShell con Azure Storage](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

### <a name="microsoft-azure-powershell-storage-cmdlets-reference"></a>Referencia de cmdlets de almacenamiento de Microsoft Azure PowerShell

* [Cmdlets de PowerShell de almacenamiento](/powershell/module/azurerm.storage#storage)

### <a name="microsoft-azure-storage-explorer"></a>Explorador de almacenamiento de Microsoft Azure

* El [Explorador de Microsoft Azure Storage](../../vs-azure-tools-storage-manage-with-storage-explorer.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) es una aplicación independiente y gratuita de Microsoft que permite trabajar visualmente con los datos de Azure Storage en Windows, macOS y Linux.
