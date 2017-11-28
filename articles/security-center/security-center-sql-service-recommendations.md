---
title: "Azure SQL aaaProtecting Azure 보안 센터에서 데이터 및 서비스 | Microsoft Docs"
description: "이 문서에서는 데이터 및 Azure SQL 서비스를 보호하고 보안 정책을 준수하는 데 도움이 되는 Azure Security Center의 권장 사항에 대해 설명합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="09dcb-103">Azure Security Center에서 Azure SQL 서비스 및 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="09dcb-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="09dcb-104">Azure 보안 센터 리소스를 Azure의 hello 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="09dcb-105">보안 센터 잠재적인 보안 문제를 식별 하는 경우 필요한 hello 컨트롤 구성 hello 과정을 안내 하는 권장 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="09dcb-106">권장 사항이 적용 tooAzure 리소스 종류: 가상 컴퓨터 (Vm), 네트워킹, SQL 및 데이터 및 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="09dcb-107">이 문서에서는 tooAzure SQL 서비스 및 데이터에 적용 되는 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="09dcb-108">권장 사항은 Azure SQL 서버 및 데이터베이스에 대한 감사 사용 및 SQL Database에 대한 암호화 설정, Azure Storage 계정의 암호화 설정에 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="09dcb-109">사용할 수 있는 SQL 서비스 및 데이터 권장 hello 및 각 용도 적용 하는 경우 참조 toohelp으로 아래 hello 테이블 사용 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="09dcb-110">제공되는 SQL 서비스 및 데이터 권장 사항</span><span class="sxs-lookup"><span data-stu-id="09dcb-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="09dcb-111">권장 사항</span><span class="sxs-lookup"><span data-stu-id="09dcb-111">Recommendation</span></span> | <span data-ttu-id="09dcb-112">설명</span><span class="sxs-lookup"><span data-stu-id="09dcb-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="09dcb-113">SQL Server에서 감사 및 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="09dcb-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="09dcb-114">Azure SQL 서버(Azure SQL 서비스만 해당, 가상 컴퓨터에서 실행되는 SQL 제외됨)에 감사 및 위협 감지를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="09dcb-115">SQL Database에서 감사 및 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="09dcb-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="09dcb-116">Azure SQL 서버(Azure SQL Database만 해당, 가상 컴퓨터에서 실행되는 SQL 제외됨)에 감사 및 위협 감지를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="09dcb-117">SQL 데이터베이스에서 투명한 데이터 암호화 활성화</span><span class="sxs-lookup"><span data-stu-id="09dcb-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="09dcb-118">SQL 데이터베이스(Azure SQL 서비스에만 해당)에 대해 암호화를 활성화하라는 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="09dcb-119">참고 항목</span><span class="sxs-lookup"><span data-stu-id="09dcb-119">See also</span></span>
<span data-ttu-id="09dcb-120">tooother Azure 리소스 유형에 적용 되는 권장 사항에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="09dcb-121">Azure 보안 센터에서 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="09dcb-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="09dcb-122">Azure 보안 센터에서 응용 프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="09dcb-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="09dcb-123">Azure 보안 센터에서 네트워크 보호</span><span class="sxs-lookup"><span data-stu-id="09dcb-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="09dcb-124">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="09dcb-125">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="09dcb-126">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="09dcb-127">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="09dcb-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
