---
title: Uso de la interfaz de usuario de Apache Tez con HDInsight basado en Windows en Azure
description: Aprenda a usar la interfaz de usuario de Apache Tez para depurar trabajos de Tez en HDInsight basado en Windows.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 01/17/2017
ms.author: hrasheed
ROBOTS: NOINDEX
ms.openlocfilehash: 1e529b2276d2e68c67696ba9d142760f5881a25e
ms.sourcegitcommit: 698ba3e88adc357b8bd6178a7b2b1121cb8da797
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2018
ms.locfileid: "53012817"
---
# <a name="use-the-apache-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a>Usar la interfaz de usuario de Apache Tez para depurar trabajos de Tez en HDInsight basado en Windows
La interfaz de usuario de [Apache Tez](https://tez.apache.org/) puede utilizarse para depurar los trabajos de [Apache Hive](https://hive.apache.org/) que utilizan Tez como motor de ejecución. La interfaz de usuario de Tez permite visualizar el trabajo como un gráfico de elementos conectados, profundizar en cada elemento y recuperar las estadísticas y la información de registro.

> [!IMPORTANT]
> Los pasos de este documento requieren un clúster de HDInsight que use Windows. Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Requisitos previos
* Un clúster de HDInsight basado en Windows Para obtener información sobre cómo crear un clúster, consulte [Introducción al uso de HDInsight basado en Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > La interfaz de usuario de Apache Tez solo está disponible en los clústeres de HDInsight basado en Windows creados después del 8 de febrero de 2016.
  >
  >
* Un cliente de escritorio remoto basado en Windows.

## <a name="understanding-apache-tez"></a>Descripción de Apache Tez
Tez es un marco de trabajo extensible para el procesamiento de datos en Apache Hadoop que proporciona una mayor velocidad que el procesamiento tradicional de [Apache Hadoop MapReduce](https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html). Puede habilitar Tez si incluye el texto siguiente como parte de una consulta de Hive:

    set hive.execution.engine=tez;

Tez crea un grafo acíclico dirigido (DAG) que describe el orden de ejecución de las acciones que requiere el trabajo. Las acciones individuales se denominan vértices y ejecutan una parte del trabajo total. La ejecución real del trabajo descrito por un vértice se denomina tarea, y puede distribuirse por varios nodos del clúster.

### <a name="understanding-the-tez-ui"></a>Descripción de la interfaz de usuario de Tez
La interfaz de usuario de Tez es una página web que proporciona información sobre los procesos que usan Tez. Puede ofrecer información útil en los escenarios siguientes:

* Supervisión de procesos de ejecución prolongada, visualización del progreso de asignación y reducción de las tareas.
* Análisis de datos históricos de procesos correctos o con errores para obtener información sobre cómo se puede mejorar el procesamiento o sobre la causa del error.

## <a name="generate-a-dag"></a>Generar un DAG
La interfaz de usuario de Tez contiene datos si se está ejecutando actualmente un trabajo que usa el motor de Tez, o bien si se ejecutó anteriormente. Las consultas simples de Hive suelen resolverse sin necesidad de usar Tez. Para aquellas consultas más complejas que realizan filtrados, agrupaciones, ordenaciones, combinaciones, etc., Tez es necesario.

Siga estos pasos para ejecutar una consulta de Hive que utilice Tez.

1. En un explorador web, vaya a https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es el nombre del clúster de HDInsight.
2. En el menú que aparece en la parte superior de la página, seleccione el **Editor de Hive**. Se mostrará una página con la siguiente consulta de ejemplo.

        Select * from hivesampletable

    Borre la consulta de ejemplo y reemplácela por lo siguiente.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Seleccione el botón **Enviar**. En la sección **Sesión de trabajo** que aparece en la parte inferior de la página se muestra el estado de la consulta. Cuando el estado cambie a **Completado**, seleccione el vínculo **Ver detalles** para ver los resultados. La **Salida del trabajo** debe ser similar a la siguiente:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a>Usar la interfaz de usuario de Tez
> [!NOTE]
> La interfaz de usuario de Tez solo está disponible en el escritorio de los nodos principales del clúster, por lo que debe usar Escritorio remoto para conectarse a los nodos principales.
>
>

1. En el [Portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight. En la parte superior de la hoja de HDInsight, seleccione el icono **Escritorio remoto**. Este vínculo muestra la hoja de Escritorio remoto.

    ![Icono de Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. En la hoja Escritorio remoto, seleccione **Conectar** para conectarse al nodo principal del clúster. Cuando se le solicite, use el nombre de usuario y la contraseña de Escritorio remoto del clúster para autenticar la conexión.

    ![Icono de conexión a Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Si no ha habilitado la conectividad de Escritorio remoto, proporcione un nombre de usuario, una contraseña y una fecha de expiración, y luego seleccione **Habilitar** para habilitar Escritorio remoto. Una vez habilitado, siga los pasos anteriores para conectarse.
   >
   >
3. Cuando se haya conectado, abra Internet Explorer en el escritorio remoto, seleccione el icono de engranaje en la esquina superior derecha del explorador y seleccione **Configuración de Vista de compatibilidad**.
4. En la parte inferior de **Configuración de Vista de compatibilidad**, desactive la casilla **Mostrar sitios de la intranet en Vista de compatibilidad** y **Usar listas de compatibilidad de Microsoft** y, luego, seleccione **Cerrar**.
5. En Internet Explorer, vaya a http://headnodehost:8188/tezui/#/. Esto muestra la interfaz de usuario de Tez

    ![Interfaz de usuario de Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    Cuando se cargue la interfaz de usuario de Tez, verá una lista de DAG que se están ejecutando actualmente o que se ejecutaron anteriormente en el clúster. La vista predeterminada incluye el nombre del DAG, el identificador, el remitente, el estado, la hora de inicio, la hora de finalización, la duración, el identificador de la aplicación y la cola. Puede agregar más columnas mediante el icono de engranaje que se encuentra a la derecha de la página.

    Si solo tiene una entrada, será la de la consulta que ejecutó en la sección anterior. Si tiene varias entradas, puede realizar una búsqueda; para ello, especifique criterios de búsqueda en los campos situados encima de los DAG y presione **ENTRAR**.
6. Seleccione el **Nombre del DAG** de la entrada de DAG más reciente. Este vínculo muestra información sobre el DAG, así como la opción de descargar un archivo ZIP con archivos JSON que contienen información sobre el DAG.

    ![Detalles del DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Encima de **Detalles del DAG** aparecen varios vínculos que pueden usarse para mostrar información sobre el DAG.

   * **Contadores del DAG** muestra información de los contadores de este DAG.
   * **Vista gráfica** muestra una representación gráfica de este DAG.
   * **Todos los vértices** muestra una lista de los vértices de este DAG.
   * **Todas las tareas** muestra una lista de las tareas de todos los vértices de este DAG.
   * **Todos los intentos de tarea** muestra información sobre los intentos de ejecutar las tareas de este DAG.

     > [!NOTE]
     > Si se desplaza por la presentación en columnas de Vértices, Tareas e Intentos de tarea, verá que hay vínculos para ver los **contadores** y para **ver o descargar los registros** de cada fila.
     >
     >

     Si se produjo un error en el trabajo, en Detalles del DAG aparecerá el estado ERROR, junto con vínculos a información relativa a la tarea con el error. Debajo de los detalles del DAG, se muestra información de diagnóstico.
8. Seleccione **Vista gráfica**. Muestra una representación gráfica del DAG. Puede colocar el mouse sobre cada vértice de la vista para mostrar su información.

    ![Vista gráfica](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Al hacer clic en un vértice, se cargan los **Detalles del vértice** de ese elemento. Haga clic en el vértice **Asignación 1** para mostrar los detalles de ese elemento. Seleccione **Confirmar** para confirmar la navegación.

    ![Detalles del vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Observe que ahora aparecen vínculos en la parte superior de la página que están relacionados con las tareas y los vértices.

    > [!NOTE]
    > Para llegar a esta página, puede regresar a **Detalles del DAG**, seleccionar **Detalles del vértice** y seleccionar el vértice **Asignación 1**.
    >
    >

    * **Contadores del vértice** muestra información de los contadores de este vértice.
    * **Tareas** muestra las tareas de este vértice.
    * **Intentos de tarea** muestra información sobre los intentos de ejecutar las tareas de este vértice.
    * **Orígenes y receptores** muestra los orígenes de datos y los receptores de este vértice.

      > [!NOTE]
      > Al igual que en el menú anterior, puede desplazarse por la presentación de columna de Tareas, Intentos de tarea y Orígenes y receptores para que aparezcan vínculos a información adicional sobre cada elemento.
      >
      >
11. Seleccione **Tareas** y luego seleccione el elemento llamado **00_000000**. Este vínculo muestra los **Detalles de la tarea** de esta tarea. En esta pantalla, puede ver los **Contadores de tarea** y los **Intentos de tarea**.

    ![Detalles de la tarea](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido a usar la vista de [Apache Tez](https://tez.apache.org/), obtenga más información sobre el [Uso de Apache Hive en HDInsight](hadoop/hdinsight-use-hive.md).

Para obtener información técnica más detallada sobre Tez, consulte la [página de Apache Tez en Hortonworks](https://hortonworks.com/hadoop/tez/).
