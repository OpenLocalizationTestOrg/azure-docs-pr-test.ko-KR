---
title: "Azure 보안 센터에서 유형별 aaaSecurity 경고 | Microsoft Docs"
description: "이 문서에서는 hello 다른 종류의 Azure 보안 센터에서 사용할 수 있는 보안 경고를 설명 합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a><span data-ttu-id="0dd21-103">Azure Security Center에서 보안 경고 이해</span><span class="sxs-lookup"><span data-stu-id="0dd21-103">Understanding security alerts in Azure Security Center</span></span>
<span data-ttu-id="0dd21-104">이 문서는 toounderstand hello 다양 한 유형의 보안 경고 및 Azure 보안 센터에서 사용할 수 있는 관련된 insights는 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-104">This article helps you toounderstand hello different types of security alerts and related insights that are available in Azure Security Center.</span></span> <span data-ttu-id="0dd21-105">Toomanage 알림 및 인시던트를 참조 하는 방법에 대 한 자세한 내용은 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-105">For more information on how toomanage alerts and incidents, see [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0dd21-106">tooset 고급 검색을 업그레이드 tooAzure 보안 센터 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-106">tooset up advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="0dd21-107">무료 60일 평가판을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-107">A free 60-day trial is available.</span></span> <span data-ttu-id="0dd21-108">tooupgrade, **가격 책정 계층** hello에 [보안 정책](security-center-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-108">tooupgrade, select **Pricing Tier** in hello [security policy](security-center-policies.md).</span></span> <span data-ttu-id="0dd21-109">toolearn hello을 더 참조 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/security-center/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-109">toolearn more, see hello [pricing page](https://azure.microsoft.com/pricing/details/security-center/).</span></span>
>

## <a name="what-type-of-alerts-are-available"></a><span data-ttu-id="0dd21-110">어떤 유형의 경고를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="0dd21-110">What type of alerts are available?</span></span>
<span data-ttu-id="0dd21-111">Azure 보안 센터의 다양 한 사용 하 여 [검색 기능이](security-center-detection-capabilities.md) tooalert 고객 toopotential 공격 환경을 대상으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-111">Azure Security Center uses a variety of [detection capabilities](security-center-detection-capabilities.md) tooalert customers toopotential attacks targeting their environments.</span></span> <span data-ttu-id="0dd21-112">이러한 경고 hello 알림을 hello 리소스, 대상 및 소스 hello 공격의 hello 트리거된 항목 hello에 대 한 중요 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-112">These alerts contain valuable information about hello what triggered hello alert, hello resources targeted, and hello source of hello attack.</span></span> <span data-ttu-id="0dd21-113">경고에 포함 된 hello 정보 사용 분석 toodetect hello 위협 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-113">hello information included in an alert varies based on hello type of analytics used toodetect hello threat.</span></span> <span data-ttu-id="0dd21-114">인시던트는 위협을 조사할 때 유용할 수 있는 추가 컨텍스트 정보를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-114">Incidents may also contain additional contextual information that can be useful when investigating a threat.</span></span>  <span data-ttu-id="0dd21-115">이 문서는 경고 유형에 따라 hello에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-115">This article provides information about hello following alert types:</span></span>

* <span data-ttu-id="0dd21-116">VMBA(가상 컴퓨터 동작 분석)</span><span class="sxs-lookup"><span data-stu-id="0dd21-116">Virtual Machine Behavioral Analysis (VMBA)</span></span>
* <span data-ttu-id="0dd21-117">네트워크 분석</span><span class="sxs-lookup"><span data-stu-id="0dd21-117">Network Analysis</span></span>
* <span data-ttu-id="0dd21-118">리소스 분석</span><span class="sxs-lookup"><span data-stu-id="0dd21-118">Resource Analysis</span></span>
* <span data-ttu-id="0dd21-119">컨텍스트 정보</span><span class="sxs-lookup"><span data-stu-id="0dd21-119">Contextual Information</span></span>

## <a name="virtual-machine-behavioral-analysis"></a><span data-ttu-id="0dd21-120">VMBA(가상 컴퓨터 동작 분석)</span><span class="sxs-lookup"><span data-stu-id="0dd21-120">Virtual machine behavioral analysis</span></span>
<span data-ttu-id="0dd21-121">Azure 보안 센터의 가상 컴퓨터 이벤트 로그 분석에 따라 동작 분석 손상 tooidentify 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-121">Azure Security Center can use behavioral analytics tooidentify compromised resources based on analysis of virtual machine event logs.</span></span> <span data-ttu-id="0dd21-122">예를 들어 프로세스 만들기 이벤트 및 로그인 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-122">For example, Process Creation Events and Login Events.</span></span> <span data-ttu-id="0dd21-123">또한 광범위 한 캠페인의 증거를 지원 하기 위한 다른 신호 toocheck와의 상관 관계는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-123">In addition, there is correlation with other signals toocheck for supporting evidence of a widespread campaign.</span></span>

> [!NOTE]
> <span data-ttu-id="0dd21-124">Security Center 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dd21-124">For more information on how Security Center detection capabilities work, see [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>
>

### <a name="crash-analysis"></a><span data-ttu-id="0dd21-125">충돌 분석</span><span class="sxs-lookup"><span data-stu-id="0dd21-125">Crash analysis</span></span>
<span data-ttu-id="0dd21-126">크래시 덤프 메모리 분석을 사용 하는 방법 toodetect 정교한 맬웨어 수 tooevade 기존 보안 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-126">Crash dump memory analysis is a method used toodetect sophisticated malware that is able tooevade traditional security solutions.</span></span> <span data-ttu-id="0dd21-127">다양 한 형태의 맬웨어 tooreduce hello 가능성이 되지 toodisk를 작성 하 여 또는 toodisk 작성 하는 소프트웨어 구성 요소를 암호화 하 여 바이러스 백신 제품에서 검색 하는 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-127">Various forms of malware try tooreduce hello chance of being detected by antivirus products by never writing toodisk, or by encrypting software components written toodisk.</span></span> <span data-ttu-id="0dd21-128">따라서 기존 맬웨어 방지 접근 방식을 사용 하 여 hello 맬웨어 어려운 toodetect 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-128">This makes hello malware difficult toodetect by using traditional antimalware approaches.</span></span> <span data-ttu-id="0dd21-129">그러나 이러한 종류의 맬웨어 맬웨어 순서 toofunction 메모리에 추적을 유지 해야 하기 때문에 메모리 분석을 사용 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-129">However, this kind of malware can be detected by using memory analysis, because malware must leave traces in memory in order toofunction.</span></span>

<span data-ttu-id="0dd21-130">소프트웨어 충돌, 크래시 덤프는 hello 충돌 hello 시 메모리의 일부를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-130">When software crashes, a crash dump captures a portion of memory at hello time of hello crash.</span></span> <span data-ttu-id="0dd21-131">hello 크래시 맬웨어, 일반 응용 프로그램 또는 시스템 문제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-131">hello crash may be caused by malware, general application or system issues.</span></span> <span data-ttu-id="0dd21-132">Hello 크래시 덤프의 hello 메모리를 분석 하 여 보안 센터 수 tooexploit 취약점 소프트웨어에서 사용 하는 기술을 검색, 기밀 데이터를 액세스 및 부정적 손상 된 컴퓨터 내에서 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-132">By analyzing hello memory in hello crash dump, Security Center can detect techniques used tooexploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine.</span></span> <span data-ttu-id="0dd21-133">이 hello 분석은 보안 센터 다시 종료 hello 수행한 것으로 최소 성능 영향 toohosts 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-133">This is accomplished with minimum performance impact toohosts as hello analysis is performed by hello Security Center back end.</span></span>

<span data-ttu-id="0dd21-134">다음 필드는 hello은 일반적인 toohello 크래시 덤프 경고 예가이 문서의 뒷부분에 나오는 나타나는:</span><span class="sxs-lookup"><span data-stu-id="0dd21-134">hello following fields are common toohello crash dump alert examples that appear later in this article:</span></span>

* <span data-ttu-id="0dd21-135">Hello 크래시 덤프 파일의 덤프 파일: 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-135">DUMPFILE: Name of hello crash dump file.</span></span>
* <span data-ttu-id="0dd21-136">Hello 충돌 프로세스의 PROCESSNAME: 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-136">PROCESSNAME: Name of hello crashing process.</span></span>
* <span data-ttu-id="0dd21-137">프로세스 충돌 하는 hello의 PROCESSVERSION: 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-137">PROCESSVERSION: Version of hello crashing process.</span></span>

### <a name="shellcode-discovered"></a><span data-ttu-id="0dd21-138">Shellcode 검색</span><span class="sxs-lookup"><span data-stu-id="0dd21-138">Shellcode discovered</span></span>
<span data-ttu-id="0dd21-139">Shellcode는 소프트웨어 취약점을 악용 하는 맬웨어 후 실행 되는 hello 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-139">Shellcode is hello payload that is run after malware exploits a software vulnerability.</span></span> <span data-ttu-id="0dd21-140">이 경고는 크래시 덤프 분석이 악의적인 페이로드에서 일반적으로 수행되는 동작을 표시하는 실행 코드를 감지했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-140">This alert indicates that crash dump analysis has detected executable code that exhibits behavior that is commonly performed by malicious payloads.</span></span> <span data-ttu-id="0dd21-141">악의적이지 않은 소프트웨어가 이 동작을 수행할 수 있지만 보통 소프트웨어 개발 방법으로서는 일반적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-141">Although non-malicious software may perform this behavior, it is not typical of normal software development practices.</span></span>

<span data-ttu-id="0dd21-142">hello Shellcode 경고 예 hello를 다음 추가 필드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-142">hello Shellcode alert example provides hello following additional field:</span></span>

* <span data-ttu-id="0dd21-143">Hello shellcode의 메모리 주소: hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-143">ADDRESS: hello location in memory of hello shellcode.</span></span>

<span data-ttu-id="0dd21-144">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-144">This is an example of this type of alert:</span></span>

![Shellcode 경고](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a><span data-ttu-id="0dd21-146">모듈 하이재킹 검색</span><span class="sxs-lookup"><span data-stu-id="0dd21-146">Module hijacking discovered</span></span>
<span data-ttu-id="0dd21-147">Windows 동적 연결 라이브러리 (Dll) tooallow 소프트웨어 tooutilize 공통 Windows 시스템 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-147">Windows uses dynamic-link libraries (DLLs) tooallow software tooutilize common Windows system functionality.</span></span> <span data-ttu-id="0dd21-148">DLL 하이재킹 변경 될 때 발생 맬웨어 hello DLL 로드 순서 tooload 악의적인 페이로드 메모리에 임의의 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-148">DLL Hijacking occurs when malware changes hello DLL load order tooload malicious payloads into memory, where arbitrary code can be executed.</span></span> <span data-ttu-id="0dd21-149">이 경고 hello 크래시 덤프를 분석 두 개의 서로 다른 경로에서 로드 된 유사한 이름의 모듈 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-149">This alert indicates that hello crash dump analysis detected a similarly named module that is loaded from two different paths.</span></span> <span data-ttu-id="0dd21-150">로드 하는 hello 패스 중 하나의 공통 Windows 시스템 이진 위치에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-150">One of hello loaded paths comes from a common Windows system binary location.</span></span>

<span data-ttu-id="0dd21-151">소프트웨어의 합법적인 개발자는 가끔 계측, 확장 hello Windows 운영 체제 또는 Windows 응용 프로그램을 확장 하는 등의 악의적인 내용이 이유로 hello DLL 로드 순서를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-151">Legitimate software developers occasionally change hello DLL load order for non-malicious reasons, such as instrumenting, extending hello Windows OS, or extending a Windows application.</span></span> <span data-ttu-id="0dd21-152">toohelp 취급 악의적인 및 잠재적으로 심각 하지 않은 변경 내용 toohello DLL 로드 순서, Azure 보안 센터 로드 된 모듈 tooa 의심 스러운 프로필 준수 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-152">toohelp differentiate between malicious and potentially benign changes toohello DLL load order, Azure Security Center checks whether a loaded module conforms tooa suspicious profile.</span></span> <span data-ttu-id="0dd21-153">이 검사의 결과 hello hello 경고의 hello "서명" 필드에 따라 표시 되 고 hello 심각도 hello 경고, 경고 설명 및 경고 문제 해결 단계에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-153">hello result of this check is indicated by hello “SIGNATURE” field of hello alert and is reflected in hello severity of hello alert, alert description, and alert remediation steps.</span></span> <span data-ttu-id="0dd21-154">tooresearch 올 바르 거 나 악성 hello 모듈 인지 모듈을 하이재킹 하는 hello의 디스크 복사본에 대해 hello를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-154">tooresearch whether hello module is legitimate or malicious, analyze hello on disk copy of hello hijacking module.</span></span> <span data-ttu-id="0dd21-155">예를 들어 바이러스 검사를 실행 하거나 hello 파일의 디지털 서명을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-155">For example, you can verify hello file's digital signature, or run an antivirus scan.</span></span>

<span data-ttu-id="0dd21-156">또한 hello 이전 "Shellcode 검색" 섹션에 설명 된 공통 필드 toohello이이 경고 필드를 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="0dd21-156">In addition toohello common fields described in hello earlier “Shellcode discovered” section, this alert provides hello following fields:</span></span>

* <span data-ttu-id="0dd21-157">서명: 모듈을 하이재킹 하는 hello tooa 의심 스러운 동작 프로필을 준수 하는 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-157">SIGNATURE: Indicates if hello hijacking module conforms tooa suspicious behavior profile.</span></span>
* <span data-ttu-id="0dd21-158">HIJACKEDMODULE: hello의 hello 이름을 하이재킹 Windows 시스템 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-158">HIJACKEDMODULE: hello name of hello hijacked Windows system module.</span></span>
* <span data-ttu-id="0dd21-159">HIJACKEDMODULEPATH: hello의 hello 경로 Windows 시스템 모듈을 하이재킹입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-159">HIJACKEDMODULEPATH: hello path of hello hijacked Windows system module.</span></span>
* <span data-ttu-id="0dd21-160">Hello 하이재킹 모듈의 HIJACKINGMODULEPATH: hello 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-160">HIJACKINGMODULEPATH: hello path of hello hijacking module.</span></span>

<span data-ttu-id="0dd21-161">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-161">This is an example of this type of alert:</span></span>

![모듈 하이재킹 경고](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a><span data-ttu-id="0dd21-163">위장 Windows 모듈 감지</span><span class="sxs-lookup"><span data-stu-id="0dd21-163">Masquerading Windows module detected</span></span>
<span data-ttu-id="0dd21-164">맬웨어는 Windows 시스템 이진 파일 (예를 들어 다음과 같이 SVCHOST의 일반 이름을 사용할 수 있습니다. EXE) 또는 모듈 (예를 들어 NTDLL 합니다. DLL) 너무*조화* 및 시스템 관리자에 게 hello 악성 소프트웨어의 hello 특성을 모호 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-164">Malware may use common names of Windows system binaries (for example, SVCHOST.EXE) or modules (for example, NTDLL.DLL) too*blend in* and obscure hello nature of hello malicious software from system administrators.</span></span> <span data-ttu-id="0dd21-165">이 경고는 hello 크래시 덤프를 분석이 해당 hello 크래시 덤프 파일에 Windows 시스템 모듈 이름을 사용 하지만 Windows 모듈의 일반적인 하는 다른 조건을 충족 하지 않는 모듈이 감지 했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-165">This alert indicates that hello crash dump analysis detects that hello crash dump file contains modules that use Windows system module names, but do not satisfy other criteria that are typical of Windows modules.</span></span> <span data-ttu-id="0dd21-166">디스크 복사본을 hello 가상 모듈 분석 hello이이 모듈의 hello 올 바르 거 나 악성 특성에 대 한 자세한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-166">Analyzing hello on disk copy of hello masquerading module may provide more information about hello legitimate or malicious nature of this module.</span></span> <span data-ttu-id="0dd21-167">분석은 다음을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-167">Analysis may include:</span></span>

* <span data-ttu-id="0dd21-168">소프트웨어의 합법적인 패키지의 일부로 제공 되는 hello 해당 파일에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-168">Confirm that hello file in question is shipped as part of a legitimate software package.</span></span>
* <span data-ttu-id="0dd21-169">Hello 파일의 디지털 서명을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-169">Verify hello file’s digital signature.</span></span>
* <span data-ttu-id="0dd21-170">Hello 파일에 대해 바이러스 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-170">Run an antivirus scan on hello file.</span></span>

<span data-ttu-id="0dd21-171">또한 toohello 공통 필드 hello "Shellcode 검색" 섹션의 앞부분에서 설명한이 경고는 hello 추가 필드를 다음을 제공:</span><span class="sxs-lookup"><span data-stu-id="0dd21-171">In addition toohello common fields described earlier in hello “Shellcode discovered” section, this alert provides hello following additional fields:</span></span>

* <span data-ttu-id="0dd21-172">세부 정보: hello 모듈의 메타 데이터가 유효 하 고 hello 모듈이 시스템 경로에서 로드 되는 여부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-172">DETAILS: Describes whether hello module's metadata is valid, and whether hello module was loaded from a system path.</span></span>
* <span data-ttu-id="0dd21-173">이름: hello hello 가상 Windows 모듈의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-173">NAME: hello name of hello masquerading Windows module.</span></span>
* <span data-ttu-id="0dd21-174">경로: hello 경로 toohello 가상 Windows 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-174">PATH: hello path toohello masquerading Windows module.</span></span>

<span data-ttu-id="0dd21-175">이 경고 또한 추출 하 고 "CHECKSUM" 및 "TIMESTAMP"와 같은 hello 모듈의 PE 헤더에서 특정 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-175">This alert also extracts and displays certain fields from hello module’s PE header, such as “CHECKSUM” and “TIMESTAMP.”</span></span> <span data-ttu-id="0dd21-176">이러한 필드는 hello 필드 hello 모듈에 있는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-176">These fields are only displayed if hello fields are present in hello module.</span></span> <span data-ttu-id="0dd21-177">Hello 참조 [Microsoft PE 및 COFF 사양](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) 이러한 필드에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-177">See hello [Microsoft PE and COFF Specification](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) for details on these fields.</span></span>

<span data-ttu-id="0dd21-178">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-178">This is an example of this type of alert:</span></span>

![가상 Windows 경고](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a><span data-ttu-id="0dd21-180">수정된 시스템 이진 파일 검색</span><span class="sxs-lookup"><span data-stu-id="0dd21-180">Modified system binary discovered</span></span>
<span data-ttu-id="0dd21-181">맬웨어 순서 toocovertly 데이터 액세스에서에서 핵심 시스템 이진 파일을 수정 또는 부정적 손상된 된 시스템에 유지 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-181">Malware may modify core system binaries in order toocovertly access data or surreptitiously persist on a compromised system.</span></span> <span data-ttu-id="0dd21-182">이 경고 메모리 나 디스크에 핵심 Windows OS 바이너리 수정 된 hello 크래시 덤프를 분석에 검색을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-182">This alert indicates that hello crash dump analysis has detected that core Windows OS binaries have been modified in memory or on disk.</span></span>

<span data-ttu-id="0dd21-183">때때로 합법적인 소프트웨어 개발자는 Detours 등 응용 프로그램 호환성을 위해 악의적이지 않은 이유로 메모리에서 자유롭게 시스템 모듈을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-183">Legitimate software developers occasionally modify system modules in memory for non-malicious reasons, such as Detours or for application compatibility.</span></span> <span data-ttu-id="0dd21-184">toohelp 취급 악의적인 및 잠재적으로 합법적인 모듈, Azure 보안 센터 hello 수정 된 모듈 tooa 의심 스러운 프로필 준수 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-184">toohelp differentiate between malicious and potentially legitimate modules, Azure Security Center checks whether hello modified module conforms tooa suspicious profile.</span></span> <span data-ttu-id="0dd21-185">이 검사의 결과 hello hello 심각도 hello 경고, 경고 설명 및 경고 업데이트 관리 단계가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-185">hello result of this check is indicated by hello severity of hello alert, alert description, and alert remediation steps.</span></span>

<span data-ttu-id="0dd21-186">또한 toohello 공통 필드 hello "Shellcode 검색" 섹션의 앞부분에서 설명한이 경고는 hello 추가 필드를 다음을 제공:</span><span class="sxs-lookup"><span data-stu-id="0dd21-186">In addition toohello common fields described earlier in hello “Shellcode discovered” section, this alert provides hello following additional fields:</span></span>

* <span data-ttu-id="0dd21-187">MODULENAME: hello의 이름을 시스템 바이너리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-187">MODULENAME: Name of hello modified system binary.</span></span>
* <span data-ttu-id="0dd21-188">MODULEVERSION: 버전의 hello 시스템 바이너리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-188">MODULEVERSION: Version of hello modified system binary.</span></span>

<span data-ttu-id="0dd21-189">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-189">This is an example of this type of alert:</span></span>

![시스템 이진 경고](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a><span data-ttu-id="0dd21-191">의심스러운 프로세스 실행</span><span class="sxs-lookup"><span data-stu-id="0dd21-191">Suspicious process executed</span></span>
<span data-ttu-id="0dd21-192">보안 센터 hello 대상 가상 컴퓨터에서 실행 되 고 다음 경고를 트리거하는 의심 스러운 프로세스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-192">Security Center identifies a suspicious process that runs on hello target virtual machine, and then triggers an alert.</span></span> <span data-ttu-id="0dd21-193">hello 검색 hello 특정 이름에 대 한 व ै 있지만 hello 실행 파일의 매개 변수를 찾고지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-193">hello detection doesn’t look for hello specific name, but does look for hello executable file's parameter.</span></span> <span data-ttu-id="0dd21-194">따라서 hello 공격자가 hello 실행 파일 이름을 바꾸거나, 경우에 보안 센터 hello 의심 스러운 프로세스를 계속 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-194">Therefore, even if hello attacker renames hello executable, Security Center can still detect hello suspicious process.</span></span>

<span data-ttu-id="0dd21-195">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-195">This is an example of this type of alert:</span></span>

![의심스러운 프로세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a><span data-ttu-id="0dd21-197">여러 도메인 계정 쿼리</span><span class="sxs-lookup"><span data-stu-id="0dd21-197">Multiple domain accounts queried</span></span>
<span data-ttu-id="0dd21-198">보안 센터 여러 tooquery Active Directory 도메인 계정에이 시도 감지할 수 공격자가 네트워크 검사 하는 동안 일반적으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-198">Security Center can detect multiple attempts tooquery Active Directory domain accounts, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="0dd21-199">공격자가이 기술은 tooquery hello 도메인 tooidentify hello 사용자 활용 하 여, hello 도메인 관리자 계정을 식별, hello 컴퓨터를 확인 하는 도메인 컨트롤러와도 다른 도메인과 hello 잠재적 도메인 트러스트 관계를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-199">Attackers can leverage this technique tooquery hello domain tooidentify hello users, identify hello domain admin accounts, identify hello computers that are domain controllers, and also identify hello potential domain trust relationship with other domains.</span></span>

<span data-ttu-id="0dd21-200">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-200">This is an example of this type of alert:</span></span>

![여러 도메인 계정 경고](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a><span data-ttu-id="0dd21-202">로컬 관리자 그룹 구성원이 열거됨</span><span class="sxs-lookup"><span data-stu-id="0dd21-202">Local Administrators group members were enumerated</span></span>

<span data-ttu-id="0dd21-203">Windows Server 2016 및 Windows 10의 보안 이벤트 hello 4798, 하나의 트리거되는 경우 보안 센터 tootrigger 경고 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-203">Security Center is going tootrigger an alert when hello security event 4798, in Windows Server 2016 and Windows 10, is trigged.</span></span> <span data-ttu-id="0dd21-204">로컬 관리자 그룹이 열거될 때 발생하며 이는 일반적으로 네트워크 정찰 중에 공격자에 의해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-204">This happens when local administrator groups are enumerated, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="0dd21-205">공격자는이 기술을 tooquery hello 관리 권한 가진 사용자의 id를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-205">Attackers can leverage this technique tooquery hello identity of users with administrative privileges.</span></span>

<span data-ttu-id="0dd21-206">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-206">This is an example of this type of alert:</span></span>

![로컬 관리자](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a><span data-ttu-id="0dd21-208">대/소문자의 비정상적인 혼합</span><span class="sxs-lookup"><span data-stu-id="0dd21-208">Anomalous mix of upper and lower case characters</span></span>

<span data-ttu-id="0dd21-209">보안 센터 대문자 및 소문자 hello 명령줄에서는 hello 사용 감지 되 면 경고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-209">Security Center will trigger an alert when it detects hello use of a mix of upper and lower case characters at hello command line.</span></span> <span data-ttu-id="0dd21-210">해시 기반 컴퓨터 규칙 또는 일부 공격자가에서 대/소문자 구분이 기술은 toohide를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-210">Some attackers may use this technique toohide from case-sensitive or hash based machine rule.</span></span>

<span data-ttu-id="0dd21-211">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-211">This is an example of this type of alert:</span></span>

![비정상적인 혼합](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a><span data-ttu-id="0dd21-213">의심스러운 Kerberos Golden Ticket 공격</span><span class="sxs-lookup"><span data-stu-id="0dd21-213">Suspected Kerberos Golden Ticket attack</span></span>

<span data-ttu-id="0dd21-214">공격에 노출 된 [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) 공격자가 toocreate Kerberos "골든 티켓," hello 공격자가 tooimpersonate 하려는 모든 사용자 허용 하 여 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-214">A compromised [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) key can be used by an attacker toocreate Kerberos "Golden Tickets," allowing hello attacker tooimpersonate any user they wish.</span></span> <span data-ttu-id="0dd21-215">보안 센터 이러한 유형의 활동을 감지 하면 경고 tootrigger를 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-215">Security Center is going tootrigger an alert when it detects this type of activity.</span></span>

> [!NOTE] 
> <span data-ttu-id="0dd21-216">Kerberos Golden Ticket에 대한 자세한 내용은 [Windows 10 자격 증명 도난 방지 가이드](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dd21-216">For more information about Kerberos Golden Ticket, read [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).</span></span>

<span data-ttu-id="0dd21-217">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-217">This is an example of this type of alert:</span></span>

![Golden ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a><span data-ttu-id="0dd21-219">의심스러운 계정 생성</span><span class="sxs-lookup"><span data-stu-id="0dd21-219">Suspicious account created</span></span>

<span data-ttu-id="0dd21-220">Security Center는 기존의 기본 제공 관리 권한 계정과 매우 유사한 계정을 만들 때 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-220">Security Center will trigger an alert when an account is created with close resemblance of an existing built in administrative privilege account.</span></span> <span data-ttu-id="0dd21-221">이 기술은 공격자가 toocreate 악의적 tooavoid 휴먼 확인 하 여 알림 메시지를 고려 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-221">This technique can be used by attackers toocreate a rogue account tooavoid being noticed by human verification.</span></span>
 
<span data-ttu-id="0dd21-222">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-222">This is an example of this type of alert:</span></span>

![의심스러운 계정](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a><span data-ttu-id="0dd21-224">의심스러운 방화벽 규칙 생성됨</span><span class="sxs-lookup"><span data-stu-id="0dd21-224">Suspicious Firewall rule created</span></span>

<span data-ttu-id="0dd21-225">공격자가 명령 및 컨트롤을 사용 하 여 사용자 지정 방화벽 규칙 tooallow 악성 응용 프로그램이 toocommunicate 만들어 toocircumvent 호스트 보안 보십시오 또는 hello 통해 hello 네트워크를 통해 toolaunch 공격 손상 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-225">Attackers might try toocircumvent host security by creating custom firewall rules tooallow malicious applications toocommunicate with command and control, or toolaunch attacks through hello network via hello compromised host.</span></span> <span data-ttu-id="0dd21-226">Security Center는 의심스러운 위치의 실행 파일에서 새 방화벽 규칙이 생성된 것을 감지하면 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-226">Security Center will trigger an alert when it detects that a new firewall rule was created from an executable file in a suspicious location.</span></span>
 
<span data-ttu-id="0dd21-227">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-227">This is an example of this type of alert:</span></span>

![방화벽 규칙](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a><span data-ttu-id="0dd21-229">HTA 및 PowerShell의 의심스러운 조합</span><span class="sxs-lookup"><span data-stu-id="0dd21-229">Suspicious combination of HTA and PowerShell</span></span>

<span data-ttu-id="0dd21-230">Security Center는 Microsoft HTML Application Host(HTA)에서 PowerShell 명령이 실행되는 것을 감지하면 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-230">Security Center will trigger an alert when it detects that a Microsoft HTML Application Host (HTA) is launching PowerShell commands.</span></span> <span data-ttu-id="0dd21-231">이 공격자가 toolaunch 악의적인 PowerShell 스크립트에서 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="0dd21-231">This is a technique used by attackers toolaunch malicious PowerShell scripts.</span></span>
 
<span data-ttu-id="0dd21-232">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-232">This is an example of this type of alert:</span></span>

![HTA 및 PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a><span data-ttu-id="0dd21-234">네트워크 분석</span><span class="sxs-lookup"><span data-stu-id="0dd21-234">Network analysis</span></span>
<span data-ttu-id="0dd21-235">Security Center 네트워크 위협 감지는 Azure IPFIX(인터넷 프로토콜 흐름 정보 내보내기)에서 보안 정보를 자동으로 수집하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-235">Security Center network threat detection works by automatically collecting security information from your Azure IPFIX (Internet Protocol Flow Information Export) traffic.</span></span> <span data-ttu-id="0dd21-236">이 정보를 종종 tooidentify 위협 여러 소스의 정보 상관 관계를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-236">It analyzes this information, often correlating information from multiple sources, tooidentify threats.</span></span>

### <a name="suspicious-outgoing-traffic-detected"></a><span data-ttu-id="0dd21-237">의심스러운 나가는 트래픽 감지</span><span class="sxs-lookup"><span data-stu-id="0dd21-237">Suspicious outgoing traffic detected</span></span>
<span data-ttu-id="0dd21-238">네트워크 장치 검색 및 많은 hello에서 프로 파일링 수 동일한 방식으로 다른 유형의 시스템.</span><span class="sxs-lookup"><span data-stu-id="0dd21-238">Network devices can be discovered and profiled in much hello same way as other types of systems.</span></span> <span data-ttu-id="0dd21-239">공격자는 일반적으로 포트 검색 또는 포트 비우기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-239">Attackers usually start with port scanning or port sweeping.</span></span> <span data-ttu-id="0dd21-240">Hello 다음 예제에서는 의심 스러운 SSH (보안 셸) 트래픽을 VM에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-240">In hello next example, you have suspicious Secure Shell (SSH) traffic from a VM.</span></span> <span data-ttu-id="0dd21-241">이 시나리오에서는 외부 리소스에 대한 SSH 무작위 공격 또는 포트 비우기 공격이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-241">In this scenario, SSH brute force or a port sweeping attack against an external resource is possible.</span></span>

![의심스러운 나가는 트래픽 경고](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

<span data-ttu-id="0dd21-243">이 경고는 사용할 수 있는 tooidentify hello 리소스의 사용된 tooinitiate이이 공격 하는 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-243">This alert gives information that you can use tooidentify hello resource that was used tooinitiate this attack.</span></span> <span data-ttu-id="0dd21-244">이 경고는 또한 tooidentify hello 손상 컴퓨터, hello 검색 시간 및 hello 프로토콜 및 포트에 사용 된 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-244">This alert also provides information tooidentify hello compromised machine, hello detection time, plus hello protocol and port that was used.</span></span> <span data-ttu-id="0dd21-245">이 블레이드 또한 있습니다 수 있는 수정 단계 목록을 사용 하는 toomitigate이이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-245">This blade also gives you a list of remediation steps that can be used toomitigate this issue.</span></span>

### <a name="network-communication-with-a-malicious-machine"></a><span data-ttu-id="0dd21-246">악의적인 컴퓨터와 네트워크 통신</span><span class="sxs-lookup"><span data-stu-id="0dd21-246">Network communication with a malicious machine</span></span>
<span data-ttu-id="0dd21-247">Azure Security Center는 Microsoft 위협 인텔리전스 피드를 활용하여 악성 IP 주소와 통신하는 손상된 컴퓨터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-247">By leveraging Microsoft threat intelligence feeds, Azure Security Center can detect compromised machines that communicate with malicious IP addresses.</span></span> <span data-ttu-id="0dd21-248">대부분의 경우에서 hello 악의적인 주소가 명령 및 제어 센터 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-248">In many cases, hello malicious address is a command and control center.</span></span> <span data-ttu-id="0dd21-249">이 경우 보안 센터 감지 hello 통신 조랑말 로더 맬웨어를 사용 하 여 수행 된 (라고도 [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).</span><span class="sxs-lookup"><span data-stu-id="0dd21-249">In this case, Security Center detected that hello communication was done by using Pony Loader malware (also known as [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).</span></span>

![네트워크 통신 경고](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

<span data-ttu-id="0dd21-251">이 경고를 사용 하는 tooinitiate tooidentify hello 리소스를 사용할 수 있는 정보를이 공격 제공, 리소스, hello 희생자 IP, hello 공격자가 IP 및 hello 검색 시간 hello 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-251">This alert gives information that enables you tooidentify hello resource that was used tooinitiate this attack, hello attacked resource, hello victim IP, hello attacker IP, and hello detection time.</span></span>

> [!NOTE]
> <span data-ttu-id="0dd21-252">라이브 IP 주소는 개인 정보 보호 목적을 위해 이 스크린샷에서 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-252">Live IP addresses were removed from this screenshot for privacy purpose.</span></span>
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a><span data-ttu-id="0dd21-253">가능한 발신 서비스 거부 공격 감지</span><span class="sxs-lookup"><span data-stu-id="0dd21-253">Possible outgoing denial-of-service attack detected</span></span>
<span data-ttu-id="0dd21-254">하나의 가상 컴퓨터에서 시작 된 비정상적인 네트워크 트래픽 보안 센터 tootrigger는 잠재적 서비스 거부 유형의 공격 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-254">Abnormal network traffic that originates from one virtual machine can cause Security Center tootrigger a potential denial-of-service type of attack.</span></span>

<span data-ttu-id="0dd21-255">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-255">This is an example of this type of alert:</span></span>

![발신 DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a><span data-ttu-id="0dd21-257">리소스 분석</span><span class="sxs-lookup"><span data-stu-id="0dd21-257">Resource analysis</span></span>
<span data-ttu-id="0dd21-258">보안 센터 리소스 분석에 중점을 두고 플랫폼 hello로 hello 통합 같은 서비스 (PaaS) 서비스로 [Azure SQL 데이터베이스 위협 검색](../sql-database/sql-database-threat-detection.md) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-258">Security Center resource analysis focuses on platform as a service (PaaS) services, such as hello integration with hello [Azure SQL Database threat detection](../sql-database/sql-database-threat-detection.md) feature.</span></span> <span data-ttu-id="0dd21-259">이러한 영역의 hello 분석 결과에 따라 보안 센터 리소스 관련 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-259">Based on hello analysis’s results from these areas, Security Center triggers a resource-related alert.</span></span>

### <a name="potential-sql-injection"></a><span data-ttu-id="0dd21-260">잠재적인 SQL 삽입</span><span class="sxs-lookup"><span data-stu-id="0dd21-260">Potential SQL injection</span></span>
<span data-ttu-id="0dd21-261">SQL 삽입은 악성 코드가 구문 분석 및 실행에 대 한 SQL Server 인스턴스의 tooan 나중 전달 되는 문자열은 삽입 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-261">SQL injection is an attack where malicious code is inserted into strings that are later passed tooan instance of SQL Server for parsing and execution.</span></span> <span data-ttu-id="0dd21-262">SQL Server가 수신하는 모든 구문상 유효한 쿼리를 실행하기 때문에 SQL 문을 생성하는 모든 프로시저에 삽입 취약성이 있는지 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-262">Because SQL Server executes all syntactically valid queries that it receives, any procedure that constructs SQL statements should be reviewed for injection vulnerabilities.</span></span> <span data-ttu-id="0dd21-263">기계 학습, 동작 분석 및 비정상 탐지 toodetermine 의심 스러운 이벤트 Azure SQL 데이터베이스의 현재 위치를 차지 하는 SQL 위협 검색을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-263">SQL Threat Detection uses machine learning, behavioral analysis, and anomaly detection toodetermine suspicious events that might be taking place in your Azure SQL databases.</span></span> <span data-ttu-id="0dd21-264">예:</span><span class="sxs-lookup"><span data-stu-id="0dd21-264">For example:</span></span>

* <span data-ttu-id="0dd21-265">이전 직원이 데이터베이스 액세스 시도</span><span class="sxs-lookup"><span data-stu-id="0dd21-265">Attempted database access by a former employee</span></span>
* <span data-ttu-id="0dd21-266">SQL 삽입 공격</span><span class="sxs-lookup"><span data-stu-id="0dd21-266">SQL injection attacks</span></span>
* <span data-ttu-id="0dd21-267">집에서 사용자 로부터 비정상적인 액세스 tooa 프로덕션 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="0dd21-267">Unusual access tooa production database from a user at home</span></span>

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

<span data-ttu-id="0dd21-269">이 경고의 hello 정보는 사용 되는 tooidentify 공격 hello 리소스, hello 검색 시간 및 hello 상태 hello 공격을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-269">hello information in this alert can be used tooidentify hello attacked resource, hello detection time, and hello state of hello attack.</span></span> <span data-ttu-id="0dd21-270">링크 toofurther 조사 단계도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-270">It also provides a link toofurther investigation steps.</span></span>

### <a name="vulnerability-toosql-injection"></a><span data-ttu-id="0dd21-271">취약점 tooSQL 삽입</span><span class="sxs-lookup"><span data-stu-id="0dd21-271">Vulnerability tooSQL Injection</span></span>
<span data-ttu-id="0dd21-272">데이터베이스에서 응용 프로그램 오류가 검색될 때 이 경고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-272">This alert is triggered when an application error is detected on a database.</span></span> <span data-ttu-id="0dd21-273">이 경고는 취약해 지지 tooSQL 주입 공격을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-273">This alert may indicate a possible vulnerability tooSQL injection attacks.</span></span>

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a><span data-ttu-id="0dd21-275">알 수 없는 위치에서 비정상적인 액세스</span><span class="sxs-lookup"><span data-stu-id="0dd21-275">Unusual access from unfamiliar location</span></span>
<span data-ttu-id="0dd21-276">이 경고는 액세스 이벤트 생소 한 IP 주소를 찾을 수 없으며 hello에서 마지막 기간은 hello 서버에서 검색 되었을 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-276">This alert is triggered when an access event from an unfamiliar IP address was detected on hello server, which was not seen in hello last period.</span></span>

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a><span data-ttu-id="0dd21-278">컨텍스트 정보</span><span class="sxs-lookup"><span data-stu-id="0dd21-278">Contextual information</span></span>
<span data-ttu-id="0dd21-279">한 조사 하는 동안 분석가 할 추가 컨텍스트 tooreach hello 위협의 hello 특성에 대 한 한 결과 방법을 toomitigate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-279">During an investigation, analysts need extra context tooreach a verdict about hello nature of hello threat and how toomitigate it.</span></span>  <span data-ttu-id="0dd21-280">예를 들어 네트워크 변칙 검색 되었지만 이해 하지 못하면 다른 일어나는 hello 네트워크 또는 관계의 대상 toohello 리소스와 그 다음 모든 하드 toounderstand 어떤 작업 tootake 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-280">For example, a network anomaly was detected, but without understanding what else is happening on hello network or with regard toohello targeted resource it is every hard toounderstand what actions tootake next.</span></span> <span data-ttu-id="0dd21-281">와 tooaid, 보안 문제가 발생 한 아티팩트, 관련된 이벤트 및 hello 에이전트용 유용한 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-281">tooaid with that, a Security Incident may include artifacts, related events and information that may help hello investigator.</span></span> <span data-ttu-id="0dd21-282">hello 추가 정보의 가용성에 따라 달라 집니다 위협이 검색 유형의 hello 및 hello 사용자 환경의 구성 되 고 모든 보안 문제에 대해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-282">hello availability of additional information will vary based on hello type of threat detected and hello configuration of your environment, and will not be available for all Security Incidents.</span></span>

<span data-ttu-id="0dd21-283">추가 정보를 사용할 수 있는 경우 경고의 hello 목록 아래의 hello 보안 사고에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-283">If additional information is available, it will be shown in hello Security Incident below hello list of alerts.</span></span> <span data-ttu-id="0dd21-284">이는 다음과 같은 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-284">This could contain information like:</span></span>

- <span data-ttu-id="0dd21-285">로그 지우기 이벤트</span><span class="sxs-lookup"><span data-stu-id="0dd21-285">Log clear events</span></span>
- <span data-ttu-id="0dd21-286">알 수 없는 장치에서 연결된 PNP 장치</span><span class="sxs-lookup"><span data-stu-id="0dd21-286">PNP device plugged from unknown device</span></span>
- <span data-ttu-id="0dd21-287">실행 가능하지 않은 경고</span><span class="sxs-lookup"><span data-stu-id="0dd21-287">Alerts which are not actionable</span></span> 

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a><span data-ttu-id="0dd21-289">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0dd21-289">See also</span></span>
<span data-ttu-id="0dd21-290">이 문서에서는 서로 다른 유형의 보안 센터에서 보안 경고를 hello에 대 한 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-290">In this article, you learned about hello different types of security alerts in Security Center.</span></span> <span data-ttu-id="0dd21-291">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-291">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="0dd21-292">Azure Security Center에서 보안 인시던트 처리</span><span class="sxs-lookup"><span data-stu-id="0dd21-292">Handling security incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="0dd21-293">Azure Security Center 감지 기능</span><span class="sxs-lookup"><span data-stu-id="0dd21-293">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="0dd21-294">Azure Security Center 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="0dd21-294">Azure Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="0dd21-295">[Azure 보안 센터 FAQ](security-center-faq.md): 찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-295">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="0dd21-296">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/): Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd21-296">[Azure security blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>
