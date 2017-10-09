---
title: "Azure 보안 센터에서 유효성 검사 aaaAlerts | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터에서 toovalidate hello 보안 경고 하면 있습니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="edffd-103">Azure Security Center에서 경고 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="edffd-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="edffd-104">이 문서에서 이해할 수 있도록 도와 어떻게 tooverify Azure 보안 센터 경고에 대 한 시스템이 올바로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="edffd-105">보안 경고란?</span><span class="sxs-lookup"><span data-stu-id="edffd-105">What are security alerts?</span></span>
<span data-ttu-id="edffd-106">보안 센터 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크 및 방화벽 및 endpoint protection 솔루션, toodetect 경고 있습니다 toothreats 같은 연결 된 파트너 솔루션에서 로그 데이터를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="edffd-107">읽기 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) 보안 경고 보기 및 읽기에 대 한 자세한 내용은 [Azure 보안 센터에서 보안 경고 이해](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn 자세한 에 대 한 hello 다른 유형의 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="edffd-108">경고 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="edffd-108">Alert validation</span></span>
<span data-ttu-id="edffd-109">보안 센터 에이전트가 컴퓨터에 설치 된 후 다음과 같이 hello 아래 hello 컴퓨터에서 toobe 공격 hello 리소스 hello 경고의 원하는 위치.</span><span class="sxs-lookup"><span data-stu-id="edffd-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="edffd-110">실행 파일 (예제 calc.exe) toohello 컴퓨터의 데스크톱 또는 사용자의 편의의 다른 디렉터리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="edffd-111">이 파일을 너무 이름을**ASC_AlertTest_662jfi039N.exe**합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="edffd-112">Hello 명령 프롬프트를 열고 인수 (방금 가짜 인수 이름)으로이 파일을 같이 실행: *ASC_AlertTest_662jfi039N.exe foo*</span><span class="sxs-lookup"><span data-stu-id="edffd-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="edffd-113">5 too10 분 기다린 보안 센터 경고를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="edffd-114">있습니다 하나는 경고와 비슷한 toofollowing를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-114">There you should find an alert similar toofollowing one:</span></span>

    ![경고 유효성 검사](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="edffd-116">이 경고를 검토할 때는 hello 필드 인수 감사가 설정 되어 완전 나타나는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="edffd-117">False 나타나면 tooenable 명령줄 인수 감사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="edffd-118">다음 명령줄 hello를 사용 하 여이 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="edffd-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="edffd-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="edffd-120">참고 항목</span><span class="sxs-lookup"><span data-stu-id="edffd-120">See also</span></span>
<span data-ttu-id="edffd-121">이 문서는 toohello 경고 유효성 검사 프로세스를 도입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="edffd-122">이 유효성 검사에 익숙하다면 했으므로 hello 문서 다음을 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="edffd-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="edffd-123">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="edffd-124">자세한 내용은 방법 toomanage 경고 및 보안 센터에서 toosecurity 인시던트 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="edffd-125">[Azure Security Center에서 보안 상태 모니터링](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="edffd-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="edffd-126">Toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="edffd-127">[Azure Security Center에서 보안 경고 이해](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="edffd-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="edffd-128">Hello 다양 한 유형의 보안 경고에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="edffd-129">[Azure Security Center 문제 해결 가이드](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="edffd-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="edffd-130">보안 센터에서 tootroubleshoot 공통 발급 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="edffd-131">[Azure Security Center FAQ](security-center-faq.md)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="edffd-132">Hello 서비스를 사용 하는 방법에 대 한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="edffd-133">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="edffd-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="edffd-134">Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="edffd-134">Find blog posts about Azure security and compliance.</span></span>

