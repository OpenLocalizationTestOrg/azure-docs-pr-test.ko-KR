---
title: "Azure 데이터 과학 가상 컴퓨터를 IPython Notebook 서버로 프로비전 | Microsoft Docs"
description: "지원 도구를 사용하여 데이터 과학 가상 컴퓨터를 IPython Notebook 서버로 설정합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: db1ffb2a226a087ecea2ea6f560c6b803e33d8c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a><span data-ttu-id="5625f-103">Azure 데이터 과학 가상 컴퓨터를 IPython Notebook 서버로 프로비전</span><span class="sxs-lookup"><span data-stu-id="5625f-103">Provision Azure Data Science Virtual Machines as IPython Notebook Servers</span></span>
<span data-ttu-id="5625f-104">Azure VM 및 SQL 서비스 포함 Azure VM을 IPython Notebook 서버로 설정하는 방법을 설명하는 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-104">Instructions are provided here that describe how to set up an Azure VM and an Azure VM with SQL Service as IPython Notebook servers.</span></span> <span data-ttu-id="5625f-105">Windows 가상 컴퓨터는 IPython Notebook, Azure Storage Explorer 및 AzCopy와 같은 지원 도구뿐만 아니라 데이터 과학 프로젝트에 유용한 기타 유틸리티로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-105">The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, and AzCopy, as well as other utilities that are useful for data science projects.</span></span> <span data-ttu-id="5625f-106">예를 들어 Azure 저장소 탐색기와 AzCopy는 로컬 컴퓨터에서 Azure 저장소로 데이터를 업로드하거나 저장소에서 로컬 컴퓨터로 데이터를 다운로드하는 데 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure storage from your local machine or to download it to your local machine from storage.</span></span> 

<span data-ttu-id="5625f-107">이 메뉴는 [TDSP(팀 데이터 과학 프로세스)](data-science-process-overview.md)에서 사용되는 다양한 데이터 과학 환경의 설정 방법을 설명하는 항목에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-107">This menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="5625f-108">여러 유형의 Azure 가상 컴퓨터를 프로비전하고 클라우드 기반 데이터 과학 환경의 일부로 사용하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-108">Several types of Azure virtual machines can be provisioned and configured to be used as part of a cloud-based data science environment.</span></span> <span data-ttu-id="5625f-109">사용할 가상 컴퓨터 유형에 대한 결정은 기계 학습으로 모델링할 데이터의 유형 및 양과 클라우드에서 해당 데이터의 대상에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-109">The decision about which flavor of virtual machine to use depends on the type and quantity of data to be modeled with machine learning, and the target destination for that data in the cloud.</span></span> 

* <span data-ttu-id="5625f-110">이러한 결정을 내릴 때 고려할 질문에 대한 지침은 [Azure 기계 학습 데이터 과학 환경 계획](machine-learning-data-science-plan-your-environment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5625f-110">For guidance on the questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span></span> 
* <span data-ttu-id="5625f-111">고급 분석을 수행할 때 발생할 수 있는 일부 시나리오의 카탈로그는 [Azure 기계 학습의 고급 분석 프로세스 및 기술 시나리오](machine-learning-data-science-plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="5625f-111">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Advanced Analytics Process and Technology in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)</span></span>

<span data-ttu-id="5625f-112">다음 두 가지 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-112">Two sets of instructions are provided:</span></span>

* <span data-ttu-id="5625f-113">[고급 분석을 위해 Azure 가상 컴퓨터를 IPython Notebook으로 설정](machine-learning-data-science-setup-virtual-machine.md) 에서는 SQL이 아닌 Azure 저장소를 사용하여 데이터를 저장할 수 있는 경우 IPython Notebook 및 데이터 과학을 수행하는 데 사용되는 기타 도구와 함께 Azure 가상 컴퓨터를 프로비전하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-113">[Set up an Azure virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-virtual-machine.md) shows how to provision an Azure virtual machine with IPython Notebook and other tools used to do data science for cases in which a form of Azure storage other than SQL can be used to store the data.</span></span>
* <span data-ttu-id="5625f-114">[고급 분석을 위해 Azure SQL Server 가상 컴퓨터를 IPython Notebook으로 설정](machine-learning-data-science-setup-sql-server-virtual-machine.md)에서는 SQL Database를 사용하여 데이터를 저장할 수 있는 경우 IPython Notebook 및 데이터 과학을 수행하는 데 사용되는 기타 도구와 함께 Azure SQL Server 가상 컴퓨터를 프로비전하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-114">[Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md) shows how to provision an Azure SQL Server virtual machine with IPython Notebook and other tools used to do data science for cases in which a SQL database can be used to store  the data.</span></span>

<span data-ttu-id="5625f-115">프로비전 및 구성한 후에는 데이터 탐색 및 처리, Azure 기계 학습 및 TDSP(팀 데이터 과학 프로세스)와 함께 수행할 다른 작업 등에 이러한 가상 컴퓨터를 IPython Notebook 서버로 사용할 준비가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-115">Once provisioned and configured, these virtual machines are ready for use as IPython Notebook servers for the exploration and processing of data, and for other tasks needed in conjunction with Azure Machine Learning and the Team Data Science Process (TDSP).</span></span> <span data-ttu-id="5625f-116">데이터 과학 프로세스의 다음 단계는 [TDSP 학습 경로](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 에서 매핑되며, 데이터를 SQL Server 또는 HDInsight로 이동한 후 Azure 기계 학습에서 데이터를 통해 학습할 준비를 수행하면서 데이터를 처리 및 샘플링하는 단계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-116">The next steps in the data science process are mapped in the [TDSP learning path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into SQL Server or HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

> [!NOTE]
> <span data-ttu-id="5625f-117">Azure 가상 컴퓨터는 **종량제**로 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-117">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="5625f-118">가상 컴퓨터를 사용하지 않을 때 비용이 청구되지 않도록 하려면 **Azure 클래식 포털** 에서 [중지(할당 해제)](http://manage.windowsazure.com/)상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5625f-118">To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state from the [Azure Classic Portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="5625f-119">가상 컴퓨터를 할당 해제하는 방법 및 단계별 지침은 [사용하지 않을 때 가상 컴퓨터 종료 및 할당 해체](machine-learning-data-science-setup-virtual-machine.md#shutdown)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5625f-119">For step-by-step instructions or how to deallocate you virtual machine, see  [Shutdown and deallocate virtual machine when not in use](machine-learning-data-science-setup-virtual-machine.md#shutdown)</span></span>
> 
> 

