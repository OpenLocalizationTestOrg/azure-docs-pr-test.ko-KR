---
title: "문제 해결: Machine Learning 작업 영역 만들기 및 연결 | Microsoft Docs"
description: "Azure 기계 학습 작업 영역 만들기 및 연결과 관련된 일반적인 문제에 대한 해결 방법"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="d3ad2-103">문제 해결 가이드: 기계 학습 작업 영역 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="d3ad2-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="d3ad2-104">이 가이드에서는 Azure 기계 학습 작업 영역을 설정할 때 자주 발생하는 몇 가지 문제에 대한 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="d3ad2-105">작업 영역 소유자</span><span class="sxs-lookup"><span data-stu-id="d3ad2-105">Workspace owner</span></span>
<span data-ttu-id="d3ad2-106">Machine Learning Studio에서 작업 영역을 열려면 작업 영역을 만드는 데 사용한 Microsoft 계정으로 로그인하거나 작업 공간에 조인하라는 소유자의 초대를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="d3ad2-107">Azure Portal에서 액세스를 구성하는 기능을 포함하여 작업 영역을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="d3ad2-108">작업 영역을 관리하는 방법에 대한 자세한 내용은 [Azure 기계 학습 작업 영역 관리]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="d3ad2-109">[Azure 기계 학습 작업 영역 관리]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="d3ad2-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="d3ad2-110">허용되는 지역</span><span class="sxs-lookup"><span data-stu-id="d3ad2-110">Allowed regions</span></span>
<span data-ttu-id="d3ad2-111">기계 학습은 현재 제한된 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="d3ad2-112">구독에 이들 지역 중 한 곳이 포함되어 있지 않으면 “허용되는 지역에 구독이 없습니다.”라는 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="d3ad2-113">구독에 영역을 추가하도록 요청하려면 Azure Portal에서 Microsoft 지원 요청을 만들고 문제 유형으로 **청구**를 선택한 다음 프롬프트에 따라 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="d3ad2-114">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="d3ad2-114">Storage account</span></span>
<span data-ttu-id="d3ad2-115">기계 학습 서비스에서 데이터를 저장하려면 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="d3ad2-116">기존 저장소 계정을 사용하거나, 새 저장소 계정을 만들 수 있는 할당량이 있는 경우 새 기계 학습 작업 영역을 만들 때 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="d3ad2-117">새 Machine Learning 작업 영역이 만들어진 후에 작업 영역을 만드는 데 사용한 Microsoft 계정을 사용하여 Machine Learning Studio에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="d3ad2-118">"작업 영역을 찾을 수 없음"(다음 스크린샷과 유사) 오류 메시지가 나타나는 경우 다음 단계를 사용하여 브라우저 쿠키를 삭제하세요.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![작업 영역을 찾을 수 없음][screen3]

<span data-ttu-id="d3ad2-120">**브라우저 쿠키를 삭제하려면**</span><span class="sxs-lookup"><span data-stu-id="d3ad2-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="d3ad2-121">Internet Explorer를 사용하는 경우 오른쪽 위에 있는 **도구** 단추를 클릭하고 **인터넷 옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![인터넷 옵션][screen4]

2. <span data-ttu-id="d3ad2-123">**일반** 탭에서 **삭제…**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-123">Under the **General** tab, click **Delete…**</span></span>

![일반 탭][screen5]

3. <span data-ttu-id="d3ad2-125">**검색 기록 삭제** 대화 상자에서 **쿠키 및 웹 사이트 데이터**가 선택되었는지 확인하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![쿠키 삭제][screen6]

<span data-ttu-id="d3ad2-127">쿠키를 삭제한 후 브라우저를 다시 시작하고 [Microsoft Azure 기계 학습](https://studio.azureml.net) 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="d3ad2-128">사용자 이름과 암호를 묻는 메시지가 표시되면 작업 영역을 만드는 데 사용한 동일한 Microsoft 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="d3ad2-129">설명</span><span class="sxs-lookup"><span data-stu-id="d3ad2-129">Comments</span></span>

<span data-ttu-id="d3ad2-130">Microsoft는 기계 학습 환경을 가능한 한 원활하게 만들기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="d3ad2-131">의견이나 문제가 있을 경우 더 나은 서비스를 제공할 수 있도록 [Azure 기계 학습 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) 에 게시해 주세요.</span><span class="sxs-lookup"><span data-stu-id="d3ad2-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
