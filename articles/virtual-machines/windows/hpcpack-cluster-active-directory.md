---
title: "Azure Active Directory와 HPC 팩 클러스터 | Microsoft Docs"
description: "Azure에서 HPC 팩 2016 클러스터를 Azure Active Directory와 통합하는 방법 알아보기"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: c5a06a9c810349b1bcce01c7f73563941a5af0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="91dbd-103">Azure Active Directory를 사용하여 Azure에서 HPC 팩 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="91dbd-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="91dbd-104">[Microsoft HPC 팩 2016](https://technet.microsoft.com/library/cc514029)은 Azure에서 HPC 팩 클러스터를 배포하는 관리자에 대해 Azure AD([Azure Active Directory](../../active-directory/index.md))와의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="91dbd-105">다음의 고급 태스크에 대해 이 문서의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-105">Follow the steps in this article for the following high level tasks:</span></span> 
* <span data-ttu-id="91dbd-106">수동으로 HPC 팩 클러스터를 Azure AD 테넌트와 통합</span><span class="sxs-lookup"><span data-stu-id="91dbd-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="91dbd-107">Azure의 HPC 팩 클러스터에서 작업 관리 및 예약</span><span class="sxs-lookup"><span data-stu-id="91dbd-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="91dbd-108">HPC 팩 클러스터 솔루션을 Azure AD와 통합하려면 기타 응용 프로그램과 서비스를 통합하는 표준 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span></span> <span data-ttu-id="91dbd-109">이 문서에서는 Azure AD의 기본 사용자 관리에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="91dbd-110">자세한 내용 및 백그라운드는 [Azure Active Directory 설명서](../../active-directory/index.md) 및 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91dbd-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="91dbd-111">통합의 이점</span><span class="sxs-lookup"><span data-stu-id="91dbd-111">Benefits of integration</span></span>


<span data-ttu-id="91dbd-112">Azure Active Directory(Azure AD)는 클라우드 솔루션에 대한 SSO(Single Sign-On) 액세스를 제공하는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span></span>

<span data-ttu-id="91dbd-113">HPC 팩 클러스터를 Azure AD와 통합하면 다음 목표를 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span></span>

* <span data-ttu-id="91dbd-114">HPC 팩 클러스터에서 기존 Active Directory 도메인 컨트롤러를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span></span> <span data-ttu-id="91dbd-115">배포 프로세스 속도를 높일 수 있고 비즈니스에 필요 없는 경우 클러스터의 유지 관리 비용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span></span>
* <span data-ttu-id="91dbd-116">Azure AD에서 가져온 다음 혜택을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-116">Leverage the following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="91dbd-117">SSO(Single sign-on)</span><span class="sxs-lookup"><span data-stu-id="91dbd-117">Single sign-on</span></span> 
    *   <span data-ttu-id="91dbd-118">Azure에서 HPC 팩 클러스터에 대한 로컬 AD ID 사용</span><span class="sxs-lookup"><span data-stu-id="91dbd-118">Using a local AD identity for the HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory 환경](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="91dbd-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="91dbd-120">Prerequisites</span></span>
* <span data-ttu-id="91dbd-121">**Azure 가상 컴퓨터에 배포된 HPC 팩 2016 클러스터** - 단계는 [Azure에서 HPC 팩 2016 클러스터 배포](hpcpack-2016-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91dbd-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="91dbd-122">이 문서의 단계를 완료하려면 헤드 노드의 DNS 이름 및 클러스터 관리자 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="91dbd-123">Azure Active Directory 통합은 HPC 팩 2016 이전에 HPC 팩의 버전에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="91dbd-124">**클라이언트 컴퓨터** - HPC 팩 클라이언트 유틸리티를 실행하는 Windows 또는 Windows Server 클라이언트 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span></span> <span data-ttu-id="91dbd-125">HPC 팩 웹 포털 또는 REST API를 사용하여 작업을 제출하려는 경우 사용자가 선택한 모든 클라이언트 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="91dbd-126">**HPC 팩 클라이언트 유틸리티** - Microsoft 다운로드 센터에서 사용할 수 있는 무료 설치 패키지를 사용하여 클라이언트 컴퓨터에서 HPC 팩 클라이언트 유틸리티를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span></span>


## <a name="step-1-register-the-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="91dbd-127">1단계: Azure AD 테넌트를 사용하여 HPC 클러스터 서버 등록</span><span class="sxs-lookup"><span data-stu-id="91dbd-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="91dbd-128">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="91dbd-129">왼쪽 메뉴에 있는 **Active Directory**를 클릭하고 구독에서 원하는 디렉터리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="91dbd-130">디렉터리에 있는 리소스에 액세스할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-130">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="91dbd-131">**사용자**를 클릭하고 사용자 계정이 이미 만든 또는 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="91dbd-132">**응용 프로그램** > **추가**를 클릭하고 **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="91dbd-133">마법사에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-133">Enter the following information in the wizard:</span></span>
    * <span data-ttu-id="91dbd-134">**이름** - HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="91dbd-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="91dbd-135">**유형**: **웹 응용 프로그램 및/또는 Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="91dbd-136">**로그온 URL**- 샘플의 기준 URL로 기본적으로 `https://hpcserver`입니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="91dbd-137">**앱 ID URI** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="91dbd-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="91dbd-138">`<Directory_name`>을 Azure AD 테넌트의 전체 이름(예: `hpclocal.onmicrosoft.com`)으로 바꾸고 `<application_name>`을 이전에 선택한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span></span>

5. <span data-ttu-id="91dbd-139">앱이 추가되면 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-139">After the app is added, click **Configure**.</span></span> <span data-ttu-id="91dbd-140">다음 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-140">Configure the following properties:</span></span>
    * <span data-ttu-id="91dbd-141">**응용 프로그램은 다중 테넌트**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="91dbd-142">**앱에 액세스하려면 사용자 할당 필요**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-142">Select **Yes** for **User assignment required to access app**.</span></span>

6. <span data-ttu-id="91dbd-143">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-143">Click **Save**.</span></span> <span data-ttu-id="91dbd-144">저장이 완료되면 **매니페스트 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="91dbd-145">이 작업은 응용 프로그램의 매니페스트 JavaScript 개체 표기법(JSON) 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="91dbd-146">`appRoles` 설정을 배치하고 다음 응용 프로그램 역할을 추가하여 다운로드한 매니페스트를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="91dbd-147">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-147">Save the file.</span></span> <span data-ttu-id="91dbd-148">그 다음 포털에서 **매니페스트 관리** > **매니페스트 업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="91dbd-149">그런 다음 편집된 매니페스트를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-149">You can then upload the edited manifest.</span></span>
8. <span data-ttu-id="91dbd-150">**사용자**를 클릭하고 사용자를 선택한 다음 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="91dbd-151">사용자에게 사용 가능한 역할(HpcUsers 또는 HpcAdminMirror) 중 하나를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span></span> <span data-ttu-id="91dbd-152">디렉터리에 추가 사용자가 있으면 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-152">Repeat this step with additional users in the directory.</span></span> <span data-ttu-id="91dbd-153">클러스터 사용자에 대한 배경 정보는 [클러스터 사용자 관리](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91dbd-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="91dbd-154">사용자를 관리하려면 [Azure Portal](https://portal.azure.com)에서 Azure Active Directory 미리 보기 블레이드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-the-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="91dbd-155">2단계: Azure AD 테넌트를 사용하여 HPC 클러스터 클라이언트 등록</span><span class="sxs-lookup"><span data-stu-id="91dbd-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="91dbd-156">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="91dbd-157">왼쪽 메뉴에 있는 **Active Directory**를 클릭하고 구독에서 원하는 디렉터리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="91dbd-158">디렉터리에 있는 리소스에 액세스할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-158">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="91dbd-159">**응용 프로그램** > **추가**를 클릭하고 **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="91dbd-160">마법사에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-160">Enter the following information in the wizard:</span></span>

    * <span data-ttu-id="91dbd-161">**이름** - HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="91dbd-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="91dbd-162">**형식** - **네이티브 클라이언트 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="91dbd-163">**URI 리디렉션** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="91dbd-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="91dbd-164">앱이 추가되면 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-164">After the app is added, click **Configure**.</span></span> <span data-ttu-id="91dbd-165">**클라이언트 ID** 값을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-165">Copy the **Client ID** value and save it.</span></span> <span data-ttu-id="91dbd-166">나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="91dbd-167">**다른 응용 프로그램에 대한 사용 권한**에서 **응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-167">In **Permissions to other applications**, click **Add Application**.</span></span> <span data-ttu-id="91dbd-168">1단계에서 만든 HpcPackClusterServer 응용 프로그램을 검색하고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="91dbd-169">**위임된 권한** 드롭다운에서 **HpcClusterServer 액세스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="91dbd-170">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-170">Then click **Save**.</span></span>


## <a name="step-3-configure-the-hpc-cluster"></a><span data-ttu-id="91dbd-171">3단계 - HPC 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="91dbd-171">Step 3: Configure the HPC cluster</span></span>

1. <span data-ttu-id="91dbd-172">Azure에서 HPC 팩 2016 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-172">Connect to the HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="91dbd-173">HPC PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="91dbd-174">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-174">Run the following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="91dbd-175">여기서,</span><span class="sxs-lookup"><span data-stu-id="91dbd-175">where</span></span>

    * <span data-ttu-id="91dbd-176">`AADTenant`은 `hpclocal.onmicrosoft.com`와 같은 Azure AD 테넌트 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="91dbd-177">`AADClientAppId`은 2단계에서 만든 앱의 클라이언트 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span></span>

4. <span data-ttu-id="91dbd-178">HpcSchedulerStateful 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-178">Restart the HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="91dbd-179">여러 개의 헤드 노드가 있는 클러스터에서는 헤드 노드에서 다음 PowerShell 명령을 실행하여 HpcSchedulerStateful 서비스의 기본 복제본을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-the-client"></a><span data-ttu-id="91dbd-180">4 단계: 클라이언트에서 작업 관리 및 제출</span><span class="sxs-lookup"><span data-stu-id="91dbd-180">Step 4: Manage and submit jobs from the client</span></span>

<span data-ttu-id="91dbd-181">컴퓨터에 HPC 팩 클라이언트 유틸리티를 설치하려면 Microsoft 다운로드 센터에서 HPC 팩 2016 설치 파일(전체 설치)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span></span> <span data-ttu-id="91dbd-182">설치를 시작할 때 **HPC Pack 클라이언트 유틸리티**에 대한 설정 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="91dbd-183">클라이언트 컴퓨터를 준비하려면 클라이언트 컴퓨터에 대한 [HPC 클러스터 설정](hpcpack-2016-cluster.md) 중에 사용되는 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span></span> <span data-ttu-id="91dbd-184">표준 Windows 인증서 관리 절차를 사용하여 **인증서 – 현재 사용자** > **신뢰할 수 있는 루트 인증 기관** 저장소에 공용 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="91dbd-185">이제 Azure AD 계정을 사용하여 클러스터 작업을 제출하고 관리하도록 HPC 팩 명령을 실행하거나 HPC 팩 작업 관리자 GUI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span></span> <span data-ttu-id="91dbd-186">작업 제출 옵션은 [Azure에서 HPC 팩 클러스터에 HPC 작업 제출](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91dbd-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="91dbd-187">처음으로 Azure의 HPC 팩 클러스터에 연결하려는 경우 팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span></span> <span data-ttu-id="91dbd-188">Azure AD 자격 증명을 입력하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-188">Enter your Azure AD credentials to log in.</span></span> <span data-ttu-id="91dbd-189">그러면 토큰이 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-189">The token is then cached.</span></span> <span data-ttu-id="91dbd-190">인증이 변경되거나 캐시된 인증이 지워지지 않으면 이후 Azure의 클러스터에 대한 연결은 캐시된 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span></span>
>
  
<span data-ttu-id="91dbd-191">예를 들어 이전 단계를 완료한 후에 온-프레미스 클라이언트에서 작업을 다음과 같이 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="91dbd-192">Azure AD 통합을 사용하는 작업 제출에 유용한 cmdlet</span><span class="sxs-lookup"><span data-stu-id="91dbd-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-the-local-token-cache"></a><span data-ttu-id="91dbd-193">로컬 토큰 캐시 관리</span><span class="sxs-lookup"><span data-stu-id="91dbd-193">Manage the local token cache</span></span>

<span data-ttu-id="91dbd-194">HPC 팩 2016은 두 개의 새로운 HPC PowerShell cmdlet을 제공하여 로컬 토큰 캐시를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span></span> <span data-ttu-id="91dbd-195">이러한 cmdlet은 비대화형으로 작업을 제출하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="91dbd-196">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91dbd-196">See the following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-the-credentials-for-submitting-jobs-using-the-azure-ad-account"></a><span data-ttu-id="91dbd-197">Azure AD 계정을 사용하여 작업을 제출하는 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="91dbd-197">Set the credentials for submitting jobs using the Azure AD account</span></span> 

<span data-ttu-id="91dbd-198">때때로 HPC 클러스터 사용자(도메인에 가입된 HPC 클러스터의 경우 도메인 사용자로 실행, 도메인에 가입되지 않은 HPC 클러스터의 경우 헤드 노드에서 로컬 사용자로 실행) 실행하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span></span>

1. <span data-ttu-id="91dbd-199">다음 명령을 실행하여 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-199">Use the following commands to set the credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="91dbd-200">그리고 다음과 같이 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-200">Then submit the job as follows.</span></span> <span data-ttu-id="91dbd-201">작업/태스크는 계산 노드의 $localUser 아래에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-201">The job/task runs under $localUser on the compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="91dbd-202">`–Credential`이 `Submit-HpcJob`으로 지정되지 않으면 작업 또는 태스크는 Azure AD 계정으로 로컬 매핑된 사용자에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span></span> <span data-ttu-id="91dbd-203">HPC 클러스터는 태스크를 실행하는 Azure AD 계정과 동일한 이름을 가진 로컬 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span></span>
    
3. <span data-ttu-id="91dbd-204">Azure AD 계정에 대해 확장된 데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-204">Set extended data for the Azure AD account.</span></span> <span data-ttu-id="91dbd-205">Azure AD 계정을 사용하여 Linux 노드에서 MPI 작업을 실행하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span></span>

   * <span data-ttu-id="91dbd-206">Azure AD 계정 자체에 대해 확장된 데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-206">Set extended data for the Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="91dbd-207">확장된 데이터를 설정하고 HPC 클러스터 사용자로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91dbd-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

