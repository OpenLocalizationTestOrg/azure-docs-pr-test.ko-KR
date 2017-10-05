---
title: "Azure AD Connect Sync: 운영 작업 및 고려 사항 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect Sync 및 이 구성 요소를 운영하기 위한 준비 방법에 대한 운영 작업을 설명합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="4c62e-103">Azure AD Connect Sync: 운영 작업 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="4c62e-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="4c62e-104">이 항목은 Azure AD Connect Sync에 대한 관리 작업을 설명하는 것을 목표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="4c62e-105">스테이징 모드</span><span class="sxs-lookup"><span data-stu-id="4c62e-105">Staging mode</span></span>
<span data-ttu-id="4c62e-106">다음을 비롯한 여러 시나리오에 스테이징 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="4c62e-107">고가용성.</span><span class="sxs-lookup"><span data-stu-id="4c62e-107">High availability.</span></span>
* <span data-ttu-id="4c62e-108">새 구성 변경 내용을 테스트하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="4c62e-109">새 서버를 도입하고 이전 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="4c62e-110">스테이징 모드에 있는 서버로 서버를 활성화하기 전에 구성을 변경하고 변경을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="4c62e-111">또한 프로덕션 환경에 해당 변경 사항을 적용하기 전에 필요한지를 확인하기 위해 전체 가져오기 및 동기화를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="4c62e-112">설치 중에 서버를 선택하여 **스테이징 모드**로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="4c62e-113">이 작업은 서버가 가져오기 및 동기화에 대해 활성화하도록 하지만 내보내기는 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="4c62e-114">설치 중에 이러한 기능을 선택하더라도 스테이징 모드에 있는 서버는 암호 동기화 또는 비밀번호 쓰기 저장을 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="4c62e-115">스테이징 모드를 해제하면 서버가 내보내기를 시작하고 암호 동기화 및 비밀번호 쓰기 저장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="4c62e-116">여전히 동기화 서비스 관리자를 사용하여 강제로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="4c62e-117">스테이징 모드에 있는 서버는 Active Directory 및 Azure AD에서 계속 변경 내용을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="4c62e-118">항상 최신 변경 내용의 복사본이 있고 빠르게 다른 서버의 책임을 넘겨 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="4c62e-119">기본 서버의 구성을 변경하는 경우 스테이징 모드에서 서버에 동일한 변경 내용을 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="4c62e-120">이전 동기화 기술에 대해 알고 있는 사용자의 경우 다른 서버에 자체 SQL 데이터베이스가 있으므로 스테이징 모드는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="4c62e-121">이 아키텍처를 통해 스테이징 모드 서버를 다른 데이터 센터에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="4c62e-122">서버의 구성 확인</span><span class="sxs-lookup"><span data-stu-id="4c62e-122">Verify the configuration of a server</span></span>
<span data-ttu-id="4c62e-123">이 메서드를 적용 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="4c62e-124">준비</span><span class="sxs-lookup"><span data-stu-id="4c62e-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="4c62e-125">구성</span><span class="sxs-lookup"><span data-stu-id="4c62e-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="4c62e-126">가져오기 및 동기화</span><span class="sxs-lookup"><span data-stu-id="4c62e-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="4c62e-127">Verify</span><span class="sxs-lookup"><span data-stu-id="4c62e-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="4c62e-128">활성 서버 전환</span><span class="sxs-lookup"><span data-stu-id="4c62e-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="4c62e-129">준비</span><span class="sxs-lookup"><span data-stu-id="4c62e-129">Prepare</span></span>
1. <span data-ttu-id="4c62e-130">Azure AD Connect를 설치하고 **스테이징 모드**를 선택하고 설치 마법사의 마지막 페이지에서 **동기화 시작**의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="4c62e-131">이 모드를 통해 동기화 엔진을 수동으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="4c62e-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="4c62e-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="4c62e-133">시작 메뉴에서 로그오프/로그온하고 **동기화 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="4c62e-134">구성</span><span class="sxs-lookup"><span data-stu-id="4c62e-134">Configuration</span></span>
<span data-ttu-id="4c62e-135">주 서버에 사용자 지정 변경 내용을 적용했으며 구성을 스테이징 서버와 비교하려는 경우 [Azure AD Connect 구성 구조 분석](https://github.com/Microsoft/AADConnectConfigDocumenter)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="4c62e-136">가져오기 및 동기화</span><span class="sxs-lookup"><span data-stu-id="4c62e-136">Import and Synchronize</span></span>
1. <span data-ttu-id="4c62e-137">**커넥터**를 선택하고 **Active Directory Domain Services** 형식을 가진 첫 번째 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="4c62e-138">**실행**을 클릭하고 **전체 가져오기** 및 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="4c62e-139">이 형식인 모든 커넥터에 해당 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="4c62e-140">**Azure Active Directory(Microsoft)**형식이 있는 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="4c62e-141">**실행**을 클릭하고 **전체 가져오기** 및 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="4c62e-142">탭 커넥터가 여전히 선택되어있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="4c62e-143">**Active Directory Domain Services** 형식인 각 커넥터의 경우 **실행**을 클릭하고 **델타 동기화** 및 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="4c62e-144">**Azure Active Directory(Microsoft)**형식이 있는 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="4c62e-145">**실행**을 클릭하고 **델타 동기화** 및 **확인**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="4c62e-146">이제 Azure AD 및 온-프레미스 AD에 스테이징된 내보내기 변경 사항이 있습니다.(Exchange 하이브리드 배포를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="4c62e-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="4c62e-147">다음 단계를 사용하면 디렉터리에 실제로 내보내기를 시작하기 전에 무엇이 변경될지를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="4c62e-148">Verify</span><span class="sxs-lookup"><span data-stu-id="4c62e-148">Verify</span></span>
1. <span data-ttu-id="4c62e-149">cmd 프롬프트를 시작하고 `%ProgramFiles%\Microsoft Azure AD Sync\bin`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="4c62e-150">실행: `csexport "Name of Connector" %temp%\export.xml /f:x` 동기화 서비스에서 커넥터의 이름을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="4c62e-151">Azure AD에 "contoso.com – AAD"와 유사한 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="4c62e-152">섹션 [CSAnalyzer](#appendix-csanalyzer)의 PowerShell 스크립트를 `csanalyzer.ps1`이라는 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="4c62e-153">PowerShell 창을 열고 PowerShell 스크립트를 만든 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="4c62e-154">`.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="4c62e-155">이제 Microsoft Excel에서 검사할 수 있는 **processedusers1.csv**라는 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="4c62e-156">Azure AD로 내보낼 준비가 된 모든 변경 내용은 이 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="4c62e-157">내보내려는 변경 사항이 예정될 때까지 데이터 또는 구성에 필요한 변경을 수행하고 이러한 단계(가져오기 및 동기화 및 확인)를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="4c62e-158">활성 서버 전환</span><span class="sxs-lookup"><span data-stu-id="4c62e-158">Switch active server</span></span>
1. <span data-ttu-id="4c62e-159">Azure AD로 내보내지 않으므로 현재 활성 서버에서 서버를 해제하거나(DirSync/FIM Azure AD Sync) 스테이징 모드로 설정합니다(Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="4c62e-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="4c62e-160">**스테이징 모드** 서버에서 설치 마법사를 실행하고 **스테이징 모드**를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="4c62e-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="4c62e-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="4c62e-162">재해 복구</span><span class="sxs-lookup"><span data-stu-id="4c62e-162">Disaster recovery</span></span>
<span data-ttu-id="4c62e-163">구현 설계의 일부는 동기화 서버를 분실한 경우 재해 발생 시 수행할 작업을 계획하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="4c62e-164">사용할 다른 모델이 있고 어떤 것을 사용하는지는 다음을 포함한 여러 요인에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="4c62e-165">가동 중지 시간 동안 Azure AD에서 개체를 변경하지 않는 오차는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4c62e-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="4c62e-166">암호 동기화를 사용하면 사용자가 온-프레미스를 변경할 경우 Azure AD에서 이전 암호를 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4c62e-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="4c62e-167">비밀번호 쓰기 저장 등의 실시간 작업에 대한 종속성이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4c62e-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="4c62e-168">이러한 질문 및 조직의 정책에 대한 답변에 따라 다음 전략 중 하나를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="4c62e-169">필요할 때 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-169">Rebuild when needed.</span></span>
* <span data-ttu-id="4c62e-170">**스테이징 모드**라고 하는 예비 대기 서버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="4c62e-171">가상 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-171">Use virtual machines.</span></span>

<span data-ttu-id="4c62e-172">기본 제공 SQL Express 데이터베이스를 사용하지 않는 경우 [SQL 고가용성](#sql-high-availability) 섹션도 또한 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="4c62e-173">필요할 때 다시 작성</span><span class="sxs-lookup"><span data-stu-id="4c62e-173">Rebuild when needed</span></span>
<span data-ttu-id="4c62e-174">실행 가능한 전략은 필요할 경우 서버를 다시 작성하려는 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="4c62e-175">일반적으로 동기화 엔진 설치와 초기 가져오기 및 동기화 수행은 몇 시간 안에 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="4c62e-176">사용 가능한 예비 서버가 없는 경우 일시적으로 동기화 엔진을 호스팅하는 데 도메인 컨트롤러를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="4c62e-177">동기화 엔진 서버는 개체에 대한 상태를 저장하지 않으므로 Active Directory 및 Azure AD의 데이터에서 데이터베이스를 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="4c62e-178">**sourceAnchor** 특성을 온-프레미스 및 클라우드에서 개체를 조인하는데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="4c62e-179">기존 온-프레미스 및 클라우드 개체로 서버를 다시 작성하는 경우 다시 설치 시 동기화 엔진은 해당 개체를 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="4c62e-180">문서화 및 저장해야 할 사항은 필터링 및 동기화 규칙 등과 같은 서버의 구성 변경입니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="4c62e-181">동기화를 시작하기 전에 해당 사용자 지정 구성을 다시 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="4c62e-182">스테이징 모드라는 예비 대기 서버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="4c62e-183">더 복잡한 환경을 사용하는 경우 하나 이상의 대기 서버가 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="4c62e-184">설치 중에 서버를 사용하도록 설정하여 **스테이징 모드**로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="4c62e-185">자세한 내용은 [스테이징 모드](#staging-mode)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c62e-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="4c62e-186">가상 컴퓨터 사용</span><span class="sxs-lookup"><span data-stu-id="4c62e-186">Use virtual machines</span></span>
<span data-ttu-id="4c62e-187">일반적이며 지원되는 메서드는 가상 컴퓨터에서 동기화 엔진을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="4c62e-188">호스트에는 문제가 있는 경우 동기화 엔진 서버로 이미지를 다른 서버에 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="4c62e-189">SQL 고가용성</span><span class="sxs-lookup"><span data-stu-id="4c62e-189">SQL High Availability</span></span>
<span data-ttu-id="4c62e-190">Azure AD Connect와 함께 제공되는 SQL Server Express를 사용하지 않는 경우 SQL Server에 대한 고가용성을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="4c62e-191">지원되는 고가용성 솔루션은 SQL 클러스터링 및 AOA(Always On 가용성 그룹)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="4c62e-192">지원되지 않는 솔루션은 미러링을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="4c62e-193">버전 1.1.524.0에서는 SQL AOA에 대한 지원이 Azure AD Connect에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="4c62e-194">Azure AD Connect를 설치하기 전에 SQL AOA를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="4c62e-195">Azure AD Connect는 설치 중에 제공된 SQL 인스턴스에서 SQL AOA를 사용하도록 설정되었는지 여부를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="4c62e-196">SQL AOA를 사용하도록 설정된 경우 Azure AD Connect는 SQL AOA에서 동기 복제 또는 비동기 복제를 사용하도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="4c62e-197">가용성 그룹 수신기를 설정할 때 RegisterAllProvidersIP 속성을 0으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="4c62e-198">이는 Azure AD Connect에서 현재 SQL Native Client를 사용하여 SQL에 연결하고, SQL Native Client에서는 MultiSubNetFailover 속성 사용을 지원하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4c62e-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="4c62e-199">Appendix CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="4c62e-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="4c62e-200">이 스크립트 사용 방법은 [verity](#verify) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c62e-200">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="4c62e-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c62e-201">Next steps</span></span>
<span data-ttu-id="4c62e-202">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="4c62e-202">**Overview topics**</span></span>  

* [<span data-ttu-id="4c62e-203">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4c62e-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="4c62e-204">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="4c62e-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
