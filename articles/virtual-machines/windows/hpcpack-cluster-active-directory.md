---
title: "Azure Active Directory와 클러스터 aaaHPC 팩 | Microsoft Docs"
description: "Azure Active Directory와 Azure에서 HPC 팩 2016 toointegrate 클러스터링 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="ca38a-103">Azure Active Directory를 사용하여 Azure에서 HPC 팩 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="ca38a-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="ca38a-104">[Microsoft HPC 팩 2016](https://technet.microsoft.com/library/cc514029)은 Azure에서 HPC 팩 클러스터를 배포하는 관리자에 대해 Azure AD([Azure Active Directory](../../active-directory/index.md))와의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="ca38a-105">상위 수준의 작업을 수행 하는 hello에 대 한이 문서의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="ca38a-106">수동으로 HPC 팩 클러스터를 Azure AD 테넌트와 통합</span><span class="sxs-lookup"><span data-stu-id="ca38a-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="ca38a-107">Azure의 HPC 팩 클러스터에서 작업 관리 및 예약</span><span class="sxs-lookup"><span data-stu-id="ca38a-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="ca38a-108">HPC Pack 클러스터 솔루션을 Azure AD와 통합 다른 응용 프로그램과 서비스 toointegrate 표준 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="ca38a-109">이 문서에서는 Azure AD의 기본 사용자 관리에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="ca38a-110">자세한 내용 및 배경 참조 hello [Azure Active Directory 설명서](../../active-directory/index.md) hello 섹션에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="ca38a-111">통합의 이점</span><span class="sxs-lookup"><span data-stu-id="ca38a-111">Benefits of integration</span></span>


<span data-ttu-id="ca38a-112">Azure Active Directory (Azure AD)는 다중 테 넌 트 클라우드 기반 디렉터리 및 id 관리 하는 서비스 toocloud 솔루션 single sign-on (SSO) 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="ca38a-113">HPC Pack 클러스터를 Azure AD와의 통합 hello는 다음과 같은 목표가 달성 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="ca38a-114">Active Directory 도메인 컨트롤러를 기존의 hello hello HPC Pack 클러스터에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="ca38a-115">이 비즈니스 및 속도 높이고 hello 배포 프로세스에 대 한 필요가 없는 경우에 hello 클러스터를 유지 관리의 hello 비용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="ca38a-116">다음 Azure AD에 의해 표시 되는 이점을 활용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="ca38a-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="ca38a-117">SSO(Single sign-on)</span><span class="sxs-lookup"><span data-stu-id="ca38a-117">Single sign-on</span></span> 
    *   <span data-ttu-id="ca38a-118">Azure의 hello HPC Pack 클러스터에 대 한 로컬 AD id를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ca38a-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Azure Active Directory 환경](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="ca38a-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ca38a-120">Prerequisites</span></span>
* <span data-ttu-id="ca38a-121">**Azure 가상 컴퓨터에 배포된 HPC 팩 2016 클러스터** - 단계는 [Azure에서 HPC 팩 2016 클러스터 배포](hpcpack-2016-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca38a-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="ca38a-122">Hello 헤드 노드의 hello DNS 이름 및 hello이이 문서의 단계를 완료 하려면 클러스터 관리자의 hello 자격 증명 필요.</span><span class="sxs-lookup"><span data-stu-id="ca38a-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ca38a-123">Azure Active Directory 통합은 HPC 팩 2016 이전에 HPC 팩의 버전에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="ca38a-124">**클라이언트 컴퓨터** -는 Windows 또는 Windows Server 클라이언트 컴퓨터 실행 너무 HPC Pack 클라이언트 유틸리티를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="ca38a-125">Toouse hello HPC Pack 웹 포털 또는 REST API toosubmit 작업을만 하려는 경우에 사용자가 선택한 모든 클라이언트 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="ca38a-126">**HPC Pack 클라이언트 유틸리티** -hello Microsoft 다운로드 센터에서에서 사용할 수 있는 hello 무료 설치 패키지를 사용 하 여 hello 클라이언트 컴퓨터에 hello HPC Pack 클라이언트 유틸리티를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="ca38a-127">1 단계: Azure AD 테 넌 트와 hello HPC 클러스터 서버 등록</span><span class="sxs-lookup"><span data-stu-id="ca38a-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="ca38a-128">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ca38a-129">클릭 **Active Directory** 왼쪽된 메뉴 hello와 구독에서 hello 원하는 디렉터리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="ca38a-130">사용 권한 tooaccess 리소스 hello 디렉터리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="ca38a-131">**사용자**를 클릭하고 사용자 계정이 이미 만든 또는 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="ca38a-132">**응용 프로그램** > **추가**를 클릭하고 **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="ca38a-133">Hello 정보 hello 마법사에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="ca38a-134">**이름** - HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="ca38a-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="ca38a-135">**유형**: **웹 응용 프로그램 및/또는 Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="ca38a-136">**로그온 URL**-hello는 기본적으로 hello 샘플에 대 한 기본 URL`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="ca38a-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="ca38a-137">**앱 ID URI** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="ca38a-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="ca38a-138">대체 `<Directory_name`> Azure AD 테 넌 트 예를 들어, 전체 이름 hello로 `hpclocal.onmicrosoft.com`, 대체 `<application_name>` 이전에 선택한 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="ca38a-139">Hello 앱을 추가한 후 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="ca38a-140">Hello 다음과 같은 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="ca38a-141">**응용 프로그램은 다중 테넌트**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="ca38a-142">선택 **예** 에 대 한 **사용자 할당 필요 tooaccess 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="ca38a-143">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-143">Click **Save**.</span></span> <span data-ttu-id="ca38a-144">저장이 완료되면 **매니페스트 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="ca38a-145">이 작업은 응용 프로그램의 매니페스트 JavaScript 개체 표기법(JSON) 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="ca38a-146">Hello를 배치 하 여 다운로드 한 hello 매니페스트 편집 `appRoles` 설정 하 고 추가한 응용 프로그램 역할을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="ca38a-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
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
7. <span data-ttu-id="ca38a-147">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-147">Save hello file.</span></span> <span data-ttu-id="ca38a-148">Hello 포털에서 클릭 **매니페스트 관리** > **매니페스트 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="ca38a-149">그런 다음 hello 편집 된 매니페스트를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="ca38a-150">**사용자**를 클릭하고 사용자를 선택한 다음 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="ca38a-151">Hello 사용 가능한 역할 (HpcUsers 또는 HpcAdminMirror) toohello 사용자 중 하나를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="ca38a-152">Hello 디렉터리에 추가 사용자와이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="ca38a-153">클러스터 사용자에 대한 배경 정보는 [클러스터 사용자 관리](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca38a-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="ca38a-154">toomanage 사용자가 사용할 수 있는 권장 hello Azure Active Directory 미리 보기 블레이드에서 hello에 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="ca38a-155">2 단계: Azure AD 테 넌 트와 hello HPC 클러스터 클라이언트 등록</span><span class="sxs-lookup"><span data-stu-id="ca38a-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="ca38a-156">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ca38a-157">클릭 **Active Directory** 왼쪽된 메뉴 hello와 구독에서 hello 원하는 디렉터리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="ca38a-158">사용 권한 tooaccess 리소스 hello 디렉터리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="ca38a-159">**응용 프로그램** > **추가**를 클릭하고 **내 조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="ca38a-160">Hello 정보 hello 마법사에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="ca38a-161">**이름** - HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="ca38a-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="ca38a-162">**형식** - **네이티브 클라이언트 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="ca38a-163">**URI 리디렉션** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="ca38a-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="ca38a-164">Hello 앱을 추가한 후 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="ca38a-165">복사 hello **클라이언트 ID** 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="ca38a-166">나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="ca38a-167">**tooother 응용 프로그램 사용 권한**, 클릭 **응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="ca38a-168">검색 하 고 hello HpcPackClusterServer 응용 프로그램 (1 단계에서에서 만든)을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="ca38a-169">Hello에 **위임 된 권한** 드롭다운 **액세스 HpcClusterServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="ca38a-170">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="ca38a-171">3 단계: hello HPC 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="ca38a-172">Azure에서 헤드 노드에 HPC 팩 2016 toohello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="ca38a-173">HPC PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="ca38a-174">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="ca38a-175">여기서,</span><span class="sxs-lookup"><span data-stu-id="ca38a-175">where</span></span>

    * <span data-ttu-id="ca38a-176">`AADTenant`같은 hello Azure AD 테 넌 트 이름 지정`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="ca38a-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="ca38a-177">`AADClientAppId`2 단계에서에서 만든 hello 앱에 대 한 hello 클라이언트 ID를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="ca38a-178">Hello HpcSchedulerStateful 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="ca38a-179">여러 헤드 노드를 클러스터에서 PowerShell 명령을 hello 헤드 노드 tooswitch hello 주 복제본에서 hello HpcSchedulerStateful 서비스에 대 한 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="ca38a-180">4 단계: 관리 하 고 hello 클라이언트에서 작업 제출</span><span class="sxs-lookup"><span data-stu-id="ca38a-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="ca38a-181">컴퓨터에 tooinstall hello HPC Pack 클라이언트 유틸리티 hello Microsoft 다운로드 센터에서에서 HPC 팩 2016 설치 파일 (전체 설치)를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="ca38a-182">Hello 설치를 시작할 때 hello에 대 한 hello 설치 옵션을 선택 합니다. **HPC Pack 클라이언트 유틸리티**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="ca38a-183">tooprepare hello 클라이언트 컴퓨터 설치 중에 사용 하는 hello 인증서 [HPC 클러스터 설정](hpcpack-2016-cluster.md) hello 클라이언트 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="ca38a-184">표준 Windows를 사용 하 여 인증서 관리 프로시저 tooinstall hello 공용 인증서 toohello **인증서 – 현재 사용자** > **신뢰할 수 있는 루트 인증 기관** 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="ca38a-185">이제 hello HPC Pack 명령을 실행 하거나 toosubmit hello HPC 팩 작업 관리자 GUI 사용 하 여 있고 hello Azure AD 계정을 사용 하 여 클러스터 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="ca38a-186">작업 전송 옵션을 참조 하십시오. [Azure에서 HPC 제출 작업 tooan HPC 팩 클러스터](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="ca38a-187">Hello에 대 한 tooconnect toohello HPC Pack 클러스터에서 Azure 처음으로 시도 하면 팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="ca38a-188">에 Azure AD 자격 증명 toolog에를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="ca38a-189">hello 토큰이 다음 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-189">hello token is then cached.</span></span> <span data-ttu-id="ca38a-190">이후 연결 toohello 클러스터 hello Azure 사용에에서 인증 변경 또는 hello 캐시의 선택을 취소 하면 않는 경우 토큰을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="ca38a-191">예를 들어 hello 이전 단계를 완료 한 후 쿼리할 수 있습니다는 온-프레미스 클라이언트에서 작업에 대 한 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="ca38a-192">Azure AD 통합을 사용하는 작업 제출에 유용한 cmdlet</span><span class="sxs-lookup"><span data-stu-id="ca38a-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="ca38a-193">Hello 로컬 토큰 캐시를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-193">Manage hello local token cache</span></span>

<span data-ttu-id="ca38a-194">HPC 팩 2016 두 개의 새로운 HPC PowerShell cmdlet toomanage hello 로컬 토큰 캐시를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="ca38a-195">이러한 cmdlet은 비대화형으로 작업을 제출하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="ca38a-196">다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ca38a-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="ca38a-197">Hello Azure AD 계정을 사용 하 여 작업을 제출 하기 위한 hello 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="ca38a-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="ca38a-198">따라, (도메인에 가입 된 HPC 클러스터의 경우 한 도메인 사용자 계정으로 실행, 도메인 가입 된 HPC 클러스터의 경우 hello 헤드 노드에 대 한 로컬 사용자로 실행) hello HPC 클러스터 사용자 toorun hello 작업을 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="ca38a-199">사용 하 여 hello 다음 명령 tooset hello 자격 증명:</span><span class="sxs-lookup"><span data-stu-id="ca38a-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="ca38a-200">그런 다음 다음과 같이 hello 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-200">Then submit hello job as follows.</span></span> <span data-ttu-id="ca38a-201">hello 계산 노드에서 hello 작업/태스크 실행 $localUser 아래에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="ca38a-202">경우 `–Credential` 으로 지정 하지 않으면 `Submit-HpcJob`, Azure AD 계정을 hello 처럼 hello 작업 또는 작업 로컬 매핑된 사용자 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="ca38a-203">(hello HPC 클러스터는 로컬 사용자를 만듭니다 hello Azure AD 계정 toorun hello 작업 이름이 hello.)</span><span class="sxs-lookup"><span data-stu-id="ca38a-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="ca38a-204">Azure AD 계정 hello에 대 한 확장된 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="ca38a-205">Hello Azure AD 계정을 사용 하 여 Linux 노드에서 MPI 작업을 실행 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="ca38a-206">Azure AD 계정 자체 hello에 대 한 확장된 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="ca38a-207">확장된 데이터를 설정하고 HPC 클러스터 사용자로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ca38a-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

