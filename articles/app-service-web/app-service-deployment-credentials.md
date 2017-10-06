---
title: "응용 프로그램 서비스에 대 한 배포 자격 증명 aaaAzure | Microsoft Docs"
description: "Toouse Azure 앱 서비스 배포 자격 증명을 hello 하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="7ccdc-103">Azure App Service의 배포 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="7ccdc-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="7ccdc-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)는 [로컬 Git 배포](app-service-deploy-local-git.md) 및 [FTP/S 배포](app-service-deploy-ftp.md)를 위해 두 가지 유형의 자격 증명을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="7ccdc-105">이러한 동일한 Azure Active Directory 자격 증명으로 hello 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="7ccdc-106">**사용자 수준 자격 증명**: 하나의 hello 전체 Azure 계정에 대 한 자격 증명 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="7ccdc-107">모든 응용 프로그램에서 Azure 계정 hello 하는 모든 구독에 권한 tooaccess에 사용 되는 toodeploy tooApp 서비스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="7ccdc-108">다음에 구성 하는 hello 기본 자격 증명 집합은 **응용 프로그램 서비스** > **&lt;app_name >** > **배포 자격 증명**.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="7ccdc-109">Hello 포털 GUI에에서 표시 되는 기본 집합 또한 hello는 이것 (hello 같은 **개요** 및 **속성** 응용 프로그램의 [리소스 블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="7ccdc-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ccdc-110">역할 기반 액세스 제어 (RBAC) 또는 공동 관리자 사용 권한을 통해 tooAzure 리소스에 액세스를 위임할 때는 액세스 tooan 응용 프로그램을 수신 하는 각 Azure 사용자 액세스가 취소 될 때까지 자신의 개인 사용자 수준 자격 증명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="7ccdc-111">이러한 배포 자격 증명은 다른 Azure 사용자와 공유하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="7ccdc-112">**앱 수준 자격 증명** - 각 앱마다 하나씩의 자격 증명 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="7ccdc-113">사용 되는 toodeploy toothat 앱의 배경에 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="7ccdc-114">각 응용 프로그램 응용 프로그램 작성 시 자동으로 생성 되 고 hello 앱에에 대 한 자격 증명 hello 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="7ccdc-115">Hello 자격 증명을 수동으로 구성할 수 없습니다 되지만 다시 설정할 수 있습니다 이러한 응용 프로그램에 대 한 언제 든 지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ccdc-116">Toothese 자격 증명을 통해 RBAC 역할 기반 액세스 제어 ()를 다른 사람이 액세스 순서 toogive, toomake 해야 해당 참가자 hello 웹 응용 프로그램에서 높은 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="7ccdc-117">판독기는 toopublish, 허용 되지 않으며 따라서 해당 자격 증명에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="7ccdc-118"><a name="userscope"></a>사용자 수준 자격 증명 설정 및 다시 설정</span><span class="sxs-lookup"><span data-stu-id="7ccdc-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="7ccdc-119">모든 앱의 [리소스 블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)에서 사용자 수준 자격 증명을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="7ccdc-120">이와 상관 없이 어떤 앱에서 이러한 자격 증명을 구성, tooall 앱을 적용 하 고 Azure의 모든 구독에 대 한 계정.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="7ccdc-121">tooconfigure 사용자 수준 자격 증명:</span><span class="sxs-lookup"><span data-stu-id="7ccdc-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="7ccdc-122">Hello에 [Azure 포털](https://portal.azure.com), 앱 서비스 >  **&lt;any_app >** > **배포 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ccdc-123">Hello 포털에서 자격 증명 블레이드를 배포 하는 hello에 액세스 하려면 먼저 앱 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="7ccdc-124">그러나 hello로 [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), 기존 응용 프로그램 없이 사용자 수준 자격 증명을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="7ccdc-125">Hello 사용자 이름 및 암호를 구성 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="7ccdc-126">배포 자격 증명을 설정한 후 hello를 찾을 수 있습니다 *Git* 응용 프로그램에 배포 사용자 이름이 **개요**,</span><span class="sxs-lookup"><span data-stu-id="7ccdc-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="7ccdc-127">그런 다음 앱의 **속성**에서 *FTP* 배포 사용자 이름을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="7ccdc-128">Azure에서는 사용자 수준 배포 암호가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="7ccdc-129">Hello 암호를 잊은 경우에 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="7ccdc-130">그러나 hello이이 섹션의에서 단계를 수행 하 여 자격 증명을 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="7ccdc-131"><a name="appscope"></a>앱 수준 자격 증명 정보 가져오기 및 다시 설정</span><span class="sxs-lookup"><span data-stu-id="7ccdc-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="7ccdc-132">앱 수준 자격 증명 hello에 저장 됩니다, 앱 서비스에서 각 앱에 대 한 게시 프로필 XML입니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="7ccdc-133">tooget hello 앱 수준 자격 증명:</span><span class="sxs-lookup"><span data-stu-id="7ccdc-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="7ccdc-134">Hello에 [Azure 포털](https://portal.azure.com), 앱 서비스 >  **&lt;any_app >** > **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="7ccdc-135">**...추가** > **게시 프로필 가져오기**를 차례로 클릭하고 .PublishSettings 파일 다운로드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="7ccdc-136">열기 번호입니다. PublishSettings 파일을 hello `<publishProfile>` hello 특성을 가진 태그가 `publishMethod="FTP"`합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="7ccdc-137">그런 다음 `userName` 및 `password` 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="7ccdc-138">이들은 hello 앱 수준 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="7ccdc-139">유사한 toohello 사용자 수준 자격 증명 hello FTP 배포 사용자 이름이 hello 형식의 `<app_name>\<username>`는 hello Git 배포 사용자 이름 및 `<username>` hello 이전 없이 `<app_name>\`합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="7ccdc-140">tooreset hello 앱 수준 자격 증명:</span><span class="sxs-lookup"><span data-stu-id="7ccdc-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="7ccdc-141">Hello에 [Azure 포털](https://portal.azure.com), 앱 서비스 >  **&lt;any_app >** > **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="7ccdc-142">**...추가** > **게시 프로필 다시 설정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="7ccdc-143">클릭 **예** tooconfirm hello를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="7ccdc-144">hello reset 작업 이전에 다운로드 한 모든 무효화 합니다. PublishSettings 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ccdc-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ccdc-145">Next steps</span></span>

<span data-ttu-id="7ccdc-146">방법을 알아보려면 toouse 이러한 자격 증명 toodeploy에서 응용 프로그램 [로컬 Git](app-service-deploy-local-git.md) 또는 사용 하 여 [FTP/S](app-service-deploy-ftp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ccdc-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
