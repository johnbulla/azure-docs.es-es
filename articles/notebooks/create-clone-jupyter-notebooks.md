---
title: Creación y clonación de Jupyter Notebooks en Azure
description: Los proyectos de Azure Notebooks administran una colección de cuadernos y archivos relacionados, que puede crear o clonar desde otro origen.
services: app-service
documentationcenter: ''
author: kraigb
manager: douge
ms.assetid: 9b6a49e2-1d71-4c0b-9e5d-16e059427e38
ms.service: notebooks
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/04/2018
ms.author: kraigb
ms.openlocfilehash: 151d945bbeda9f7dd496f8469f8f858e8369da8f
ms.sourcegitcommit: efcd039e5e3de3149c9de7296c57566e0f88b106
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2018
ms.locfileid: "53164422"
---
# <a name="create-and-clone-projects"></a>Creación y clonación de proyectos

Azure Notebooks organiza sus cuadernos de Jupyter Notebooks y los archivos relacionados en grupos lógicos llamados *proyectos*. En primer lugar, crea un proyecto como contenedor, luego, crea o clona uno o más cuadernos de una carpeta junto con otros archivos del proyecto. (Este proceso se muestra en el [tutorial](tutorial-create-run-jupyter-notebook.md)).

Un proyecto también mantiene los metadatos y otras opciones de configuración que afectan al servidor en el que se ejecutan los cuadernos, incluidos los pasos de instalación personalizados y la instalación del paquete. Para más información, consulte [Administración y configuración de proyectos](configure-manage-azure-notebooks-projects.md).

## <a name="use-the-my-projects-dashboard"></a>Uso del panel Mis proyectos

El panel **Mis proyectos** en `https://notebooks.azure.com/<userID>/projects` es donde se pueden ver, administrar y crear proyectos:

[![](media/my-projects-dashboard.png "Panel Mis proyectos en Azure Notebooks")](media/my-projects-dashboard.png#lightbox)

Lo que puede hacer en el panel depende de si ha iniciado sesión con la cuenta que posee el identificador de usuario:

| Get-Help | Disponible para | DESCRIPCIÓN |
| --- | --- | --- |
| **Run** | Propietario | Inicia el servidor del proyecto y abre la carpeta del proyecto en Jupyter. (Más comúnmente, navega primero a una carpeta del proyecto y luego inicia un cuaderno desde allí). |
| **Descargar** | Todos | Descarga una copia del proyecto seleccionado como archivo ZIP. |
| **Compartir** | Todos | Muestra la ventana emergente para compartir a través de la cual puede obtener una dirección URL hacia un proyecto seleccionado, compartir en medios sociales, enviar un correo electrónico con la dirección URL y obtener el código HTML o Markdown con una notificación de "iniciar cuaderno" (consulte [obtención de una notificación de inicio](#obtain-a-launch-badge)) con la dirección URL. |
| **Eliminar** | Propietario | Elimina el proyecto seleccionado. Esta operación no se puede deshacer. |
| **Terminal** | Propietario | Inicia el servidor del proyecto y luego abre una nueva ventana del explorador con la terminal bash para ese servidor. |
| **+ Nuevo proyecto** | Propietario | Crea un nuevo proyecto. Consulte [Creación de un nuevo proyecto](#create-a-new-project). |
| **Upload GitHub Repo** | Propietario | Importa un proyecto desde GitHub. [Importe un proyecto desde GitHub](#import-a-project-from-github). |
| **Clonar** | Todos | Copia un proyecto seleccionado en su propia cuenta. Le pedirá que inicie sesión en aún no lo hizo. Consulte [Clonación de un proyecto](#clone-a-project). |

### <a name="obtain-a-launch-badge"></a>Obtención una notificación de inicio

Cuando use el comando **Compartir** y seleccione la pestaña **Insertar**, puede copiar código HTML o Markdown que crea una notificación "iniciar cuaderno":

![Notificación de inicio de cuaderno ](https://notebooks.azure.com/launch.png)

Si no tiene un proyecto de Azure Notebooks, puede crear un vínculo que clone desde GitHub directamente mediante las plantillas siguientes, sustituyendo el nombre de usuario y los nombres de repositorio correspondientes:

```html
<a href="https://notebooks.azure.com/import/gh/<GitHub_username>/<repository_name>"><img src="https://notebooks.azure.com/launch.png" /></a>
```

```markdown
[![Azure Notebooks](https://notebooks.azure.com/launch.png)](https://notebooks.azure.com/import/gh/<GitHub_username>/<repository_name>)
```

## <a name="create-a-new-project"></a>Creación de un nuevo proyecto

Cuando usa el comando **+ Nuevo proyecto**, Azure Notebooks muestra una ventana emergente **Crear proyecto**. En esta ventana emergente, escriba la siguiente información y seleccione **Crear**:

| Campo | DESCRIPCIÓN |
| --- | --- |
| Nombre de proyecto | Un nombre descriptivo para el proyecto que usa Azure Notebooks para fines de presentación. Por ejemplo, "Mi proyecto de cuaderno". |
| Identificador del proyecto | Un identificador personalizado que se vuelve parte de la dirección URL que usa para compartir un proyecto. Este identificador solo puede usar letras, números y guiones y se limita a 30 caracteres. Si no está seguro de qué usar, una convención común es usar una versión en minúsculas del nombre del proyecto, donde los espacios se convierten en guiones, como "mi-proyecto-de-cuaderno" (truncado si es necesario para que se ajuste al límite de longitud). |
| Público | Si se establece, permite a cualquier usuario con el vínculo acceder al proyecto. Al crear un proyecto privado, desactive esta opción. |
| Initialize this project with a README (Inicializar este proyecto con un archivo Léame) | Si se establece, se crea un archivo predeterminado *README.md* en el proyecto. Un archivo *README.md* es donde proporciona documentación para el proyecto, si lo desea. |

## <a name="import-a-project-from-github"></a>Importación de un proyecto desde GitHub

Puede importar fácilmente un repositorio de GitHub público completo como un proyecto, incluidos todos los datos y archivos *README.md*. Use el comando **Upload GitHub Repo** (Cargar repositorio de GitHub), proporcione los detalles siguientes en el menú emergente y luego seleccione **Importar**:

| Campo | DESCRIPCIÓN |
| --- | --- |
| Repositorio de GitHub | El nombre del repositorio de origen en github.com. Por ejemplo, para clonar los cuadernos de Jupyter Notebooks para Azure Cognitive Services en [https://github.com/Microsoft/cognitive-services-notebooks](https://github.com/Microsoft/cognitive-services-notebooks), escriba "Microsoft/cognitive-services-notebooks".  |
| Clone recursively (Clonar de forma recursiva) | Los repositorios de GitHub pueden contener varias bases de datos secundarias. Establezca esta opción si desea clonar el repositorio primario y todos sus elementos secundarios. Dado que es posible que un repositorio tenga muchos elementos secundarios, deje esta opción desmarcada, a menos que sepa que la necesita. |
| Nombre de proyecto | Un nombre descriptivo para el proyecto que usa Azure Notebooks para fines de presentación. |
| Identificador del proyecto | Un identificador personalizado que se vuelve parte de la dirección URL que usa para compartir un proyecto. Este identificador solo puede contener letras, números y guiones. |
| Público | Si se establece, permite a cualquier usuario con el vínculo acceder al proyecto. Al crear un proyecto privado, desactive esta opción. |

Importar un repositorio de GitHub también importa su historial. Puede usar los comandos de Git estándar desde el terminal para confirmar los cambios nuevos, extraer los cambios de GitHub, etc.

## <a name="clone-a-project"></a>Clonación de un proyecto

La clonación crea una copia de un proyecto existente en su propia cuenta, donde luego puede ejecutar y modificar cualquier cuaderno u otro archivo en el proyecto. También puede usar la clonación para hacer copias de sus propios proyectos, en las que haga experimentos u otros trabajos sin tener que tocar el proyecto original.

Para clonar un proyecto:

1. En el panel **Mis proyectos**, haga clic con el botón derecho en el proyecto deseado y seleccione **Clonar** (método abreviado de teclado: c).

    ![Comando de clonación en el menú contextual del proyecto](media/clone-command.png)

1. En la ventana emergente **Clone Project** (Clonar proyecto), escriba un nombre e identificador de la clonación y especifique si el clon es público. Estos valores son los mismos que para un [nuevo proyecto](#create-a-new-project).

    ![Ventana emergente Clonar proyecto](media/clone-project.png)

1. Después de seleccionar el botón **Clonar**, Azure Notebooks navega directamente hasta la copia.

## <a name="next-steps"></a>Pasos siguientes

- [Exploración de cuadernos de ejemplo](azure-notebooks-samples.md)
- [Procedimientos: Configuración y administración de proyectos](configure-manage-azure-notebooks-projects.md)
- [Procedimientos: Instalación de paquetes en un cuaderno](install-packages-jupyter-notebook.md)
- [Procedimientos: Presentación](present-jupyter-notebooks-slideshow.md)
- [Procedimientos: Uso de archivos de datos](work-with-project-data-files.md)
- [Procedimientos: Acceso a recursos de datos](access-data-resources-jupyter-notebooks.md)
- [Procedimientos: Uso de Azure Machine Learning Services](use-machine-learning-services-jupyter-notebooks.md)
