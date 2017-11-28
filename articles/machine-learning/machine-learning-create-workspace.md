---
title: "Machine Learning 작업 영역 만들기 | Microsoft Docs"
description: "Azure 기계 학습 스튜디오의 작업 영역을 만드는 방법"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="2fcdc-103">Azure 기계 학습 작업 영역 만들기 및 공유</span><span class="sxs-lookup"><span data-stu-id="2fcdc-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="2fcdc-104">이 메뉴는 CAPS(Cortana 분석 프로세스)에서 사용하는 다양한 데이터 과학 환경을 설정하는 방법을 설명하는 항목에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="2fcdc-105">Azure 기계 학습 스튜디오를 사용하려면 기계 학습 작업 영역이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="2fcdc-106">이 작업 영역에는 실험을 만들고 관리, 게시하는 데 필요한 도구가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="2fcdc-107">작업 영역을 만들려면</span><span class="sxs-lookup"><span data-stu-id="2fcdc-107">To create a workspace</span></span>
1. <span data-ttu-id="2fcdc-108">[Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="2fcdc-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="2fcdc-109">로그인하여 작업 영역을 만들려면 Azure 구독 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="2fcdc-110">**+새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-110">Click **+New**</span></span>

3. <span data-ttu-id="2fcdc-111">**인텔리전스 + 분석**을 선택하고 **Machine Learning 작업 영역**을 클릭한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="2fcdc-112">작업 영역 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-112">Enter your workspace information</span></span>

    - <span data-ttu-id="2fcdc-113">*작업 영역 이름*은 공백으로 끝나지 않고 최대 260자로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="2fcdc-114">이름에는 다음과 같은 문자를 포함하지 않아야 합니다. `< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="2fcdc-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="2fcdc-115">사용자가 선택하거나 만든 *웹 서비스 계획*은 사용자가 선택한 연결된 *가격 책정 계층*과 함께, 이 작업 영역에서 웹 서비스를 배포하는 경우 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![새 작업 영역 만들기](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="2fcdc-117">**만들기**</span><span class="sxs-lookup"><span data-stu-id="2fcdc-117">Click **Create**</span></span>

<span data-ttu-id="2fcdc-118">작업 영역이 배포되면 Machine Learning Studio에서 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="2fcdc-119">Machine Learning Studio([https://studio.azureml.net/](https://studio.azureml.net/))로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="2fcdc-120">오른쪽 위 모서리에서 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![작업 영역 선택](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="2fcdc-122">**내 실험**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-122">Click **my experiments**.</span></span>

    ![실험 열기](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="2fcdc-124">작업 영역을 관리하는 방법에 대한 자세한 내용은 [Azure 기계 학습 작업 영역 관리](machine-learning-manage-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="2fcdc-125">작업 영역을 만드는 데 문제가 발생한 경우 [문제 해결 가이드: Machine Learning 작업 영역 만들기 및 연결](machine-learning-troubleshooting-creating-ml-workspace.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="2fcdc-126">Azure 기계 학습 작업 영역 공유</span><span class="sxs-lookup"><span data-stu-id="2fcdc-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="2fcdc-127">Machine Learning 작업 영역이 만들어진 후에는 사용자를 작업 영역에 초대하고 작업 영역과 모든 실험, 데이터 집합, Notebook 등에 대한 액세스를 공유할 수 있습니다. 이 두 역할 중 하나에 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="2fcdc-128">**사용자** - 작업 영역 사용자는 작업 영역에서 실험, 데이터 집합 등을 만들기, 열기, 수정 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="2fcdc-129">**소유자** - 소유자는 사용자가 수행할 수 있는 작업 외에도 작업 영역에 사용자를 초대 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="2fcdc-130">작업 영역을 만든 관리자 계정은 작업 영역 소유자 권한으로 작업 영역에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="2fcdc-131">그러나 구독에 있는 다른 관리자 또는 사용자에게는 작업 영역에 대한 액세스 권한이 자동으로 부여되지 않으며 명시적으로 초대해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="2fcdc-132">작업 영역을 공유하려면</span><span class="sxs-lookup"><span data-stu-id="2fcdc-132">To share a workspace</span></span>

1. <span data-ttu-id="2fcdc-133">Machine Learning Studio([https://studio.azureml.net/Home](https://studio.azureml.net/Home))에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="2fcdc-134">왼쪽 패널에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="2fcdc-135">**사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="2fcdc-136">페이지 맨 아래에 있는 **더 많은 사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Studio 설정](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="2fcdc-138">하나 이상의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-138">Enter one or more email addresses.</span></span> <span data-ttu-id="2fcdc-139">사용자에게는 유효한 Microsoft 계정(Azure Active Directory에서) 또는 Azure Active Directory의 조직 계정만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="2fcdc-140">사용자를 소유자 또는 사용자로 추가할지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="2fcdc-141">**확인** 확인 표시 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="2fcdc-142">추가된 각 사용자는 공유 작업 영역에 로그인하는 방법에 대한 설명이 포함된 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="2fcdc-143">이 작업 영역에서 웹 서비스를 배포 또는 관리할 수 있는 사용자인 경우 Azure 구독에서 참여자 또는 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fcdc-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



