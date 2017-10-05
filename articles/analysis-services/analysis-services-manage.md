---
title: "Azure Analysis Services 관리 | Microsoft Docs"
description: "Azure에서 Analysis Services 서버를 관리하는 방법을 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="6aa7a-103">Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="6aa7a-103">Manage Analysis Services</span></span>
<span data-ttu-id="6aa7a-104">Azure에 Analysis Services 서버를 만들었으면 즉시 또는 조만간에 수행해야 하는 몇 가지 운영 및 관리 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="6aa7a-105">예를 들어 데이터 새로 고침 처리를 실행하거나, 서버의 모델에 대한 액세스 권한이 있는 사용자를 제어하거나, 서버의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="6aa7a-106">일부 관리 작업은 Azure 포털에서만, 일부 다른 작업은 SSMS(SQL Server Management Studio)에서만, 일부 작업은 둘 중 하나에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="6aa7a-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="6aa7a-107">Azure portal</span></span>
<span data-ttu-id="6aa7a-108">[Azure Portal](http://portal.azure.com/)은 서버를 생성 및 삭제하고, 서버 리소스를 모니터링하고, 크기를 변경하고, 서버에 액세스할 수 있는 사용자를 관리할 수 있는 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="6aa7a-109">몇 가지 문제가 발생하면 지원 요청을 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-109">If you're having some problems, you can also submit a support request.</span></span>

![Azure에서 서버 이름 가져오기](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="6aa7a-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="6aa7a-111">SQL Server Management Studio</span></span>
<span data-ttu-id="6aa7a-112">Azure에서 서버를 연결하는 것은 조직에서 서버 인스턴스를 연결하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="6aa7a-113">SSMS에서는 데이터 처리와 같이 동일한 작업을 많이 수행하거나 처리 스크립트를 만들고 역할을 관리하고 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="6aa7a-115">SSMS 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="6aa7a-115">Download and install SSMS</span></span>
<span data-ttu-id="6aa7a-116">모든 최신 기능과 Azure Analysis Services 서버에 연결할 때 가장 원활한 환경을 얻으려면 최신 버전의 SSMS를 사용하고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="6aa7a-117">[SQL Server Management Studio를 다운로드합니다](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="6aa7a-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="6aa7a-118">SSMS로 연결</span><span class="sxs-lookup"><span data-stu-id="6aa7a-118">To connect with SSMS</span></span>
 <span data-ttu-id="6aa7a-119">SSMS를 사용할 때 처음으로 서버에 연결하기 전에 Analysis Services 관리자 그룹에 사용자 이름이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="6aa7a-120">자세한 내용은 이 문서의 뒷부분에 나오는 [서버 관리자](#server-administrators)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="6aa7a-121">먼저 서버 이름을 가져온 후에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="6aa7a-122">**Azure 포털** > 서버 > **개요** > **서버 이름**에서 서버 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="6aa7a-124">SSMS > **개체 탐색기**에서 **연결** > **Analysis Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="6aa7a-125">**서버에 연결** 대화 상자에서 서버 이름을 붙여넣은 다음 **인증**에서 다음 인증 유형 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="6aa7a-126">**Windows 인증** - Windows 도메인\사용자 이름 및 암호 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="6aa7a-127">**Active Directory 암호 인증** - 조직의 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="6aa7a-128">예를 들어 비도메인 가입 컴퓨터에서 연결하는 경우에 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="6aa7a-129">**Active Directory 범용 인증** - [비대화형 또는 다단계 인증](../sql-database/sql-database-ssms-mfa-authentication.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![SSMS에서 연결](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="6aa7a-131">서버 관리자 및 데이터베이스 사용자</span><span class="sxs-lookup"><span data-stu-id="6aa7a-131">Server administrators and database users</span></span>
<span data-ttu-id="6aa7a-132">Azure Analysis Services에서는 두 가지 유형의 사용자, 서버 관리자 및 데이터베이스 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="6aa7a-133">두 가지 유형의 사용자 모두 Azure Active Directory에 포함되어야 하며 조직 전자 메일 주소 또는 UPN으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="6aa7a-134">자세한 내용은 [인증 및 사용자 권한](analysis-services-manage-users.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="6aa7a-135">연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6aa7a-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="6aa7a-136">SSMS를 사용하여 연결할 때 문제가 발생하는 경우 로그인 캐시를 지워야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="6aa7a-137">아무것도 디스크로 캐시되지 않습니다. 캐시를 지우려면 연결 프로세스를 닫았다가 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6aa7a-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6aa7a-138">Next steps</span></span>
<span data-ttu-id="6aa7a-139">새 서버에 테이블 형식 모델을 아직 배포하지 않았으면 지금이야말로 좋은 기회입니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="6aa7a-140">자세한 내용은 [Azure Analysis Services에 배포](analysis-services-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="6aa7a-141">서버에 모델을 배포한 경우에는 클라이언트 또는 브라우저를 통해 연결할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="6aa7a-142">자세한 내용은 [Azure Analysis Services 서버에서 데이터 가져오기](analysis-services-connect.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa7a-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

