---
title: "aaaProvision IPython 노트북 서버와 Azure 데이터 과학 가상 컴퓨터 | Microsoft Docs"
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
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a><span data-ttu-id="e48ad-103">Azure 데이터 과학 가상 컴퓨터를 IPython Notebook 서버로 프로비전</span><span class="sxs-lookup"><span data-stu-id="e48ad-103">Provision Azure Data Science Virtual Machines as IPython Notebook Servers</span></span>
<span data-ttu-id="e48ad-104">지침은 제공 여기에서 설명 하는 방법을 IPython 노트북 서버로 Azure VM 및 SQL 서비스는 Azure VM을 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-104">Instructions are provided here that describe how tooset up an Azure VM and an Azure VM with SQL Service as IPython Notebook servers.</span></span> <span data-ttu-id="e48ad-105">IPython 노트북, Azure 저장소 탐색기, AzCopy를 뿐 아니라 데이터 과학 프로젝트에 유용한 기타 유틸리티와 같은 도구를 지 원하는 hello Windows 가상 컴퓨터 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-105">hello Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, and AzCopy, as well as other utilities that are useful for data science projects.</span></span> <span data-ttu-id="e48ad-106">Azure 저장소 탐색기 및 AzCopy, 예를 들어 편리 하 게 방법 tooupload 데이터 저장소를 제공할 tooAzure에서 로컬 컴퓨터 또는 toodownload 것 tooyour 로컬 컴퓨터 저장소에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways tooupload data tooAzure storage from your local machine or toodownload it tooyour local machine from storage.</span></span> 

<span data-ttu-id="e48ad-107">이 메뉴 tootopics tooset hello 다양 한 데이터 과학 환경에서 어떻게 사용 hello를 설명 하는 링크 [팀 데이터 과학 프로세스 (TDSP)](data-science-process-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-107">This menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="e48ad-108">여러 유형의 Azure 가상 컴퓨터 프로 비전 할 수 구성과 toobe 클라우드 기반 데이터 과학 환경의 일부로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-108">Several types of Azure virtual machines can be provisioned and configured toobe used as part of a cloud-based data science environment.</span></span> <span data-ttu-id="e48ad-109">가상 컴퓨터의 어떤 버전에 대 한 toouse hello 유형 및 데이터 toobe의 수량에 따라 하는 hello 결정 기계 학습과 hello 클라우드에서 해당 데이터에 대 한 hello 목표 대상으로 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-109">hello decision about which flavor of virtual machine toouse depends on hello type and quantity of data toobe modeled with machine learning, and hello target destination for that data in hello cloud.</span></span> 

* <span data-ttu-id="e48ad-110">이 결정을 내릴 때 hello 질문 tooconsider에 대 한 지침을 참조 하십시오. [Plan Your Azure 시스템 학습 데이터 과학 환경](machine-learning-data-science-plan-your-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-110">For guidance on hello questions tooconsider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span></span> 
* <span data-ttu-id="e48ad-111">고급 분석을 수행 하는 경우 발생할 수 있습니다 hello 시나리오 중 일부의 카탈로그에 대 한 참조 [고급 분석 프로세스 및 Azure 기계 학습에서 기술에 대 한 시나리오 hello](machine-learning-data-science-plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="e48ad-111">For a catalog of some of hello scenarios you might encounter when doing advanced analytics, see [Scenarios for hello Advanced Analytics Process and Technology in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)</span></span>

<span data-ttu-id="e48ad-112">다음 두 가지 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-112">Two sets of instructions are provided:</span></span>

* <span data-ttu-id="e48ad-113">[고급 분석에 대 한 IPython 노트북 서버도 Azure 가상 컴퓨터를 설정할](machine-learning-data-science-setup-virtual-machine.md) tooprovision IPython 전자 필기장 및 기타 도구로 Azure 가상 컴퓨터 된 경우 toodo 데이터 과학을 사용 하는 방법을 보여 주는 SQL이 아닌 Azure 저장소의 형태 사용 되는 toostore hello 데이터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-113">[Set up an Azure virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-virtual-machine.md) shows how tooprovision an Azure virtual machine with IPython Notebook and other tools used toodo data science for cases in which a form of Azure storage other than SQL can be used toostore hello data.</span></span>
* <span data-ttu-id="e48ad-114">[고급 분석에 대 한 IPython 노트북 서버도 Azure SQL Server 가상 컴퓨터를 설정할](machine-learning-data-science-setup-sql-server-virtual-machine.md) tooprovision IPython 전자 필기장 및 기타 도구로 Azure SQL Server 가상 컴퓨터는 된 경우 toodo 데이터 과학을 사용 하는 방법을 보여 주는 SQL 데이터베이스 사용 되는 toostore hello 데이터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-114">[Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md) shows how tooprovision an Azure SQL Server virtual machine with IPython Notebook and other tools used toodo data science for cases in which a SQL database can be used toostore  hello data.</span></span>

<span data-ttu-id="e48ad-115">프로 비전 하 고 구성 된 이러한 가상 컴퓨터 IPython 노트북 서버 hello 탐색 및 데이터의 처리에 대 한 Azure 기계 학습 및 hello 팀 데이터 과학 프로세스 (TDSP)와 함께에서 필요한 다른 작업으로 사용할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-115">Once provisioned and configured, these virtual machines are ready for use as IPython Notebook servers for hello exploration and processing of data, and for other tasks needed in conjunction with Azure Machine Learning and hello Team Data Science Process (TDSP).</span></span> <span data-ttu-id="e48ad-116">hello hello 데이터 과학 프로세스의 다음 단계에에서 매핑된 hello [TDSP 학습 경로](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 를 SQL Server 나 HDInsight에 대 한 데이터를 처리 하 고 Azure 사용 하 여 hello 데이터에서 학습을 위한 준비 과정에서 샘플링 하는 것이 있으면 이동 하는 단계를 포함할 수 있습니다 기계 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-116">hello next steps in hello data science process are mapped in hello [TDSP learning path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into SQL Server or HDInsight, process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

> [!NOTE]
> <span data-ttu-id="e48ad-117">Azure 가상 컴퓨터는 **종량제**로 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-117">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="e48ad-118">되 고 있지 tooensure toobe hello에가 가상 컴퓨터를 사용 하지 않는 경우 대금 청구를 **중지 (할당 취소)** hello에서 상태 [Azure 클래식 포털](http://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e48ad-118">tooensure that you are not being billed when not using your virtual machine, it has toobe in hello **Stopped (Deallocated)** state from hello [Azure Classic Portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="e48ad-119">단계별 지침을 보려면 어떻게 toodeallocate 가상 컴퓨터 참조 [종료를 취소할 때 사용 중이 아닌 가상 컴퓨터](machine-learning-data-science-setup-virtual-machine.md#shutdown)</span><span class="sxs-lookup"><span data-stu-id="e48ad-119">For step-by-step instructions or how toodeallocate you virtual machine, see  [Shutdown and deallocate virtual machine when not in use](machine-learning-data-science-setup-virtual-machine.md#shutdown)</span></span>
> 
> 

