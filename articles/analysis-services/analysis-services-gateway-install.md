---
title: "온-프레미스 데이터 게이트웨이 aaaInstall | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall 및 온-프레미스 데이터 게이트웨이 구성 합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="1ed9a-103">온-프레미스 데이터 게이트웨이 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="1ed9a-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="1ed9a-104">온-프레미스 데이터 게이트웨이 하나 이상의 Azure Analysis Services 서버에 동일한 hello 때 필요 지역 tooon 온-프레미스 데이터 원본 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="1ed9a-105">hello 게이트웨이에 대 한 자세한 정보는 toolearn 참조 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ed9a-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1ed9a-106">Prerequisites</span></span>
<span data-ttu-id="1ed9a-107">**최소 요구 사항:**</span><span class="sxs-lookup"><span data-stu-id="1ed9a-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="1ed9a-108">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="1ed9a-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="1ed9a-109">64비트 버전의 Windows 7/Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="1ed9a-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="1ed9a-110">**권장:**</span><span class="sxs-lookup"><span data-stu-id="1ed9a-110">**Recommended:**</span></span>

* <span data-ttu-id="1ed9a-111">8 코어 CPU</span><span class="sxs-lookup"><span data-stu-id="1ed9a-111">8 Core CPU</span></span>
* <span data-ttu-id="1ed9a-112">8GB 메모리</span><span class="sxs-lookup"><span data-stu-id="1ed9a-112">8 GB Memory</span></span>
* <span data-ttu-id="1ed9a-113">64비트 버전의 Windows 2012 R2 이상</span><span class="sxs-lookup"><span data-stu-id="1ed9a-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="1ed9a-114">**중요 고려 사항:**</span><span class="sxs-lookup"><span data-stu-id="1ed9a-114">**Important considerations:**</span></span>

* <span data-ttu-id="1ed9a-115">Azure와 게이트웨이 등록 하는 경우 설치를 하는 동안에 구독에 대 한 hello 기본 영역이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="1ed9a-116">다른 지역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-116">You can choose a different region.</span></span> <span data-ttu-id="1ed9a-117">서버가 여러 지역에 있는 경우 각 지역에 대한 게이트웨이를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="1ed9a-118">hello 게이트웨이 도메인 컨트롤러에 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="1ed9a-119">단일 컴퓨터에는 하나의 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="1ed9a-120">에 남아 있으며 toosleep는 설명 하지 않습니다 하는 컴퓨터에서 hello 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="1ed9a-121">컴퓨터 tooyour 무선으로 연결 된 네트워크의 hello 게이트웨이 설치 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="1ed9a-122">성능이 감소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-122">Performance can be diminished.</span></span>


## <span data-ttu-id="1ed9a-123"><a name="download"></a>다운로드</span><span class="sxs-lookup"><span data-stu-id="1ed9a-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="1ed9a-124">Hello 게이트웨이 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="1ed9a-125"><a name="install"></a>설치</span><span class="sxs-lookup"><span data-stu-id="1ed9a-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="1ed9a-126">설치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-126">Run setup.</span></span>

2. <span data-ttu-id="1ed9a-127">위치 선택, hello 조건에 동의 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![설치 위치 및 사용 조건](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="1ed9a-129">**온-프레미스 데이터 게이트웨이(권장)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="1ed9a-130">Azure Analysis Services는 개인 모드를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-130">Azure Analysis Services does not support personal mode.</span></span>

   ![게이트웨이 유형 선택](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="1ed9a-132">계정 toosign tooAzure 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="1ed9a-133">hello 계정은 테 넌 트의 Azure Active Directory에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="1ed9a-134">이 계정은 hello 게이트웨이 관리자에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-134">This account is used for hello gateway administrator.</span></span> 

   ![계정 toosign tooAzure에 입력](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="1ed9a-136">도메인 계정으로 로그인 하는 경우 tooyour 조직 계정을 Azure AD에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="1ed9a-137">조직 계정으로 hello 게이트웨이 관리자에 게 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="1ed9a-138"><a name="register"></a>등록</span><span class="sxs-lookup"><span data-stu-id="1ed9a-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="1ed9a-139">순서 toocreate Azure에서 게이트웨이 리소스 hello 게이트웨이 클라우드 서비스와 함께 설치 하는 hello 로컬 인스턴스를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="1ed9a-140">**이 컴퓨터에 새 게이트웨이 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-140">Select **Register a new gateway on this computer**.</span></span>

    ![등록](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="1ed9a-142">게이트웨이에 대한 이름 및 복구 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="1ed9a-143">기본적으로 hello 게이트웨이 구독의 기본 영역을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="1ed9a-144">다른 지역 tooselect 필요한 경우에 선택 **변경 지역**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![등록](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="1ed9a-146"><a name="create-resource"></a>Azure 게이트웨이 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ed9a-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="1ed9a-147">설치 된 게이트웨이 등록 한 후 Azure 구독에서 게이트웨이 리소스 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="1ed9a-148">Hello로 tooAzure에 동일한 로그인 hello 게이트웨이 등록할 때 사용 되는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="1ed9a-149">Azure Portal에서 **새 서비스 만들기** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이** > **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![게이트웨이 리소스 만들기](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="1ed9a-151">**연결 게이트웨이 만들기**에서 이러한 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="1ed9a-152">**이름**: 게이트웨이 리소스의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="1ed9a-153">**구독**: 선택 hello 게이트웨이 리소스와 Azure 구독 tooassociate 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="1ed9a-154">이 구독 해야 hello 서버에 있는 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="1ed9a-155">hello 기본 구독 hello toosign에 사용한 Azure 계정 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="1ed9a-156">**리소스 그룹**: 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="1ed9a-157">**위치**: hello 선택 영역에 게이트웨이 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="1ed9a-158">**설치 이름**: 게이트웨이 설치 선택 되어 있지 않으면 선택 hello 게이트웨이 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="1ed9a-159">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="1ed9a-160"><a name="connect-servers"></a>서버 toohello 게이트웨이 리소스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="1ed9a-161">Azure Analysis Services 서버 개요에서 **온-프레미스 데이터 게이트웨이**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![서버 toogateway 연결](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="1ed9a-163">**온-프레미스 데이터 게이트웨이 tooconnect 선택**게이트웨이 리소스를 선택한 다음 클릭 **연결 선택한 게이트웨이**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![서버 toogateway 리소스 연결](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="1ed9a-165">게이트웨이 hello 목록에 나타나지 않으면 서버 가능성이 없는 경우에 hello hello 게이트웨이 등록 하는 경우 지정한 hello 영역으로 같은 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="1ed9a-166">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-166">That's it.</span></span> <span data-ttu-id="1ed9a-167">모든 문제 해결을 수행 하거나 tooopen 포트를 필요한 경우 수 있는지 toocheck 아웃 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9a-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ed9a-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ed9a-168">Next steps</span></span>
* [<span data-ttu-id="1ed9a-169">Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="1ed9a-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="1ed9a-170">Azure Analysis Services에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="1ed9a-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
