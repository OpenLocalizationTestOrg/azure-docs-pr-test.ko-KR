---
title: "문제 해결: 만들고 tooa 기계 학습 작업 영역 연결 | Microsoft Docs"
description: "만들기 및 tooan Azure 기계 학습 작업 영역 연결의 일반적인 문제에 대 한 솔루션"
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
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="9d768-103">문제 해결 가이드: 만들고 tooan 기계 학습 작업 영역 연결</span><span class="sxs-lookup"><span data-stu-id="9d768-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="9d768-104">이 가이드에서는 Azure 기계 학습 작업 영역을 설정할 때 자주 발생하는 몇 가지 문제에 대한 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="9d768-105">작업 영역 소유자</span><span class="sxs-lookup"><span data-stu-id="9d768-105">Workspace owner</span></span>
<span data-ttu-id="9d768-106">기계 학습 스튜디오에서 작업 영역 tooopen 여야 tooreceive hello 소유자 toojoin hello 작업 영역에서 초대장이 필요 또는 toocreate hello 작업 영역에서 사용한 toohello Microsoft 계정으로에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="9d768-107">Hello Azure 포털에서에서 hello 기능 tooconfigure 액세스를 포함 하는 hello 작업 영역을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="9d768-108">작업 영역을 관리하는 방법에 대한 자세한 내용은 [Azure 기계 학습 작업 영역 관리]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d768-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[Azure 기계 학습 작업 영역 관리]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="9d768-110">허용되는 지역</span><span class="sxs-lookup"><span data-stu-id="9d768-110">Allowed regions</span></span>
<span data-ttu-id="9d768-111">기계 학습은 현재 제한된 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="9d768-112">구독에 해당이 영역 중 하나 포함 되어 있지 않으면, hello 오류 메시지가 표시 될 수 있습니다, 그리고 "에 구독이 없습니다 hello 영역을 허용 합니다."</span><span class="sxs-lookup"><span data-stu-id="9d768-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="9d768-113">영역 수 toorequest tooyour 구독을 추가, hello Azure 포털에서에서 새 Microsoft 지원 요청을 만들거나, 선택 **청구** hello 문제 유형 및 다음으로 hello 메시지 표시 toosubmit 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="9d768-114">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="9d768-114">Storage account</span></span>
<span data-ttu-id="9d768-115">hello 기계 학습 서비스 저장소 계정 toostore 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="9d768-116">기존 저장소 계정을 사용할 수 있습니다 또는 (있는 경우 할당량 toocreate 새 저장소 계정) hello 새 기계 학습 작업 영역을 만들 때 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="9d768-117">Hello 새 기계 학습 작업 영역을 만든 후 toocreate hello 작업 영역을 사용 하는 hello Microsoft 계정을 사용 하 여 tooMachine 학습 스튜디오에에서 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="9d768-118">"작업 영역 찾을 수 없음" (다음 스크린샷 유사한 toohello) hello 오류 메시지에서 발생 하는 경우 브라우저 쿠키 사용 hello toodelete 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9d768-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![작업 영역을 찾을 수 없음][screen3]

<span data-ttu-id="9d768-120">**toodelete 브라우저 쿠키**</span><span class="sxs-lookup"><span data-stu-id="9d768-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="9d768-121">Internet Explorer를 사용 하면 클릭 hello **도구** hello 오른쪽 위 모퉁이 클릭 한 선택 **인터넷 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![인터넷 옵션][screen4]

2. <span data-ttu-id="9d768-123">Hello에서 **일반** 탭을 클릭 **삭제 중...**</span><span class="sxs-lookup"><span data-stu-id="9d768-123">Under hello **General** tab, click **Delete…**</span></span>

![일반 탭][screen5]

3. <span data-ttu-id="9d768-125">Hello에 **검색 기록 삭제** 대화 상자의 **쿠키 및 웹 사이트 데이터가** 을 선택한 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![쿠키 삭제][screen6]

<span data-ttu-id="9d768-127">Hello 브라우저를 다시 시작 하 고 toohello 이동 하 여 hello 쿠키를 삭제 한 후 [Microsoft Azure 기계 학습](https://studio.azureml.net) 페이지.</span><span class="sxs-lookup"><span data-stu-id="9d768-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="9d768-128">사용자 이름 및 암호를 입력에 대 한 메시지가 표시 되 면 hello toocreate hello 작업 영역을 사용 하는 동일한 Microsoft 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="9d768-129">설명</span><span class="sxs-lookup"><span data-stu-id="9d768-129">Comments</span></span>

<span data-ttu-id="9d768-130">목표는 toomake hello 최대한 원활 하 게 기계 학습 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="9d768-131">의견이 나 문제 hello에 게시 하세요 [Azure 기계 학습 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us 서비스를 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d768-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
