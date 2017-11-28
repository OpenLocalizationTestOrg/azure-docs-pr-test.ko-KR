---
title: "Azure 자동화 계정 aaaManage | Microsoft Docs"
description: "이 문서에서는 toomanage 인증서 갱신, 삭제 및 잘못 된 구성이 같은 자동화 계정 구성을 hello 하는 방법을 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="8a5f6-103">Azure Automation 계정 관리</span><span class="sxs-lookup"><span data-stu-id="8a5f6-103">Manage Azure Automation account</span></span>
<span data-ttu-id="8a5f6-104">어느 시점 자동화 계정 만료 되기 전에 인증서가 필요 toorenew hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="8a5f6-105">실행 계정이 해당 hello가 손상 된 경우 삭제 한 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="8a5f6-106">이 섹션에서는 어떻게 tooperform 이러한 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="8a5f6-107">자체 서명된 인증서 갱신</span><span class="sxs-lookup"><span data-stu-id="8a5f6-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="8a5f6-108">hello 실행 계정에 대해 만든 자체 서명 된 인증서를 hello hello 생성 날짜 로부터 1 년에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="8a5f6-109">만료되기 전에 언제든지 갱신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="8a5f6-110">Hello 현재 유효한 인증서를 갱신 하기 경우 보존된 tooensure 하는 최대 또는 적극적으로 실행 되 고 실행 계정 hello로 인증 하는 모든 runbook 부정적인 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="8a5f6-111">hello 인증서 만료 날짜까지 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="8a5f6-112">프로그램 엔터프라이즈 인증 기관에서 발급 한 인증서의 자동화 계정으로 실행 계정 toouse 구성한 경우이 옵션을 사용 하는 경우에 hello 엔터프라이즈 인증서 자체 서명 된 인증서로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="8a5f6-113">toorenew hello 인증서, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="8a5f6-114">Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="8a5f6-115">Hello에 **자동화 계정** hello에 블레이드 **속성 계정** 창 아래에서 **계정 설정**선택, **실행 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Automation 계정 속성 창](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="8a5f6-117">Hello에 **실행 계정** 속성 블레이드를 선택 하거나 hello 계정 또는 계정으로 실행 hello 클래식 계정으로 실행에 대 한 toorenew hello 인증서 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="8a5f6-118">Hello에 **속성** 블레이드 hello에 대 한 계정 선택, 클릭 **갱신 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![실행 계정용 인증서 갱신](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="8a5f6-120">Hello 인증서를 갱신 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="8a5f6-121">실행 또는 클래식 실행 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="8a5f6-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="8a5f6-122">이 섹션에서는 설명 방법을 toodelete 다시 실행 또는 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="8a5f6-123">이 작업을 수행 하는 경우 자동화 계정을 hello 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="8a5f6-124">다음 계정으로 실행 또는 클래식 계정으로 실행 계정을 삭제 한 후 hello Azure 포털에에서 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="8a5f6-125">Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="8a5f6-126">Hello에 **자동화 계정** hello 계정 속성 창에서 선택 블레이드 **실행 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="8a5f6-127">Hello에 **실행 계정** toodelete 원하는 계정 속성 블레이드를 선택 하거나 hello 실행 계정 또는 클래식 계정으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="8a5f6-128">그런 다음 hello **속성** 블레이드 hello에 대 한 계정 선택, 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![실행 계정 삭제](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="8a5f6-130">Hello 계정을 삭제 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="8a5f6-131">Hello 계정을 삭제 한 후 다시 만들 수 있습니다이 hello에 **실행 계정** hello를 선택 하 여 속성 블레이드 생성 옵션 **Azure 실행 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Hello 자동화 계정으로 실행 계정을 다시 만드는](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="8a5f6-133">잘못된 구성</span><span class="sxs-lookup"><span data-stu-id="8a5f6-133">Misconfiguration</span></span>
<span data-ttu-id="8a5f6-134">Hello 계정으로 실행 또는 클래식 실행 계정 toofunction에 필요한 일부 구성 항목 제대로 수 삭제 되거나 부적절 하 게 초기 설치 중에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="8a5f6-135">hello 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-135">hello items include:</span></span>

* <span data-ttu-id="8a5f6-136">인증서 자산</span><span class="sxs-lookup"><span data-stu-id="8a5f6-136">Certificate asset</span></span>
* <span data-ttu-id="8a5f6-137">연결 자산</span><span class="sxs-lookup"><span data-stu-id="8a5f6-137">Connection asset</span></span>
* <span data-ttu-id="8a5f6-138">실행 계정은 hello 참가자 역할에서 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="8a5f6-139">Azure AD의 서비스 주체 또는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8a5f6-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="8a5f6-140">위의 hello 및 잘못 된 구성의 다른 인스턴스 hello 자동화 계정을 검색 hello 변경의 상태를 표시 하 고 *완료 안 됨* hello에 **실행 계정** hello에 대 한 속성 블레이드 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![불완전 실행 계정 구성 상태](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="8a5f6-142">Hello 실행 계정을 선택 하면 계정 hello **속성** 창 hello 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![불완전 실행 계정 구성 경고 메시지](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="8a5f6-144">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-144">.</span></span>

<span data-ttu-id="8a5f6-145">삭제 및 다시 hello 계정을 작성 하 여 이러한 계정으로 실행 계정 문제를 신속 하 게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a5f6-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a5f6-146">Next steps</span></span>
* <span data-ttu-id="8a5f6-147">서비스 사용자에 대 한 자세한 내용은 참조 너무[응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="8a5f6-148">Azure 자동화에서 역할 기반 액세스 제어에 대 한 자세한 내용은 참조 너무[Azure 자동화에서 역할 기반 액세스 제어](automation-role-based-access-control.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="8a5f6-149">인증서 및 Azure 서비스에 대 한 자세한 내용은 참조 너무[Azure 클라우드 서비스에 대 한 인증서 개요](../cloud-services/cloud-services-certs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a5f6-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
