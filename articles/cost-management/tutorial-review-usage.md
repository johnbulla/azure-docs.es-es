---
title: 'Tutorial: Revisión del uso y los costos con Cloudyn en Azure | Microsoft Docs'
description: En este tutorial, revisará el uso y los costos para realizar un seguimiento de las tendencias, detectar deficiencias y crear alertas.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 12/07/2018
ms.topic: tutorial
ms.service: cost-management
ms.custom: seodec18
manager: benshy
ms.openlocfilehash: 928b8fd8ef076afa2c60c870fb705a9a682003d1
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53093614"
---
<!-- Intent: As a cloud-consuming user, I need to view usage and costs for my cloud resources and services.
-->

# <a name="tutorial-review-usage-and-costs"></a>Tutorial: Revisión del uso y los costos

Cloudyn muestra el uso y los costos para que pueda realizar un seguimiento de las tendencias, detectan deficiencias y crear alertas. Todos los datos de uso y costos se muestran en los informes y paneles de Cloudyn. Los ejemplos de este tutorial le guiarán en la revisión del uso y los costos de los paneles e informes.

Azure Cost Management ofrece una funcionalidad similar a Cloudyn. Azure Cost Management es una solución de administración de costos de Azure nativa. Le ayuda a analizar costos, crear y administrar presupuestos, exportar datos, y revisar y actuar sobre recomendaciones de optimización para ahorrar dinero. Para más información, consulte [Azure Cost Management](overview-cost-mgt.md).

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Realizar un seguimiento de las tendencias de uso y costos
> * Detectar deficiencias de uso
> * Crear alertas de gastos innecesarios o inusuales
> * Exportar datos

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

- Debe tener una cuenta de Azure.
- Debe tener un registro de prueba o una suscripción de pago en Cloudyn.

## <a name="open-the-cloudyn-portal"></a>Abrir el portal de Cloudyn

Revise todos los usos y costos en el portal de Cloudyn. Abra el portal de Cloudyn desde Azure Portal o vaya a https://azure.cloudyn.com e inicie sesión.

## <a name="track-usage-and-cost-trends"></a>Realizar un seguimiento de las tendencias de uso y costos

El seguimiento del dinero real gastado en uso y costos se realiza con informes a lo largo del tiempo para identificar tendencias. Para empezar a observar tendencias, use el informe de costo real a lo largo del tiempo. En la parte superior izquierda del portal, haga clic en **Costs** > **Cost Analysis** > **Actual Cost Over Time** (Costos > Análisis de costos > Costo real a lo largo del tiempo). Cuando abra el informe por primera vez, no tendrá grupos ni filtros aplicados.

A continuación se muestra un informe de ejemplo:

![Ejemplo de informe de costo real a lo largo del tiempo](./media/tutorial-review-usage/actual-cost01.png)

El informe muestra todos los gastos de los últimos 30 días. Para ver solo el gasto de los servicios de Azure, aplique el grupo de servicio y, a continuación, filtre por todos los servicios de Azure. En la siguiente imagen se muestran los servicios de filtrado.

![Ejemplo que muestra los servicios de Azure filtrados](./media/tutorial-review-usage/actual-cost02.png)

En el ejemplo anterior, se gastó menos dinero a partir del 29/10/2018. Sin embargo, un exceso de columnas puede ocultar una tendencia obvia. Puede cambiar la vista de informe a un gráfico de línea o área para ver los datos mostrados en otras vistas. En la siguiente imagen muestra la tendencia con mayor claridad.

![Ejemplo que muestra una tendencia decreciente de costos de máquinas virtuales de Azure](./media/tutorial-review-usage/actual-cost03.png)

Siguiendo con el ejemplo, puede ver que se redujo el costo de la máquina virtual de Azure. Los costos de otros servicios de Azure también comienzan a reducirse durante ese día. Por lo tanto, ¿qué causó esa reducción en los gastos? En este ejemplo, se completó un gran proyecto de trabajo por lo que también se redujo el consumo de muchos servicios de Azure.

Para ver un tutorial en vídeo acerca del seguimiento de las tendencias de uso y costo, consulte [Analyzing your cloud billing data vs. time with Cloudyn](https://youtu.be/7LsVPHglM0g) (Análisis de los datos frente al tiempo de facturación en la nube con Cloudyn).

## <a name="detect-usage-inefficiencies"></a>Detectar deficiencias de uso

Los informes de optimizador mejoran la eficacia, optimizan el uso e identifican formas de ahorrar dinero invertido en recursos de nube. Resultan especialmente útiles con las recomendaciones de ajuste de tamaño rentables diseñadas para ayudar a reducir las máquinas virtuales inactivas o costosas.

Un problema común que afecta a las organizaciones cuando mueven recursos inicialmente a la nube es su estrategia de virtualización. A menudo usan un enfoque similar al que usan para crear máquinas virtuales para el entorno de virtualización local. Además, supone que los costos se reducen moviendo sus máquinas virtuales locales a la nube, tal cual. Sin embargo, es improbable que este enfoque reduzca los costos.

El problema es que ya se ha pagado su infraestructura existente. Los usuarios pueden crear y mantener máquinas virtuales muy grandes en ejecución: inactivas o no, y con muy pocas consecuencias. Mover máquinas virtuales grandes o inactivas a la nube es probable que *aumente* los costos. La asignación de costos para recursos es importante al formalizar acuerdos con proveedores de servicios en la nube. Deberá pagar por aquello con lo que se comprometa, independientemente de si usa el recurso completamente.

El informe de recomendaciones de tamaño rentables identifica posibles ahorros anuales comparando la capacidad de tipo de instancia de máquina virtual con los datos de uso de memoria y CPU históricos correspondientes.  

En el menú de la parte superior del portal, haga clic en **Optimizer** > **Sizing Optimization** > **Cost Effective Sizing Recommendations** (Optimizador > Optimización de tamaño > Recomendaciones de tamaño rentables). Si es útil, aplique un filtro para reducir los resultados. A continuación se muestra una imagen de ejemplo.

![Informe de recomendación de ajuste de tamaño rentable para máquinas virtuales de Azure](./media/tutorial-review-usage/sizing01.png)

En este ejemplo, se pudieron ahorrar 2382 USD siguiendo las recomendaciones para cambiar los tipos de instancia de máquina virtual. Haga clic en el signo más (+) en **Detalles** para ver la primera recomendación. Aquí encontrará detalles acerca de la primera recomendación.

![Ejemplo que muestra detalles de recomendación](./media/tutorial-review-usage/sizing02.png)

Para ver los identificadores de instancia de máquina virtual, haga clic en el símbolo más junto a **Lista de candidatos**.

![Ejemplo que muestra una lista de candidatos de máquinas virtuales para cambiar tamaño](./media/tutorial-review-usage/sizing03.png)

Para ver un tutorial en vídeo acerca de cómo detectar deficiencias de uso, consulte [Optimizing VM Size in Cloudyn](https://youtu.be/1xaZBNmV704) (Optimización del tamaño de máquina virtual en Cloudyn).

Azure Cost Management también proporciona recomendaciones de ahorro de costos para los servicios de Azure. Para obtener más información, consulte [Tutorial: Optimización de los costos a partir de las recomendaciones](tutorial-acm-opt-recommendations.md).

## <a name="create-alerts-for-unusual-spending"></a>Crear alertas de gastos inusuales

También pueden alertar automáticamente a las partes interesadas sobre anomalías de gastos y riesgos de gastos innecesarios. Se pueden crear alertas fácilmente mediante informes que admitan alertas basadas en umbrales de presupuesto y costos.

Cree una alerta para cualquier gasto mediante cualquier informe de costos. En este ejemplo, use el informe de costo a lo largo del tiempo para recibir una notificación cuando el gasto de la máquina virtual de Azure se acerque al presupuesto total. Para crear la alerta es necesario realizar los pasos siguientes. En el menú de la parte superior del portal, haga clic en **Costs** > **Cost Analysis** > **Actual Cost Over Time** (Costos > Análisis de costos > Costo real a lo largo del tiempo). Establezca **Grupos** en **Servicio** y **Filter on the service (Filtrar el servicio)** en **Azure/VM**. En la parte superior derecha del informe, haga clic en **Acciones** y, a continuación, seleccione **Schedule report (Programar informe)**.

En el cuadro Save or Schedule this report (Guardar o programar este informe), utilice la pestaña **Scheduling** (Programación) para que se envíe a su propia dirección un correo electrónico del informe con la frecuencia que desee. Asegúrese de seleccionar **Send via email** (Enviar por correo electrónico). Las etiquetas, la agrupación y el filtrado que usa se incluyen en el informe enviado por correo electrónico. Haga clic en la pestaña **Umbral** y seleccione **Actual Cost vs. Threshold (Costo real frente a umbral)**. Si tiene un presupuesto total de 20 000 USD y desea una notificación cuando los costos se acerquen a la mitad, cree una **alerta roja** en 10 000 dólares y una **alerta amarilla** en 9 000 USD. No incluya comas en los valores que especifique. A continuación, elija el número de alertas consecutivas. Cuando recibe el número total de alertas especificado, no se envían más alertas. Guarde el informe programado.

![Ejemplo que muestra alertas rojas y amarillas según los umbrales de gastos](./media/tutorial-review-usage/schedule-alert01.png)

También puede elegir la métrica del umbral de porcentaje frente a presupuesto para crear alertas. Si usa esa métrica, puede emplear porcentajes de presupuesto en lugar de valores de divisa.

## <a name="export-data"></a>Exportar datos

De igual forma que puede crear alertas de los informes, también puede exportar los datos de cualquier informe. Por ejemplo, es posible que desee exportar una lista de las cuentas de Cloudyn u otros datos de usuario. Para exportar un informe, ábralo y, en la parte superior derecha, haga clic en **Actions** (Acciones). Una de las acciones disponibles es **Export all report data** (Exportar todos los datos del informe), lo que le permitirá descargar o imprimir la información. También puede seleccionar **Schedule report** (Programar informe) si desea programar un informe para que se envíe por correo electrónico.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial aprendió lo siguiente:

> [!div class="checklist"]
> * Realizar un seguimiento de las tendencias de uso y costos
> * Detectar deficiencias de uso
> * Crear alertas de gastos innecesarios o inusuales
> * Exportar datos


Avance al siguiente tutorial para aprender a pronosticar gastos mediante datos históricos.

> [!div class="nextstepaction"]
> [Previsión de gastos futuros](tutorial-forecast-spending.md)
