---
title: 'Azure Toolkit for IntelliJ: depuración de forma remota aplicaciones Spark mediante SSH '
description: Instrucciones paso a paso para el uso de las herramientas de HDInsight del Kit de herramientas de Azure para IntelliJ para depurar aplicaciones de forma remota en clústeres de HDInsight mediante SSH
keywords: depurar remotamente intellij, depuración remota intellij, ssh, intellij, hdinsight, depurar intellij, depuración
services: hdinsight
ms.service: hdinsight
author: jejiang
ms.author: jejiang
ms.reviewer: jasonh
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 11/25/2017
ms.openlocfilehash: ae22319c54335695a52e803c0c030858e2782c38
ms.sourcegitcommit: 56d20d444e814800407a955d318a58917e87fe94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/29/2018
ms.locfileid: "52582486"
---
# <a name="debug-spark-applications-locally-or-remotely-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Depuración de aplicaciones de Spark de forma local o remota en un clúster de HDInsight con el kit de herramientas de Azure para IntelliJ mediante SSH

En este artículo se ofrecen instrucciones paso a paso para el empleo de las herramientas de HDInsight de [Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij?view=azure-java-stable) para depurar aplicaciones de forma remota en un clúster de HDInsight. Para depurar el proyecto, también puede ver el vídeo [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ (Depurar aplicaciones HDInsight Spark con el Kit de herramientas de Azure para IntelliJ)](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ).

**Requisitos previos**
* **Herramientas de HDInsight del kit de herramientas de Azure para IntelliJ**. Esta herramienta es parte del Kit de herramientas de Azure para IntelliJ. Para más información, vea [Instalación del kit de herramientas de Azure para IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation). Y el **kit de herramientas de Azure para IntelliJ**. Use este kit de herramientas para crear aplicaciones Apache Spark para un clúster de HDInsight. Para más información, siga las instrucciones de [Uso de Azure Toolkit for IntelliJ con el fin de crear aplicaciones Apache Spark para un clúster de HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).

* **Servicio SSH de HDInsight con administración de nombre de usuario y contraseña**. Para más información, consulte [Conexión a través de SSH con HDInsight (Apache Hadoop)](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y [Uso de la tunelización SSH para tener acceso a la interfaz de usuario web de Ambari, JobHistory, NameNode, Oozie y otras interfaces de usuario web](https://docs.microsoft.com/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 
## <a name="learn-how-to-perform-local-run-and-debugging"></a>Obtenga información acerca de cómo ejecutar y depurar localmente
### <a name="scenario-1-create-a-spark-scala-application"></a>Escenario 1: Creación de una aplicación de Scala en Spark 

1. Inicie IntelliJ IDEA y, después, cree un proyecto. En el cuadro de diálogo **Nuevo proyecto** , haga lo siguiente:

    a. Seleccione **HDInsight**. 

   b. Seleccione una plantilla de Java o Scala según sus preferencias. Seleccione entre las siguientes opciones:

      - **Spark en HDInsight (Scala)**

      - **Spark en HDInsight (Java)**

      - **Spark on HDInsight Sample (Scala)**

      En este ejemplo se usa una plantilla **Spark on HDInsight Sample (Scala)**.

   c. En la lista de **herramientas de compilación**, seleccione cualquiera de las siguientes, según sus necesidades:

      - **Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala

      -  **SBT**, para administrar las dependencias y compilar el proyecto de Scala 

      ![Creación de un proyecto de depuración](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-create-projectfor-debug-remotely.png)

   d. Seleccione **Next** (Siguiente).     
 
1. En la siguiente ventana **Nuevo proyecto**, haga lo siguiente:

   ![Selección del SDK de Spark](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-new-project.png)

    a. Escriba un nombre y una ubicación de proyecto.

   b. En la lista desplegable **SDK de proyecto**, seleccione **Java 1.8** para el clúster de **Spark 2.x** o **Java 1.7** para el clúster de **Spark 1.x**.

   c. En la lista desplegable **Versión de Spark**, el asistente para la creación de proyectos de Scala integra la versión correcta del SDK de Spark y el SDK de Scala. Si la versión del clúster de Spark es anterior a la 2.0, seleccione **Spark 1.x**. De lo contrario, seleccione **Spark 2.x**. Este ejemplo utiliza **Spark 2.0.2 (Scala 2.11.8)**.

   d. Seleccione **Finalizar**.

1. Seleccione **src** > **main** > **scala** para abrir el código en el proyecto. En este artículo se usa el script **SparkCore_wasbloTest**.

### <a name="prerequisite-for-windows"></a>Requisito previo para Windows
Mientras se ejecuta la aplicación Spark en Scala local en un equipo Windows, puede producirse una excepción, como se explica en [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356). Esta excepción se produce porque falta WinUtils.exe en Windows. 

Para solucionar este error, [descargue el archivo ejecutable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) y guárdelo en una ubicación como **C:\WinUtils\bin**. Después, agregue una variable de entorno **HADOOP_HOME** y establezca el valor de la variable en **C:\WinUtils**.

### <a name="scenario-2-perform-local-run"></a>Escenario 2: Realizar una ejecución local
1. Abra el script **SparkCore_wasbloTest**, haga clic con el botón derecho en el editor de scripts y, a continuación, seleccione la opción **Run '[Spark Job]XXX'** para realizar la ejecución local.
1. Una vez completada la ejecución local, puede ver el archivo de salida guardado en el Explorador de proyectos actual **datos** > **__default__**.

    ![Resultados de la ejecución local](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/local-run-result.png)
1. Nuestras herramientas han establecido automáticamente la configuración de la ejecución local predeterminada al realizar la ejecución local y la depuración local. Abra la configuración de **[Spark Job] XXX** en la esquina superior derecha; verá que **[Spark Job] XXX** ya se ha creado en **Azure HDInsight Spark Job**. Cambie a la pestaña **Ejecutar localmente**.

    ![Configuración de la ejecución local](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/local-run-configuration.png)
    - [Variables de entorno](#prerequisite-for-windows): si ya ha establecido la variable de entorno del sistema **HADOOP_HOME** en **C:\WinUtils**, detecta automáticamente que no es necesario agregarla manualmente.
    - [Ubicación de WinUtils.exe](#prerequisite-for-windows): si no se ha establecido la variable de entorno del sistema, haga clic en el botón correspondiente para encontrar la ubicación.
    - Solo tiene que elegir cualquiera de las dos opciones. No se necesitan en MacOS y Linux.
1. También puede establecer la configuración manualmente antes de realizar la depuración local y la ejecución local. En la captura de pantalla anterior, seleccione el signo más (**+**). Después, seleccione la opción **Azure HDInsight Spark Job**. Escriba la información en **Name** (Nombre), **Main class name** (Nombre de clase principal) y haga clic en el botón de ejecución local.

### <a name="scenario-3-perform-local-debugging"></a>Escenario 3: Realizar una depuración local
1. Abra el script **SparkCore_wasbloTest** y establezca los puntos de interrupción.
1. Haga clic con el botón derecho en el editor de scripts y seleccione la opción **Debug '[Spark Job]XXX'** para realizar la depuración local.   



## <a name="learn-how-to-perform-remote-run-and-debugging"></a>Obtenga información acerca de cómo ejecutar y depurar de forma remota
### <a name="scenario-1-perform-remote-run"></a>Escenario 1: Realizar la ejecución remota

1. Para acceder al menú **Editar configuraciones**, seleccione el icono de la esquina superior derecha. Desde este menú, puede crear o modificar las configuraciones para la depuración remota.

   ![Editar configuraciones](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-edit-configurations.png) 

1. En el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/depurar configuraciones), seleccione el signo más (**+**). Después, seleccione la opción **Azure HDInsight Spark Job**.

   ![Adición de nueva configuración](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-add-new-Configuration.png)
1. Cambie a la pestaña **Remotely Run in Cluster** (Ejecutar de forma remota en clúster). Escriba la información en los campos **Name** (Nombre), **Spark cluster** (Clúster de Spark) y **Main class name** (Nombre de clase principal). Después seleccione **Advanced configuration** (Configuración avanzada). Nuestras herramientas admiten la depuración con **ejecutores**. Elv alor predeterminado de **numExectors** es 5. Es mejor no establecer más de 3.

   ![Ejecutar configuraciones de depuración](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-run-debug-configurations.png)

1. En el cuadro de diálogo **Spark Submission Advanced Configuration** (Configuración avanzada de envío de Spark), seleccione **Enable Spark remote debug** (Habilitar depuración remota de Spark). Escriba el nombre de usuario SSH y luego especifique una contraseña o use un archivo de clave privada. Para guardar la configuración, seleccione **Aceptar**. Si desea realizar la depuración remota, debe establecerla. No es necesario establecerla si solo desea usar la ejecución remota.

   ![Habilitar la depuración remota de Spark](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-enable-spark-remote-debug.png)

1. La configuración se guarda ahora con el nombre especificado. Para ver los detalles de configuración, seleccione el nombre de configuración. Para realizar cambios, seleccione **Edit Configurations** (Editar configuraciones). 

1. Después de completar la configuración, puede ejecutar el proyecto en el clúster remoto o realizar la depuración remota.
   
   ![Botón de ejecución remota](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/perform-remote-run.png)

1. Haga clic en el botón **Desconectar** si los registros de envío no aparecen en el panel izquierdo. Sin embargo, continúa en ejecución en el back-end.

   ![Botón de ejecución remota](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/remote-run-result.png)



### <a name="scenario-2-perform-remote-debugging"></a>Escenario 2: Realizar la depuración remota
1. Configure los puntos de interrupción y luego seleccione el icono **Remote debug** (Depuración remota). La diferencia con el envío remoto es que hay que configurar el nombre de usuario y la contraseña de SSH.

   ![Selección del icono de depuración](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-debug-icon.png)

1. Cuando la ejecución del programa alcanza el punto de interrupción, aparecen una pestaña **Controlador** y dos pestañas **Ejecutor** en el panel **Depurador**. Seleccione el icono **Resume Program** (Continuar programa) para seguir ejecutando el código, que luego alcanza el siguiente punto de interrupción. Debe cambiar a la pestaña **Executor** (Ejecutor) correcta para buscar el ejecutor de destino que se va a depurar. Puede ver los registros de ejecución en la pestaña **Console** (Consola) correspondiente.

   ![Pestaña Depuración](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-debugger-tab.png)

### <a name="scenario-3-perform-remote-debugging-and-bug-fixing"></a>Escenario 3: Realizar la depuración remota y corrección de errores
1. Configure dos puntos de interrupción y luego seleccione el icono **Depurar** para iniciar el proceso de depuración remota.

1. El código se detiene en el primer punto de interrupción y se muestra la información de parámetros y variables en el panel **Variables**. 

1. Seleccione el icono **Resume Program** (Continuar programa) para continuar. El código se detiene en el segundo punto. La excepción se detecta según lo previsto.

   ![Iniciar error](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-throw-error.png) 

1. Vuelva a seleccionar el icono **Resume Program** (Continuar programa). La ventana **HDInsight Spark Subsmission**  (Envío de HDInsight Spark) muestra un error de ejecución de trabajo.

   ![Envío de error](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-error-submission.png) 

1. Para actualizar de forma dinámica el valor de variable mediante la funcionalidad de depuración de IntelliJ, vuelva a seleccionar **Depurar**. El panel **Variables** aparece de nuevo. 

1. Haga clic con el botón derecho en el destino en el pestaña **Depurar** y, a continuación, seleccione **Establecer valor**. Luego escriba un nuevo valor para la variable. A continuación, seleccione **Entrar** para guardar el valor. 

   ![Establecer valor](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-set-value.png) 

1. Seleccione el icono **Resume Program** (Continuar programa) para seguir ejecutando el programa. Esta vez no se detecta ninguna excepción. Puede ver que el proyecto se ejecuta correctamente sin ninguna excepción.

   ![Depurar sin excepciones](./media/apache-spark-intellij-tool-debug-remotely-through-ssh/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Pasos siguientes
* [Introducción a Apache Spark en HDInsight de Azure](apache-spark-overview.md)

### <a name="demo"></a>Demostración
* Creación del proyecto Scala (vídeo): [Create Apache Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creación de aplicaciones Scala de Apache Spark)
* Depuración remota (vídeo): [Use Azure Toolkit for IntelliJ to debug Apache Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (Uso de Azure Toolkit for IntelliJ para depurar de forma remota aplicaciones Apache Spark en clústeres de HDInsight)

### <a name="scenarios"></a>Escenarios
* [Apache Spark con BI: realización del análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](apache-spark-use-bi-tools.md)
* [Apache Spark con Machine Learning: uso de Spark en HDInsight para analizar la temperatura de edificios con los datos del sistema de acondicionamiento de aire](apache-spark-ipython-notebook-machine-learning.md)
* [Apache Spark con Machine Learning: Uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos](apache-spark-machine-learning-mllib-ipython.md)
* [Análisis de registros de un sitio web mediante Apache Spark en HDInsight](../hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](../hdinsight-apache-spark-create-standalone-application.md)
* [Ejecución de trabajos de forma remota en un clúster de Apache Spark mediante Apache Livy](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Uso de Azure Toolkit for IntelliJ con el fin de crear aplicaciones Apache Spark para un clúster de HDInsight](apache-spark-intellij-tool-plugin.md)
* [Uso de Azure Toolkit for IntelliJ para depurar de forma remota aplicaciones de Apache Spark mediante VPN](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox](../hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Uso de las herramientas de HDInsight de Azure Toolkit for Eclipse con el fin de crear aplicaciones Apache Spark](../hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Uso de cuadernos de Apache Zeppelin con un clúster Apache Spark en HDInsight](apache-spark-zeppelin-notebook.md)
* [Kernels para Jupyter Notebook en clústeres Azure Spark en Azure HDInsight](apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administración de recursos para el clúster Apache Spark en HDInsight de Azure](apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](apache-spark-job-debugging.md)
