---
title: "Azure Security Center에서 투명한 데이터 암호화 사용 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **투명한 데이터 암호화 사용**을 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2a2963affdbff3710ad08f86c6ed4e6304335559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="1577a-103">Azure 보안 센터에서 투명한 데이터 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="1577a-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="1577a-104">아직 TDE(투명한 데이터 암호화)를 사용하도록 설정하지 않은 경우 SQL 데이터베이스에서 TDE를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="1577a-105">TDE는 데이터를 보호하며, 응용 프로그램을 변경할 필요 없이 휴지 상태의 데이터베이스, 연결된 백업 및 트랜잭션 로그 파일을 암호화하여 준수 요구를 충족하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="1577a-106">자세한 내용은 [Azure SQL 데이터베이스를 사용한 투명한 데이터 암호화](https://msdn.microsoft.com/library/dn948096)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1577a-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="1577a-107">이러한 권장 지침은 Azure SQL 서비스에만 적용되며 가상 컴퓨터에서 실행되는 SQL은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="1577a-108">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="1577a-109">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="1577a-110">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="1577a-110">Implement the recommendation</span></span>
1. <span data-ttu-id="1577a-111">**권장 사항** 블레이드에서 **투명한 데이터 암호화 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="1577a-112">![투명한 데이터 암호화 사용][1]</span><span class="sxs-lookup"><span data-stu-id="1577a-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="1577a-113">이렇게 하면 **SQL 데이터베이스에서 투명한 데이터 암호화 사용** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="1577a-114">TDE를 사용하도록 설정할 SQL 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="1577a-115">![SQL DB를 선택하여 TDE 활성화][2]</span><span class="sxs-lookup"><span data-stu-id="1577a-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="1577a-116">**투명한 데이터 암호화** 블레이드의 데이터 암호화에서 **켜기**를 선택하고 블레이드의 위쪽 리본에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="1577a-117">![TDE 켜기][3]</span><span class="sxs-lookup"><span data-stu-id="1577a-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="1577a-118">선택한 SQL Database에서 TDE가 사용되도록 설정되면 **암호화 상태**가 **암호화됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![암호화 상태][4]

## <a name="see-also"></a><span data-ttu-id="1577a-120">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1577a-120">See also</span></span>
<span data-ttu-id="1577a-121">이 문서에서는 보안 센터 권장 사항 "투명한 데이터 암호화 사용"을 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="1577a-122">SQL TDE에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1577a-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="1577a-123">Azure SQL 데이터베이스를 사용한 투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="1577a-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="1577a-124">투명한 데이터 암호화(TDE) 시작</span><span class="sxs-lookup"><span data-stu-id="1577a-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="1577a-125">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1577a-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="1577a-126">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="1577a-127">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1577a-128">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="1577a-129">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="1577a-130">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="1577a-131">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="1577a-132">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1577a-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
