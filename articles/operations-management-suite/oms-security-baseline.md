---
title: "관리 도구 모음 보안 및 감사 솔루션 초기 aaaOperations | Microsoft Docs"
description: "이 문서에서는 설명 어떻게 toouse OMS 보안 및 감사 솔루션 tooperform 규정 준수 및 보안 용도 대 한 모든 모니터링 대상된 컴퓨터의 초기 평가 합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="94a1f-103">Operations Management Suite 보안 및 감사 솔루션의 기준 평가</span><span class="sxs-lookup"><span data-stu-id="94a1f-103">Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="94a1f-104">이 문서를 사용 하면 toouse [Operations Management Suite (OMS) 보안 및 감사 솔루션](operations-management-suite-overview.md) 기능 tooaccess hello 보안 리소스 상태를 모니터링 하는 초기 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-baseline-assessment"></a><span data-ttu-id="94a1f-105">기준 평가란?</span><span class="sxs-lookup"><span data-stu-id="94a1f-105">What is Baseline Assessment?</span></span>
<span data-ttu-id="94a1f-106">전 세계 산업 및 정부 조직과 함께 Microsoft에서는 보안 수준이 높은 서버 배포를 나타내는 Windows 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-106">Microsoft, together with industry and government organizations worldwide, defines a Windows configuration that represents highly secure server deployments.</span></span> <span data-ttu-id="94a1f-107">이 구성은 일련의 레지스트리 키, 감사 정책 설정 및 이러한 설정에 대한 Microsoft의 권장된 값과 함께 보안 정책 설정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-107">This configuration is a set of registry keys, audit policy settings, and security policy settings along with Microsoft’s recommended values for these settings.</span></span> <span data-ttu-id="94a1f-108">이러한 규칙 집합을 보안 기준이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-108">This set of rules is known as Security baseline.</span></span> <span data-ttu-id="94a1f-109">OMS 보안 및 감사 초기 평가 기능은 규정 준수를 위해 모든 컴퓨터를 원활하게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-109">OMS Security and Audit baseline assessment capability can seamlessly scan all your computers for compliance.</span></span> 

<span data-ttu-id="94a1f-110">세 가지 유형의 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-110">There are three types of rules:</span></span>

* <span data-ttu-id="94a1f-111">**레지스트리 규칙**: 레지스트리 키가 올바르게 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-111">**Registry rules**: check that registry keys are set correctly.</span></span>
* <span data-ttu-id="94a1f-112">**감사 정책 규칙**: 감사 정책과 관한 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-112">**Audit policy rules**: rules regarding your audit policy.</span></span>
* <span data-ttu-id="94a1f-113">**보안 정책 규칙**: hello 컴퓨터에 대 한 hello 사용자의 사용 권한을 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-113">**Security policy rules**: rules regarding hello user’s permissions on hello machine.</span></span>

> [!NOTE]
> <span data-ttu-id="94a1f-114">읽기 [사용 하 여 OMS 보안 tooassess hello 보안 구성 기준을](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) 에 대 한이 기능에 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-114">Read [Use OMS Security tooassess hello Security Configuration Baseline](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) for a brief overview of this feature.</span></span>
> 
> 

## <a name="security-baseline-assessment"></a><span data-ttu-id="94a1f-115">보안 기준 평가</span><span class="sxs-lookup"><span data-stu-id="94a1f-115">Security Baseline Assessment</span></span>
<span data-ttu-id="94a1f-116">OMS 보안 및 감사 hello 대시보드를 사용 하 여 모니터링 되는 모든 컴퓨터에 대 한 현재 보안 초기 평가 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-116">You can review your current security baseline assessment for all computers that are monitored by OMS Security and Audit using hello dashboard.</span></span>  <span data-ttu-id="94a1f-117">다음 단계 tooaccess hello 보안 기준 평가 대시보드 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-117">Execute hello following steps tooaccess hello security baseline assessment dashboard:</span></span>

1. <span data-ttu-id="94a1f-118">Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **보안 및 감사** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-118">In hello **Microsoft Operations Management Suite** main dashboard, click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="94a1f-119">Hello에 **보안 및 감사** 대시보드를 클릭 하 여 **초기 평가** 아래 **보안 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-119">In hello **Security and Audit** dashboard, click **Baseline Assessment** under **Security Domains**.</span></span> <span data-ttu-id="94a1f-120">hello **보안 기준 평가** hello 다음 이미지에에서 표시 된 대로 대시보드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-120">hello **Security Baseline Assessment** dashboard appears as shown in hello following image:</span></span>
   
    ![OMS 보안 및 감사 기준 평가](./media/oms-security-baseline/oms-security-baseline-fig1.png)

<span data-ttu-id="94a1f-122">이 대시보드는 세 가지 주요 영역으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-122">This dashboard is divided in three major areas:</span></span>

* <span data-ttu-id="94a1f-123">**컴퓨터 비교 toobaseline**:이 섹션에서는 hello 평가 통과 한 컴퓨터의 백분율 hello 액세스 된 컴퓨터의 hello 숫자의 요약을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-123">**Computers compared toobaseline**: this section gives a summary of hello number of computers that were accessed and hello percentage of computers that passed hello assessment.</span></span> <span data-ttu-id="94a1f-124">또한 hello 평가 대 한 상위 10 개 컴퓨터 hello 및 hello 백분율 결과 제공.</span><span class="sxs-lookup"><span data-stu-id="94a1f-124">It also gives hello top 10 computers and hello percentage result for hello assessment.</span></span>
* <span data-ttu-id="94a1f-125">**필요한 규칙 상태**:이 섹션 hello 의도 toobring 인식 하지 못했습니다 hello 규칙의 심각도 별로 개이고 유형별로 규칙에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-125">**Required Rules Status**: this section has hello intent toobring awareness of hello failed rules by severity and failed rules by type.</span></span> <span data-ttu-id="94a1f-126">대부분 hello 규칙에 실패 한 경우를 신속 하 게 식별할 수 있습니다 toohello 첫 번째 그래프를 확인 하 여 지에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-126">By looking toohello first graph you can quickly identify if most hello failed rules are critical, or not.</span></span> <span data-ttu-id="94a1f-127">또한 hello 상위 10 개의 실패 한 규칙 및 심각도 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-127">It also gives a list of hello top 10 failed rules and their severity.</span></span> <span data-ttu-id="94a1f-128">hello 두 번째 그래프 hello 유형을 hello 평가 중 실패 한 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-128">hello second graph shows hello type of rule that failed during hello assessment.</span></span> 
* <span data-ttu-id="94a1f-129">**초기 평가 누락 된 컴퓨터**:이 섹션 toooperating 시스템 비호환 또는 실패로 인해 액세스 되지는 hello 컴퓨터의 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-129">**Computers missing baseline assessment**: this section list hello computers that were not accessed due toooperating system incompatibility or failures.</span></span> 

### <a name="accessing-computers-compared-toobaseline"></a><span data-ttu-id="94a1f-130">Toobaseline 비교 컴퓨터에 액세스</span><span class="sxs-lookup"><span data-stu-id="94a1f-130">Accessing computers compared toobaseline</span></span>
<span data-ttu-id="94a1f-131">이상적으로 컴퓨터가 모든 hello 보안 기준 평가 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-131">Ideally all your computers are be compliant with hello security baseline assessment.</span></span> <span data-ttu-id="94a1f-132">그러나 어떤 상황에서는 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-132">However it is expected that in some circumstances this doesn't happen.</span></span> <span data-ttu-id="94a1f-133">Hello 보안 관리 프로세스의 일환으로, toopass 실패 한 모든 보안 평가 테스트 하는 hello 컴퓨터 검토는 중요 한 tooinclude 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-133">As part of hello security management process, it is important tooinclude reviewing hello computers that failed toopass all security assessment tests.</span></span> <span data-ttu-id="94a1f-134">Hello 옵션을 선택 하 여 신속 하 게 toovisualize **액세스 한 컴퓨터** hello에 **컴퓨터 비교 toobaseline** 섹션.</span><span class="sxs-lookup"><span data-stu-id="94a1f-134">A quick way toovisualize that is by selecting hello option **Computers accessed** located in hello **Computers compared toobaseline** section.</span></span> <span data-ttu-id="94a1f-135">Hello 다음 화면에서에서와 같이 hello 로그 검색 결과 표시 된 hello 컴퓨터 목록이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-135">You should see hello log search result showing hello list of computers as shows in hello following screen:</span></span>

![컴퓨터가 액세스한 결과](./media/oms-security-baseline/oms-security-baseline-fig2.png)

<span data-ttu-id="94a1f-137">hello 검색 결과가 여기서 hello 첫 번째 열 hello 컴퓨터와 이름이 hello 두 번째 색 규칙에 실패 한 클라이언트 hello 수는 테이블 형식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-137">hello search result is shown in a table format, where hello first column has hello computer name and hello second color has hello number of rules that failed.</span></span> <span data-ttu-id="94a1f-138">hello 유형의 실패, 규칙에 대 한 tooretrieve hello 정보 hello 수가 hello 컴퓨터 이름 외에도 실패 한 규칙에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-138">tooretrieve hello information regarding hello type of rule that failed, click in hello number of failed rules besides hello computer name.</span></span> <span data-ttu-id="94a1f-139">결과 유사한 toohello hello 다음 이미지에에서 표시 된 것 하나 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-139">You should see a result similar toohello one shown in hello following image:</span></span>

![컴퓨터가 액세스한 결과 세부 정보](./media/oms-security-baseline/oms-security-baseline-fig3.png)

<span data-ttu-id="94a1f-141">이 검색 결과에서 액세스 규칙의 hello 합계, hello 중요 한 규칙에 실패 한 클라이언트 수, 경고 규칙 hello에 있고 정보 실패 규칙 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-141">In this search result, you have hello total of accessed rules, hello number of critical rules that failed, hello warning rules and hello information failed rules.</span></span>

### <a name="accessing-required-rules-status"></a><span data-ttu-id="94a1f-142">필수 규칙 상태 액세스</span><span class="sxs-lookup"><span data-stu-id="94a1f-142">Accessing required rules status</span></span>
<span data-ttu-id="94a1f-143">Hello 평가 통과 한 컴퓨터의 백분율 숫자 hello에 대 한 hello 정보를 얻은 후 tooobtain 되는 규칙에 대 한 자세한 내용은 toohello 중요도 따라 실패 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-143">After obtaining hello information regarding hello percentage number of computers that passed hello assessment, you may want tooobtain more information about which rules are failing according toohello criticality.</span></span> <span data-ttu-id="94a1f-144">Tooprioritize 어떤 컴퓨터 해야 첫 번째 tooensure 해결이 시각화를 사용 하면 됩니다 hello 다음 평가에 규정을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-144">This visualization helps you tooprioritize which computers should be addressed first tooensure they will be compliant in hello next assessment.</span></span> <span data-ttu-id="94a1f-145">Hello에 있는 hello 그래프의 중요 한 부분 hello 위로 마우스를 가져가고 **심각도 별 실패 한 규칙** 타일 아래에서 **필요한 규칙 상태** 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-145">Hover over hello Critical part of hello graph located in hello **Failed rules by severity** tile, under **Required rules status** and click it.</span></span> <span data-ttu-id="94a1f-146">화면 다음 결과 유사한 toohello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-146">You should see a result similar toohello following screen:</span></span>

![심각도별 실패한 규칙 정보](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

<span data-ttu-id="94a1f-148">이 로그 결과 hello 유형의 기준 규칙에 실패 한,이 규칙과이 보안 규칙의 hello 일반적인 구성 열거형 CCE () ID에 대 한 hello 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-148">In this log result you see hello type of baseline rule that failed, hello description of this rule, and hello Common Configuration Enumeration (CCE) ID of this security rule.</span></span> <span data-ttu-id="94a1f-149">이러한 특성 충분 한 tooperform 정정 작업 toofix hello 대상 컴퓨터에서이 문제를 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-149">These attributes should be enough tooperform a corrective action toofix this problem in hello target computer.</span></span>

> [!NOTE]
> <span data-ttu-id="94a1f-150">CCE에 대 한 자세한 내용은 hello 액세스 [National Vulnerability 데이터베이스](https://nvd.nist.gov/cce/index.cfm)합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-150">For more information about CCE, access hello [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm).</span></span>
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="94a1f-151">기준 평가가 누락된 컴퓨터에 액세스</span><span class="sxs-lookup"><span data-stu-id="94a1f-151">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="94a1f-152">OMS는 tooWindows Server 2012 r 2를 Windows Server 2008 r 2에서 도메인 구성원 hello 및 도메인 컨트롤러 초기 프로필을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-152">OMS supports hello domain member and Domain Controller baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="94a1f-153">Windows Server 2016 기준은 계획은 아직 최종본이 아니며 게시되는 즉시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-153">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="94a1f-154">OMS 보안 및 감사 초기 평가 통해 검색 된 다른 모든 운영 체제 hello 아래에 나타납니다. **초기 평가 누락 된 컴퓨터** 섹션.</span><span class="sxs-lookup"><span data-stu-id="94a1f-154">All other operating systems scanned via OMS Security and Audit baseline assessment appears under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="94a1f-155">참고 항목</span><span class="sxs-lookup"><span data-stu-id="94a1f-155">See also</span></span>
<span data-ttu-id="94a1f-156">이 문서에서는 OMS 보안 및 감사 기준 평가에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="94a1f-156">In this document, you learned about OMS Security and Audit baseline assessment.</span></span> <span data-ttu-id="94a1f-157">OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="94a1f-157">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="94a1f-158">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="94a1f-158">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="94a1f-159">모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고</span><span class="sxs-lookup"><span data-stu-id="94a1f-159">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="94a1f-160">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="94a1f-160">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

