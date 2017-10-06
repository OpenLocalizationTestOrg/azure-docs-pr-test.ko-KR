---
title: "Azure 보안 센터에서 투명 한 데이터 암호화 aaaEnable | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * *를 사용 하도록 설정 투명 한 데이터 암호화 * *입니다."
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
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="a194a-103">Azure 보안 센터에서 투명한 데이터 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="a194a-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="a194a-104">아직 TDE(투명한 데이터 암호화)를 사용하도록 설정하지 않은 경우 SQL 데이터베이스에서 TDE를 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="a194a-105">TDE는에서는 데이터를 보호 하 고 변경 내용을 tooyour 응용 프로그램 필요 없이 데이터베이스, 연결 된 백업 및 트랜잭션 로그 파일에, 암호화 하 여 규정 준수 요구 사항을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="a194a-106">toolearn 더 참조 [Azure SQL 데이터베이스를 사용한 투명 한 데이터 암호화](https://msdn.microsoft.com/library/dn948096)합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="a194a-107">이 권장 사항은 적용 toohello Azure SQL 서비스에만 사용 합니다. 가상 컴퓨터에서 실행 되는 SQL 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="a194a-108">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="a194a-109">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="a194a-110">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="a194a-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="a194a-111">Hello에 **권장 사항을** 블레이드를 **투명 한 데이터 암호화**합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="a194a-112">![투명한 데이터 암호화 사용][1]</span><span class="sxs-lookup"><span data-stu-id="a194a-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="a194a-113">Hello 열립니다 **SQL 데이터베이스에서 투명 한 데이터 암호화를 사용 하도록 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="a194a-114">에 SQL 데이터베이스 tooenable TDE를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="a194a-115">![선택 하는 SQL DB tooenable TDE][2]</span><span class="sxs-lookup"><span data-stu-id="a194a-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="a194a-116">Hello에 **투명 한 데이터 암호화** 블레이드를 **ON** 데이터 암호화 및 선택에서 **저장** hello 블레이드의 hello 위쪽 리본 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="a194a-117">![TDE 켜기][3]</span><span class="sxs-lookup"><span data-stu-id="a194a-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="a194a-118">TDE가 설정 되 면 hello 선택한 SQL 데이터베이스 hello **암호화 상태** 너무 바뀝니다**암호화**합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![암호화 상태][4]

## <a name="see-also"></a><span data-ttu-id="a194a-120">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a194a-120">See also</span></span>
<span data-ttu-id="a194a-121">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 "Enable 투명 한 데이터 암호화 합니다."</span><span class="sxs-lookup"><span data-stu-id="a194a-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="a194a-122">SQL TDE에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="a194a-123">Azure SQL 데이터베이스를 사용한 투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="a194a-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="a194a-124">투명한 데이터 암호화(TDE) 시작</span><span class="sxs-lookup"><span data-stu-id="a194a-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="a194a-125">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="a194a-126">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="a194a-127">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a194a-128">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="a194a-129">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="a194a-130">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="a194a-131">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="a194a-132">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a194a-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
