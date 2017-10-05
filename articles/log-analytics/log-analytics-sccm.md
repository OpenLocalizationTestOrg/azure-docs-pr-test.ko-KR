---
title: "Log Analytics에 구성 관리자 연결 | Microsoft Docs"
description: "이 문서는 구성 관리자를 Log Analytics에 연결하고 데이터 분석을 시작하는 단계를 보여줍니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: 62d31ed486458245156f7fc832294d662c62991e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-configuration-manager-to-log-analytics"></a><span data-ttu-id="04d5d-103">Log Analytics에 구성 관리자 연결</span><span class="sxs-lookup"><span data-stu-id="04d5d-103">Connect Configuration Manager to Log Analytics</span></span>
<span data-ttu-id="04d5d-104">System Center Configuration Manager를 OMS의 Log Analytics에 연결하여 장치 수집 데이터를 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-104">You can connect System Center Configuration Manager to Log Analytics in OMS to sync device collection data.</span></span> <span data-ttu-id="04d5d-105">이 경우 OMS에서 구성 관리자 계층 구조의 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-105">This makes data from your Configuration Manager hierarchy available in OMS.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04d5d-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="04d5d-106">Prerequisites</span></span>

<span data-ttu-id="04d5d-107">Log Analytics는 System Center Configuration Manager 현재 분기, 1606 이상 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-107">Log Analytics supports System Center Configuration Manager current branch, version 1606 and higher.</span></span>  

## <a name="configuration-overview"></a><span data-ttu-id="04d5d-108">구성 개요</span><span class="sxs-lookup"><span data-stu-id="04d5d-108">Configuration overview</span></span>
<span data-ttu-id="04d5d-109">다음 단계는 구성 관리자를 Log Analytics에 연결하는 과정을 요약하여 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-109">The following steps summarizes the process to connect Configuration Manager to Log Analytics.</span></span>  

1. <span data-ttu-id="04d5d-110">Azure Management Portal에서 구성 관리자를 웹 응용 프로그램 및/또는 Web API 앱으로 등록하고 Azure Active Directory에서 등록할 때 사용한 클라이언트 ID와 클라이언트 비밀 키가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-110">In the Azure Management Portal, register Configuration Manager as a Web Application and/or Web API app, and ensure that you have the client ID and client secret key from the registration from Azure Active Directory.</span></span> <span data-ttu-id="04d5d-111">이 단계를 수행하는 방법은 [포털을 사용하여 리소스에 액세스할 수 있는 Active Directory 응용 프로그램 및 서비스 주체 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04d5d-111">See [Use portal to create Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md) for detailed information about how accomplish this step.</span></span>
2. <span data-ttu-id="04d5d-112">Azure Management Portal에서 [구성 관리자(등록된 웹앱)에 OMS에 대한 액세스 권한을 제공](#provide-configuration-manager-with-permissions-to-oms)합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-112">In the Azure Management Portal, [provide Configuration Manager (the registered web app) with permission to access OMS](#provide-configuration-manager-with-permissions-to-oms).</span></span>
3. <span data-ttu-id="04d5d-113">구성 관리자에서 [DMS 연결 추가 마법사를 사용하여 연결을 추가](#add-an-oms-connection-to-configuration-manager)합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-113">In Configuration Manager, [add a connection using the Add OMS Connection Wizard](#add-an-oms-connection-to-configuration-manager).</span></span>
4. <span data-ttu-id="04d5d-114">구성 관리자에서 암호 또는 클라이언트 비밀 키가 만료되거나 분실된 경우 [연결 속성을 업데이트](#update-oms-connection-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-114">In Configuration Manager, [update the connection properties](#update-oms-connection-properties) if the password or client secret key ever expires or is lost.</span></span>
5. <span data-ttu-id="04d5d-115">OMS 포털의 정보를 사용하여 구성 관리자 서비스 연결 지점 사이트 시스템 역할을 실행하는 컴퓨터에서 [Microsoft Monitoring Agent를 다운로드 및 설치](#download-and-install-the-agent)합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-115">With information from the OMS portal, [download and install the Microsoft Monitoring Agent](#download-and-install-the-agent) on the computer running the Configuration Manager service connection point site system role.</span></span> <span data-ttu-id="04d5d-116">에이전트가 구성 관리자 데이터를 OMS로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-116">The agent sends Configuration Manager data to OMS.</span></span>
6. <span data-ttu-id="04d5d-117">Log Analytics에서 컴퓨터 그룹으로 [구성 관리자의 컬렉션을 가져옵니다](#import-collections).</span><span class="sxs-lookup"><span data-stu-id="04d5d-117">In Log Analytics, [import collections from Configuration Manager](#import-collections) as computer groups.</span></span>
7. <span data-ttu-id="04d5d-118">Log Analytics에서 [컴퓨터 그룹](log-analytics-computer-groups.md)으로 구성 관리자에서 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-118">In Log Analytics, view data from Configuration Manager as [computer groups](log-analytics-computer-groups.md).</span></span>

<span data-ttu-id="04d5d-119">[Microsoft Operations Management Suite에 구성 관리자의 데이터 동기화](https://technet.microsoft.com/library/mt757374.aspx)에서 구성 관리자를 OMS에 연결하는 방법에 대해 자세히 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-119">You can read more about connecting Configuration Manager to OMS at [Sync data from Configuration Manager to the Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).</span></span>

## <a name="provide-configuration-manager-with-permissions-to-oms"></a><span data-ttu-id="04d5d-120">구성 관리자에 OMS에 대한 사용 권한 제공</span><span class="sxs-lookup"><span data-stu-id="04d5d-120">Provide Configuration Manager with permissions to OMS</span></span>
<span data-ttu-id="04d5d-121">다음 절차에서는 Azure Management Portal에 OMS에 대한 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-121">The following procedure provides the Azure Management Portal with permissions to access OMS.</span></span> <span data-ttu-id="04d5d-122">특히, Azure 관리 포털에서 구성 관리자를 OMS에 연결할 수 있도록 하기 위해 리소스 그룹의 사용자에게 *참가자 역할*을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-122">Specifically, you must grant the *Contributor role* to users in the resource group in order to allow the Azure Management Portal to connect Configuration Manager to OMS.</span></span>

> [!NOTE]
> <span data-ttu-id="04d5d-123">구성 관리자의 OMS에 사용 권한을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-123">You must specify permissions in OMS for Configuration Manager.</span></span> <span data-ttu-id="04d5d-124">그렇지 않고 구성 관리자에세 구성 마법사를 사용하면 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-124">Otherwise, you'll receive an error message when you use the configuration wizard in Configuration Manager.</span></span>
>
>

1. <span data-ttu-id="04d5d-125">[Azure Portal](https://portal.azure.com/)을 열고 **찾아보기** > **Log Analytics(OMS)**를 클릭하여 Log Analytics(OMS) 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-125">Open the [Azure portal](https://portal.azure.com/) and click **Browse** > **Log Analytics (OMS)** to open the Log Analytics (OMS) blade.</span></span>  
2. <span data-ttu-id="04d5d-126">**Log Analytics(OMS)** 블레이드에서 **추가**를 클릭해 **OMS 작업 영역** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-126">On the **Log Analytics (OMS)** blade, click **Add** to open the **OMS Workspace** blade.</span></span>  
   <span data-ttu-id="04d5d-127">![OMS 블레이드](./media/log-analytics-sccm/sccm-azure01.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-127">![OMS blade](./media/log-analytics-sccm/sccm-azure01.png)</span></span>
3. <span data-ttu-id="04d5d-128">**OMS 작업 영역** 블레이드에서 다음 정보를 제공한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-128">On the **OMS Workspace** blade, provide the following information and then click **OK**.</span></span>

   * <span data-ttu-id="04d5d-129">**OMS 작업 영역**</span><span class="sxs-lookup"><span data-stu-id="04d5d-129">**OMS Workspace**</span></span>
   * <span data-ttu-id="04d5d-130">**구독**</span><span class="sxs-lookup"><span data-stu-id="04d5d-130">**Subscription**</span></span>
   * <span data-ttu-id="04d5d-131">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="04d5d-131">**Resource group**</span></span>
   * <span data-ttu-id="04d5d-132">**위치**:</span><span class="sxs-lookup"><span data-stu-id="04d5d-132">**Location**</span></span>
   * <span data-ttu-id="04d5d-133">**가격 책정 계층**</span><span class="sxs-lookup"><span data-stu-id="04d5d-133">**Pricing tier**</span></span>  
     <span data-ttu-id="04d5d-134">![OMS 블레이드](./media/log-analytics-sccm/sccm-azure02.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-134">![OMS blade](./media/log-analytics-sccm/sccm-azure02.png)</span></span>  

     > [!NOTE]
     > <span data-ttu-id="04d5d-135">위의 예제는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-135">The example above creates a new resource group.</span></span> <span data-ttu-id="04d5d-136">리소스 그룹은 구성 관리자에 이 예제의 OMS 작업 영역에 대한 권한을 제공하는 데에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-136">The resource group is only used to provide Configuration Manager with permissions to the OMS workspace in this example.</span></span>
     >
     >
4. <span data-ttu-id="04d5d-137">**찾아보기** > **리소스 그룹**을 클릭하여 **리소스 그룹** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-137">Click **Browse** > **Resource groups** to open the **Resource groups** blade.</span></span>
5. <span data-ttu-id="04d5d-138">**리소스 그룹** 블레이드에서 위에서 만든 리소스 그룹을 클릭하여 &lt;리소스 그룹 이름&gt; 설정 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-138">In the **Resource groups** blade, click the resource group that you created above to open the &lt;resource group name&gt; settings blade.</span></span>  
   <span data-ttu-id="04d5d-139">![리소스 그룹 설정 블레이드](./media/log-analytics-sccm/sccm-azure03.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-139">![resource group settings blade](./media/log-analytics-sccm/sccm-azure03.png)</span></span>
6. <span data-ttu-id="04d5d-140">&lt;리소스 그룹&gt; 이름 설정 블레이드에서 Access Control(IAM)을 클릭하여 &lt;리소스 그룹 이름&gt; 사용자 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-140">In the &lt;resource group name&gt; settings blade, click Access control (IAM) to open the &lt;resource group name&gt; Users blade.</span></span>  
   ![리소스 그룹 사용자 블레이드](./media/log-analytics-sccm/sccm-azure04.png)  
7. <span data-ttu-id="04d5d-142">&lt;리소스 그룹 이름&gt; 사용자 블레이드에서 **추가**를 클릭하여 **액세스 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-142">In the &lt;resource group name&gt; Users blade, click **Add** to open the **Add access** blade.</span></span>
8. <span data-ttu-id="04d5d-143">**액세스 추가** 블레이드에서 **역할 선택**을 클릭한 다음 **참가자** 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-143">In the **Add access** blade, click **Select a role**, and then select the **Contributor** role.</span></span>  
   <span data-ttu-id="04d5d-144">![역할 선택](./media/log-analytics-sccm/sccm-azure05.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-144">![select a role](./media/log-analytics-sccm/sccm-azure05.png)</span></span>  
9. <span data-ttu-id="04d5d-145">**사용자 추가**를 클릭하고 구성 관리자 사용자를 선택한 다음 **선택**을 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-145">Click **Add users**, select the Configuration Manager user, click **Select**, and then click **OK**.</span></span>  
   <span data-ttu-id="04d5d-146">![사용자 추가](./media/log-analytics-sccm/sccm-azure06.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-146">![add users](./media/log-analytics-sccm/sccm-azure06.png)</span></span>  

## <a name="add-an-oms-connection-to-configuration-manager"></a><span data-ttu-id="04d5d-147">구성 관리자에 OMS 연결 추가</span><span class="sxs-lookup"><span data-stu-id="04d5d-147">Add an OMS connection to Configuration Manager</span></span>
<span data-ttu-id="04d5d-148">OMS 연결을 추가하려면 구성 관리자 환경에 온라인 모드를 위해 구성된 [서비스 연결 지점](https://technet.microsoft.com/library/mt627781.aspx)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-148">In order to add an OMS connection, your Configuration Manager environment must have a [service connection point](https://technet.microsoft.com/library/mt627781.aspx) configured for online mode.</span></span>

1. <span data-ttu-id="04d5d-149">구성 관리자의 **관리** 작업 영역에서 **OMS 커넥터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-149">In the **Administration** workspace of Configuration Manager, select **OMS Connector**.</span></span> <span data-ttu-id="04d5d-150">그러면 **OMS 연결 추가 마법사**가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-150">This opens the **Add OMS Connection Wizard**.</span></span> <span data-ttu-id="04d5d-151">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-151">Select **Next**.</span></span>
2. <span data-ttu-id="04d5d-152">**일반** 화면에서 아래의 작업을 완료했는지와 각 항목에 대한 상세 정보가 있는지 확인하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-152">On the **General** screen, confirm that you have done the following actions and that you have details for each item, then select **Next**.</span></span>

   1. <span data-ttu-id="04d5d-153">Azure Management Portal에서 구성 관리자를 웹 응용 프로그램 및/또는 웹 API 앱으로 등록했는지 여부 및 [등록 시 지정한 클라이언트 ID](../active-directory/active-directory-integrating-applications.md)가 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="04d5d-153">In the Azure Management Portal, you've registered Configuration Manager as a Web Application and/or Web API app, and that you have the [client ID from the registration](../active-directory/active-directory-integrating-applications.md).</span></span>
   2. <span data-ttu-id="04d5d-154">Azure Management Portal에서 Azure Active Directory에 등록된 앱의 앱 비밀 키를 만들었는지 여부</span><span class="sxs-lookup"><span data-stu-id="04d5d-154">In the Azure Management Portal, you've created an app secret key for the registered app in Azure Active Directory.</span></span>  
   3. <span data-ttu-id="04d5d-155">Azure Management Portal에서 등록된 웹앱에 OMS에 대한 액세스 권한을 제공했는지 여부</span><span class="sxs-lookup"><span data-stu-id="04d5d-155">In the Azure Management Portal, you've provided the registered web app with permission to access OMS.</span></span>  
      ![OMS 마법사 일반 페이지 연결](./media/log-analytics-sccm/sccm-console-general01.png)
3. <span data-ttu-id="04d5d-157">**Azure Active Directory** 화면에서 **테넌트** , **클라이언트 ID** , **클라이언트 비밀 키**를 지정하여 OMS에 대한 연결 설정을 구성하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-157">On the **Azure Active Directory** screen, configure your connection settings to OMS by providing your **Tenant** , **Client ID** , and **Client Secret Key** , then select **Next**.</span></span>  
   <span data-ttu-id="04d5d-158">![OMS Wizard Azure Active Directory 페이지에 연결](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-158">![Connection to OMS Wizard Azure Active Directory page](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)</span></span>
4. <span data-ttu-id="04d5d-159">나머지 절차를 성공적으로 완료한 경우 이 페이지에 **OMS 연결 구성** 화면이 자동으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-159">If you accomplished all the other procedures successfully, then the information on the **OMS Connection Configuration** screen will automatically appear on this page.</span></span> <span data-ttu-id="04d5d-160">**Azure 구독**, **Azure 리소스 그룹**, **Operations Management Suite 작업 영역**에 대한 연결 설정 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-160">Information for the connection settings should appear for your **Azure subscription** , **Azure resource group** , and **Operations Management Suite Workspace**.</span></span>  
   <span data-ttu-id="04d5d-161">![OMS 연결 마법사의 OMS 연결 페이지](./media/log-analytics-sccm/sccm-wizard-configure04.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-161">![Connection to OMS Wizard OMS Connection page](./media/log-analytics-sccm/sccm-wizard-configure04.png)</span></span>
5. <span data-ttu-id="04d5d-162">이 마법사는 사용자가 입력한 정보를 사용하여 OMS 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-162">The wizard connects to the OMS service using the information you've input.</span></span> <span data-ttu-id="04d5d-163">OMS와 동기화하려는 장치 컬렉션을 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-163">Select the device collections that you want to sync with OMS and then click **Add**.</span></span>  
   <span data-ttu-id="04d5d-164">![컬렉션 선택](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-164">![Select Collections](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)</span></span>
6. <span data-ttu-id="04d5d-165">**요약** 화면에서 연결 설정을 확인하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-165">Verify your connection settings on the **Summary** screen, then select **Next**.</span></span> <span data-ttu-id="04d5d-166">**진행률** 화면에 연결 상태와 **완료**가 차례로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-166">The **Progress** screen shows the connection status, then should **Complete**.</span></span>

> [!NOTE]
> <span data-ttu-id="04d5d-167">OMS를 계층의 최고 계층 사이트에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-167">You must connect OMS to the top-tier site in your hierarchy.</span></span> <span data-ttu-id="04d5d-168">OMS를 독립형 기본 사이트에 연결한 다음 환경에 중앙 관리 사이트를 추가할 경우 새 계층 안에서 OMS 연결을 삭제하고 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-168">If you connect OMS to a standalone primary site and then add a central administration site to your environment, you'll have to delete and recreate the OMS connection within the new hierarchy.</span></span>
>
>

<span data-ttu-id="04d5d-169">OMS에 구성 관리자를 연결한 후에는 컬렉션을 추가 또는 제거하고 OMS 연결의 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-169">After you have linked Configuration Manager to OMS, you can add or remove collections, and view the properties of the OMS connection.</span></span>

## <a name="update-oms-connection-properties"></a><span data-ttu-id="04d5d-170">OMS 연결 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="04d5d-170">Update OMS connection properties</span></span>
<span data-ttu-id="04d5d-171">암호 또는 클라이언트 비밀 키가 만료되거나 분실된 경우 OMS 연결 속성을 수동으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-171">If a password or client secret key ever expires or is lost, you'll need to manually update the OMS connection properties.</span></span>

1. <span data-ttu-id="04d5d-172">**구성 관리자**에서 Cloud Services로 이동한 다음 **OMS 커넥터**를 선택하여 **OMS 연결 속성** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-172">In Configuration Manager, navigate to **Cloud Services** , then select **OMS Connector** to open the **OMS Connection Properties** page.</span></span>
2. <span data-ttu-id="04d5d-173">이 페이지에서 **Azure Active Directory** 탭을 클릭하여 **테넌트**, **클라이언트 ID**, **클라이언트 비밀 키 만료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-173">On this page, click the **Azure Active Directory** tab to view your **Tenant**, **Client ID**, **Client secret key expiration**.</span></span> <span data-ttu-id="04d5d-174">**클라이언트 비밀 키**가 만료되었는지 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-174">**Verify** your **Client secret key** if it has expired.</span></span>

## <a name="download-and-install-the-agent"></a><span data-ttu-id="04d5d-175">에이전트 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="04d5d-175">Download and install the agent</span></span>
1. <span data-ttu-id="04d5d-176">OMS 포털에서 [OMS 에이전트 설치 파일을 다운로드](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms)합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-176">In the OMS portal, [Download the agent setup file from OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).</span></span>
2. <span data-ttu-id="04d5d-177">다음 중 한 가지 방법을 사용하여 구성 관리자 서비스 연결 지점 사이트 시스템 역할을 실행하는 컴퓨터에 에이전트를 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-177">Use one of the following methods to install and configure the agent on the computer running the Configuration Manager service connection point site system role:</span></span>
   * [<span data-ttu-id="04d5d-178">설치를 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="04d5d-178">Install the agent using setup</span></span>](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [<span data-ttu-id="04d5d-179">명령줄을 사용하여 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="04d5d-179">Install the agent using the command line</span></span>](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [<span data-ttu-id="04d5d-180">Azure Automation에서 DSC를 사용하여 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="04d5d-180">Install the agent using DSC in Azure Automation</span></span>](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a><span data-ttu-id="04d5d-181">컬렉션 가져오기</span><span class="sxs-lookup"><span data-stu-id="04d5d-181">Import collections</span></span>
<span data-ttu-id="04d5d-182">구성 관리자에 OMS 연결을 추가하고 구성 관리자 서비스 연결 지점 사이트 시스템 역할을 실행하는 컴퓨터에 에이전트를 설치한 후 다음 단계는 컴퓨터 그룹으로 OMS의 구성 관리자 컬렉션을 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-182">After you've added an OMS connection to Configuration Manager and installed the agent on the computer running the Configuration Manager service connection point site system role, the next step is to import collections from Configuration Manager in OMS as computer groups.</span></span>

<span data-ttu-id="04d5d-183">가져오기를 사용하도록 설정하면 3시간마다 컬렉션 멤버 자격 정보가 검색되어 컬렉션 멤버 자격을 최신 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-183">After importation is enabled, the collection membership information is retrieved every 3 hours to keep the collection memberships current.</span></span> <span data-ttu-id="04d5d-184">언제든지 가져오기를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-184">You can choose to disable importation at any time.</span></span>

1. <span data-ttu-id="04d5d-185">OMS 포털에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-185">In the OMS portal, click **Settings**.</span></span>
2. <span data-ttu-id="04d5d-186">**컴퓨터 그룹** 탭을 클릭한 다음 **SCCM** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-186">Click the **Computer Groups** tab and then click the **SCCM** tab.</span></span>
3. <span data-ttu-id="04d5d-187">**구성 관리자 컬렉션 멤버 자격 가져오기**를 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-187">Select **Import Configuration Manager collection memberships** and then click **Save**.</span></span>  
   <span data-ttu-id="04d5d-188">![컴퓨터 그룹 - SCCM 탭](./media/log-analytics-sccm/sccm-computer-groups01.png)</span><span class="sxs-lookup"><span data-stu-id="04d5d-188">![Computer Groups - SCCM tab](./media/log-analytics-sccm/sccm-computer-groups01.png)</span></span>

## <a name="view-data-from-configuration-manager"></a><span data-ttu-id="04d5d-189">구성 관리자의 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="04d5d-189">View data from Configuration Manager</span></span>
<span data-ttu-id="04d5d-190">구성 관리자에 OMS 연결을 추가하고 구성 관리자 서비스 연결 지점 사이트 시스템 역할을 실행하는 컴퓨터에 에이전트를 설치하면 에이전트의 데이터가 OMS로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-190">After you've added an OMS connection to Configuration Manager and installed the agent on the computer running the Configuration Manager service connection point site system role, data from the agent is sent to OMS.</span></span> <span data-ttu-id="04d5d-191">OMS에서 구성 관리자 컬렉션이 [컴퓨터 그룹](log-analytics-computer-groups.md)으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-191">In OMS, your Configuration Manager collections appear as [computer groups](log-analytics-computer-groups.md).</span></span> <span data-ttu-id="04d5d-192">**설정**의 **컴퓨터 그룹**에서 **구성 관리자** 페이지의 그룹을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-192">You can view the groups from the **Configuration Manager** page under **Computer Groups** in **Settings**.</span></span>

<span data-ttu-id="04d5d-193">컬렉션을 가져오면 컬렉션 멤버 자격이 있는 컴퓨터 중 삭제된 컴퓨터 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-193">After the collections are imported, you can see how many computers with collection memberships have been detected.</span></span> <span data-ttu-id="04d5d-194">또한 가져온 컬렉션 수도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-194">You can also see the number of collections that have been imported.</span></span>

![컴퓨터 그룹 - SCCM 탭](./media/log-analytics-sccm/sccm-computer-groups02.png)

<span data-ttu-id="04d5d-196">각 항목을 클릭하면 가져온 그룹 전체 또는 각 그룹에 속하는 전체 컴퓨터가 표시된 검색이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-196">When you click either one, Search opens, displaying either all of the imported groups or all computers that belong to each group.</span></span> <span data-ttu-id="04d5d-197">[로그 검색](log-analytics-log-searches.md)을 사용하여 구성 관리자 데이터의 자세한 분석을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-197">Using [Log Search](log-analytics-log-searches.md), you can start in-depth analysis of Configuration Manager data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04d5d-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04d5d-198">Next steps</span></span>
* <span data-ttu-id="04d5d-199">[로그 검색](log-analytics-log-searches.md)을 사용하여 구성 관리자 데이터에 대한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04d5d-199">Use [Log Search](log-analytics-log-searches.md) to view detailed information about your Configuration Manager data.</span></span>
