---
title: "Azure Security Center에서 유형별 보안 경고 | Microsoft Docs"
description: "이 문서에서는 Azure Security Center에서 사용할 수 있는 다양한 종류의 보안 경고를 설명합니다."
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
ms.openlocfilehash: 19f71e0d5a8a4642b86ae60a3ab2a4042fa2990e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a><span data-ttu-id="b52a9-103">Azure Security Center에서 보안 경고 이해</span><span class="sxs-lookup"><span data-stu-id="b52a9-103">Understanding security alerts in Azure Security Center</span></span>
<span data-ttu-id="b52a9-104">이 문서를 통해 Azure Security Center에서 사용할 수 있는 다양한 유형의 보안 경고 및 관련된 정보를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-104">This article helps you to understand the different types of security alerts and related insights that are available in Azure Security Center.</span></span> <span data-ttu-id="b52a9-105">경고 및 인시던트를 관리하는 방법에 대한 자세한 내용은 [Azure Security Center에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52a9-105">For more information on how to manage alerts and incidents, see [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b52a9-106">고급 감지를 설정하려면 Azure Security Center 표준으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-106">To set up advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="b52a9-107">무료 60일 평가판을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-107">A free 60-day trial is available.</span></span> <span data-ttu-id="b52a9-108">업그레이드하려면 [보안 정책](security-center-policies.md)에서 **가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-108">To upgrade, select **Pricing Tier** in the [security policy](security-center-policies.md).</span></span> <span data-ttu-id="b52a9-109">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/security-center/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52a9-109">To learn more, see the [pricing page](https://azure.microsoft.com/pricing/details/security-center/).</span></span>
>

## <a name="what-type-of-alerts-are-available"></a><span data-ttu-id="b52a9-110">어떤 유형의 경고를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b52a9-110">What type of alerts are available?</span></span>
<span data-ttu-id="b52a9-111">Azure Security Center는 다양한 [검색 기능](security-center-detection-capabilities.md)을 사용하여 고객에게 환경을 대상으로 하는 잠재적인 공격에 대해 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-111">Azure Security Center uses a variety of [detection capabilities](security-center-detection-capabilities.md) to alert customers to potential attacks targeting their environments.</span></span> <span data-ttu-id="b52a9-112">이러한 경고는 트리거한 경고, 대상 리소스 및 공격의 출처에 대한 중요한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-112">These alerts contain valuable information about the what triggered the alert, the resources targeted, and the source of the attack.</span></span> <span data-ttu-id="b52a9-113">경고에 포함된 정보는 위협을 검색하는 데 사용되는 분석의 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-113">The information included in an alert varies based on the type of analytics used to detect the threat.</span></span> <span data-ttu-id="b52a9-114">인시던트는 위협을 조사할 때 유용할 수 있는 추가 컨텍스트 정보를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-114">Incidents may also contain additional contextual information that can be useful when investigating a threat.</span></span>  <span data-ttu-id="b52a9-115">이 문서는 다음 경고 유형에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-115">This article provides information about the following alert types:</span></span>

* <span data-ttu-id="b52a9-116">VMBA(가상 컴퓨터 동작 분석)</span><span class="sxs-lookup"><span data-stu-id="b52a9-116">Virtual Machine Behavioral Analysis (VMBA)</span></span>
* <span data-ttu-id="b52a9-117">네트워크 분석</span><span class="sxs-lookup"><span data-stu-id="b52a9-117">Network Analysis</span></span>
* <span data-ttu-id="b52a9-118">리소스 분석</span><span class="sxs-lookup"><span data-stu-id="b52a9-118">Resource Analysis</span></span>
* <span data-ttu-id="b52a9-119">컨텍스트 정보</span><span class="sxs-lookup"><span data-stu-id="b52a9-119">Contextual Information</span></span>

## <a name="virtual-machine-behavioral-analysis"></a><span data-ttu-id="b52a9-120">VMBA(가상 컴퓨터 동작 분석)</span><span class="sxs-lookup"><span data-stu-id="b52a9-120">Virtual machine behavioral analysis</span></span>
<span data-ttu-id="b52a9-121">Azure Security Center는 동작 분석을 사용하여 가상 컴퓨터 이벤트 로그의 분석에 따라 손상된 리소스를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-121">Azure Security Center can use behavioral analytics to identify compromised resources based on analysis of virtual machine event logs.</span></span> <span data-ttu-id="b52a9-122">예를 들어 프로세스 만들기 이벤트 및 로그인 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-122">For example, Process Creation Events and Login Events.</span></span> <span data-ttu-id="b52a9-123">또한 광범위한 캠페인의 증거 지원을 확인하는 다른 신호와의 상관 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-123">In addition, there is correlation with other signals to check for supporting evidence of a widespread campaign.</span></span>

> [!NOTE]
> <span data-ttu-id="b52a9-124">Security Center 감지 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 감지 기능](security-center-detection-capabilities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52a9-124">For more information on how Security Center detection capabilities work, see [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>
>

### <a name="crash-analysis"></a><span data-ttu-id="b52a9-125">충돌 분석</span><span class="sxs-lookup"><span data-stu-id="b52a9-125">Crash analysis</span></span>
<span data-ttu-id="b52a9-126">크래시 덤프 메모리 분석은 기존 보안 솔루션을 피할 수 있는 정교한 맬웨어를 감지하는 데 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-126">Crash dump memory analysis is a method used to detect sophisticated malware that is able to evade traditional security solutions.</span></span> <span data-ttu-id="b52a9-127">다양한 형식의 맬웨어는 디스크에 작성하지 않거나 디스크에 작성된 소프트웨어 구성 요소를 암호화하여 바이러스 백신 제품에서 탐지되지 않으려 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-127">Various forms of malware try to reduce the chance of being detected by antivirus products by never writing to disk, or by encrypting software components written to disk.</span></span> <span data-ttu-id="b52a9-128">따라서 맬웨어는 기존 맬웨어 방지 방법을 사용하여 감지하기 어렵게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-128">This makes the malware difficult to detect by using traditional antimalware approaches.</span></span> <span data-ttu-id="b52a9-129">그러나 이러한 종류의 맬웨어는 작동하기 위해 메모리에 추적을 남겨야 하므로 메모리 분석을 사용하여 검색될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-129">However, this kind of malware can be detected by using memory analysis, because malware must leave traces in memory in order to function.</span></span>

<span data-ttu-id="b52a9-130">소프트웨어가 충돌할 때 크래시 덤프는 충돌 시 메모리의 일부를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-130">When software crashes, a crash dump captures a portion of memory at the time of the crash.</span></span> <span data-ttu-id="b52a9-131">충돌은 맬웨어, 일반 응용 프로그램 또는 시스템 문제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-131">The crash may be caused by malware, general application or system issues.</span></span> <span data-ttu-id="b52a9-132">크래시 덤프의 메모리를 분석하여 Security Center는 소프트웨어에서 취약점을 악용하고 기밀 데이터에 액세스하고 손상된 컴퓨터에서 은밀하게 유지하는 데 사용되는 기술을 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-132">By analyzing the memory in the crash dump, Security Center can detect techniques used to exploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine.</span></span> <span data-ttu-id="b52a9-133">분석이 Security Center 백 엔드에 의해 수행되므로 호스트에 대한 최소 성능에 영향을 주게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-133">This is accomplished with minimum performance impact to hosts as the analysis is performed by the Security Center back end.</span></span>

<span data-ttu-id="b52a9-134">다음 필드는 이 문서의 뒷부분에 나타나는 크래시 덤프 경고 예제에 공통적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-134">The following fields are common to the crash dump alert examples that appear later in this article:</span></span>

* <span data-ttu-id="b52a9-135">DUMPFILE: 크래시 덤프 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-135">DUMPFILE: Name of the crash dump file.</span></span>
* <span data-ttu-id="b52a9-136">PROCESSNAME: 충돌하는 프로세스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-136">PROCESSNAME: Name of the crashing process.</span></span>
* <span data-ttu-id="b52a9-137">PROCESSVERSION: 충돌하는 프로세스의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-137">PROCESSVERSION: Version of the crashing process.</span></span>

### <a name="shellcode-discovered"></a><span data-ttu-id="b52a9-138">Shellcode 검색</span><span class="sxs-lookup"><span data-stu-id="b52a9-138">Shellcode discovered</span></span>
<span data-ttu-id="b52a9-139">Shellcode는 맬웨어가 소프트웨어 취약점을 악용한 후에 실행되는 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-139">Shellcode is the payload that is run after malware exploits a software vulnerability.</span></span> <span data-ttu-id="b52a9-140">이 경고는 크래시 덤프 분석이 악의적인 페이로드에서 일반적으로 수행되는 동작을 표시하는 실행 코드를 감지했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-140">This alert indicates that crash dump analysis has detected executable code that exhibits behavior that is commonly performed by malicious payloads.</span></span> <span data-ttu-id="b52a9-141">악의적이지 않은 소프트웨어가 이 동작을 수행할 수 있지만 보통 소프트웨어 개발 방법으로서는 일반적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-141">Although non-malicious software may perform this behavior, it is not typical of normal software development practices.</span></span>

<span data-ttu-id="b52a9-142">이 Shellcode 경고 예제는 다음과 같은 추가 필드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-142">The Shellcode alert example provides the following additional field:</span></span>

* <span data-ttu-id="b52a9-143">ADDRESS: shellcode의 메모리에 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-143">ADDRESS: The location in memory of the shellcode.</span></span>

<span data-ttu-id="b52a9-144">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-144">This is an example of this type of alert:</span></span>

![Shellcode 경고](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a><span data-ttu-id="b52a9-146">모듈 하이재킹 검색</span><span class="sxs-lookup"><span data-stu-id="b52a9-146">Module hijacking discovered</span></span>
<span data-ttu-id="b52a9-147">Windows는 DLL(동적 링크 라이브러리)을 사용하여 소프트웨어가 일반적인 Windows 시스템 기능을 활용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-147">Windows uses dynamic-link libraries (DLLs) to allow software to utilize common Windows system functionality.</span></span> <span data-ttu-id="b52a9-148">DLL 하이재킹은 맬웨어가 DLL 로드 순서를 변경시켜 악의적인 페이로드를 임의 코드를 실행할 수 있는 메모리에 로드할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-148">DLL Hijacking occurs when malware changes the DLL load order to load malicious payloads into memory, where arbitrary code can be executed.</span></span> <span data-ttu-id="b52a9-149">이 경고는 크래시 덤프 분석이 서로 다른 두 경로에서 로드되는 이름이 비슷한 모듈을 감지했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-149">This alert indicates that the crash dump analysis detected a similarly named module that is loaded from two different paths.</span></span> <span data-ttu-id="b52a9-150">로드된 경로 중 하나는 일반적인 Windows 시스템 이진 위치에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-150">One of the loaded paths comes from a common Windows system binary location.</span></span>

<span data-ttu-id="b52a9-151">합법적인 소프트웨어 개발자는 종종 Windows OS를 조율하고 확장하거나 Windows 응용 프로그램을 확장하는 등 악의적이지 않은 이유로 DLL 로드 순서를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-151">Legitimate software developers occasionally change the DLL load order for non-malicious reasons, such as instrumenting, extending the Windows OS, or extending a Windows application.</span></span> <span data-ttu-id="b52a9-152">DLL 로드 순서에 대한 악의적인 변경 내용과 잠재적으로 심각하지 않은 변경 내용을 구분하기 위해 Azure Security Center는 로드된 모듈이 의심스러운 프로필을 준수하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-152">To help differentiate between malicious and potentially benign changes to the DLL load order, Azure Security Center checks whether a loaded module conforms to a suspicious profile.</span></span> <span data-ttu-id="b52a9-153">이 검사의 결과는 경고의 "서명" 필드에 의해 나타나고 경고, 경고 설명 및 경고 문제 해결 단계의 심각도에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-153">The result of this check is indicated by the “SIGNATURE” field of the alert and is reflected in the severity of the alert, alert description, and alert remediation steps.</span></span> <span data-ttu-id="b52a9-154">모듈이 합법적이거나 악성 여부를 조사하려면 하이재킹 모듈의 온 디스크 복사본을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-154">To research whether the module is legitimate or malicious, analyze the on disk copy of the hijacking module.</span></span> <span data-ttu-id="b52a9-155">예를 들어 파일의 디지털 서명을 확인하거나 바이러스 백신 검사를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-155">For example, you can verify the file's digital signature, or run an antivirus scan.</span></span>

<span data-ttu-id="b52a9-156">이 경고는 이전의 "Shellcode 검색" 섹션에서 설명한 공통 필드 외에 다음과 같은 필드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-156">In addition to the common fields described in the earlier “Shellcode discovered” section, this alert provides the following fields:</span></span>

* <span data-ttu-id="b52a9-157">SIGNATURE: 하이재킹 모듈이 의심스러운 동작 프로필을 준수하는 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-157">SIGNATURE: Indicates if the hijacking module conforms to a suspicious behavior profile.</span></span>
* <span data-ttu-id="b52a9-158">HIJACKEDMODULE: 하이재킹된 Windows 시스템 모듈의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-158">HIJACKEDMODULE: The name of the hijacked Windows system module.</span></span>
* <span data-ttu-id="b52a9-159">HIJACKEDMODULEPATH: 하이재킹된 Windows 시스템 모듈의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-159">HIJACKEDMODULEPATH: The path of the hijacked Windows system module.</span></span>
* <span data-ttu-id="b52a9-160">HIJACKINGMODULEPATH: 하이재킹된 모듈의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-160">HIJACKINGMODULEPATH: The path of the hijacking module.</span></span>

<span data-ttu-id="b52a9-161">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-161">This is an example of this type of alert:</span></span>

![모듈 하이재킹 경고](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a><span data-ttu-id="b52a9-163">위장 Windows 모듈 감지</span><span class="sxs-lookup"><span data-stu-id="b52a9-163">Masquerading Windows module detected</span></span>
<span data-ttu-id="b52a9-164">맬웨어는 시스템 관리자로부터 악성 소프트웨어의 특성을 *섞고* 가리기 위해 Windows 시스템 이진 파일(예: SVCHOST.EXE) 또는 모듈(예: NTDLL.DLL)의 일반적인 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-164">Malware may use common names of Windows system binaries (for example, SVCHOST.EXE) or modules (for example, NTDLL.DLL) to *blend in* and obscure the nature of the malicious software from system administrators.</span></span> <span data-ttu-id="b52a9-165">이 경고는 크래시 덤프 파일이 Windows 시스템 모듈 이름을 사용하는 모듈을 포함하지만 Windows 모듈의 일반적인 다른 조건을 만족하지 않는다는 점을 크래시 덤프 분석에서 감지했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-165">This alert indicates that the crash dump analysis detects that the crash dump file contains modules that use Windows system module names, but do not satisfy other criteria that are typical of Windows modules.</span></span> <span data-ttu-id="b52a9-166">위장 모듈의 온 디스크 복사본에 대해 분석하면 이 모듈의 합법적인 또는 악의적인 특성에 대한 자세한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-166">Analyzing the on disk copy of the masquerading module may provide more information about the legitimate or malicious nature of this module.</span></span> <span data-ttu-id="b52a9-167">분석은 다음을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-167">Analysis may include:</span></span>

* <span data-ttu-id="b52a9-168">문제의 파일이 합법적인 소프트웨어 패키지의 일부로 제공되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-168">Confirm that the file in question is shipped as part of a legitimate software package.</span></span>
* <span data-ttu-id="b52a9-169">파일의 디지털 서명을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-169">Verify the file’s digital signature.</span></span>
* <span data-ttu-id="b52a9-170">파일에 대해 바이러스 백신 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-170">Run an antivirus scan on the file.</span></span>

<span data-ttu-id="b52a9-171">이 경고는 이전의 "Shellcode 검색" 섹션에서 설명한 공통 필드 외에 다음과 같은 추가 필드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-171">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span></span>

* <span data-ttu-id="b52a9-172">DETAILS: 모듈의 메타데이터가 유효한지와 모듈이 시스템 경로에서 로드되는지 여부를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-172">DETAILS: Describes whether the module's metadata is valid, and whether the module was loaded from a system path.</span></span>
* <span data-ttu-id="b52a9-173">NAME: 위장 Windows 모듈의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-173">NAME: The name of the masquerading Windows module.</span></span>
* <span data-ttu-id="b52a9-174">PATH: 위장 Windows 모듈의 경로</span><span class="sxs-lookup"><span data-stu-id="b52a9-174">PATH: The path to the masquerading Windows module.</span></span>

<span data-ttu-id="b52a9-175">또한 이 경고는 "CHECKSUM" 및 "TIMESTAMP"와 같은 모듈의 PE 헤더에서 특정 필드를 추출하고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-175">This alert also extracts and displays certain fields from the module’s PE header, such as “CHECKSUM” and “TIMESTAMP.”</span></span> <span data-ttu-id="b52a9-176">이러한 필드는 모듈에 있는 경우에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-176">These fields are only displayed if the fields are present in the module.</span></span> <span data-ttu-id="b52a9-177">이러한 필드에 대한 자세한 내용은 [Microsoft PE 및 COFF 사양](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52a9-177">See the [Microsoft PE and COFF Specification](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) for details on these fields.</span></span>

<span data-ttu-id="b52a9-178">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-178">This is an example of this type of alert:</span></span>

![가상 Windows 경고](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a><span data-ttu-id="b52a9-180">수정된 시스템 이진 파일 검색</span><span class="sxs-lookup"><span data-stu-id="b52a9-180">Modified system binary discovered</span></span>
<span data-ttu-id="b52a9-181">맬웨어는 은밀하게 데이터에 액세스하거나 손상된 시스템 상에 몰래 지속되기 위해 핵심 시스템 이진 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-181">Malware may modify core system binaries in order to covertly access data or surreptitiously persist on a compromised system.</span></span> <span data-ttu-id="b52a9-182">이 경고는 핵심 Windows OS 이진 파일이 메모리나 디스크에서 수정된 것을 크래시 덤프 분석에서 감지했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-182">This alert indicates that the crash dump analysis has detected that core Windows OS binaries have been modified in memory or on disk.</span></span>

<span data-ttu-id="b52a9-183">때때로 합법적인 소프트웨어 개발자는 Detours 등 응용 프로그램 호환성을 위해 악의적이지 않은 이유로 메모리에서 자유롭게 시스템 모듈을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-183">Legitimate software developers occasionally modify system modules in memory for non-malicious reasons, such as Detours or for application compatibility.</span></span> <span data-ttu-id="b52a9-184">악의적인 모듈과 잠재적으로 합법적인 모듈을 구분하기 위해 Azure Security Center는 수정된 모듈이 의심스러운 프로필을 준수하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-184">To help differentiate between malicious and potentially legitimate modules, Azure Security Center checks whether the modified module conforms to a suspicious profile.</span></span> <span data-ttu-id="b52a9-185">이 검사의 결과는 경고, 경고 설명 및 경고 문제 해결 단계의 심각도 별로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-185">The result of this check is indicated by the severity of the alert, alert description, and alert remediation steps.</span></span>

<span data-ttu-id="b52a9-186">이 경고는 이전의 "Shellcode 검색" 섹션에서 설명한 공통 필드 외에 다음과 같은 추가 필드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-186">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span></span>

* <span data-ttu-id="b52a9-187">MODULENAME: 수정된 시스템 이진 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-187">MODULENAME: Name of the modified system binary.</span></span>
* <span data-ttu-id="b52a9-188">MODULEVERSION: 수정된 시스템 이진 파일의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-188">MODULEVERSION: Version of the modified system binary.</span></span>

<span data-ttu-id="b52a9-189">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-189">This is an example of this type of alert:</span></span>

![시스템 이진 경고](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a><span data-ttu-id="b52a9-191">의심스러운 프로세스 실행</span><span class="sxs-lookup"><span data-stu-id="b52a9-191">Suspicious process executed</span></span>
<span data-ttu-id="b52a9-192">Security Center는 대상 가상 컴퓨터에서 실행되는 의심스러운 프로세스를 식별한 다음 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-192">Security Center identifies a suspicious process that runs on the target virtual machine, and then triggers an alert.</span></span> <span data-ttu-id="b52a9-193">검색은 특정 이름을 찾지 않지만 실행 파일의 매개 변수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-193">The detection doesn’t look for the specific name, but does look for the executable file's parameter.</span></span> <span data-ttu-id="b52a9-194">따라서 공격자가 실행 파일의 이름을 바꾸더라도 Security Center는 여전히 의심스러운 프로세스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-194">Therefore, even if the attacker renames the executable, Security Center can still detect the suspicious process.</span></span>

<span data-ttu-id="b52a9-195">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-195">This is an example of this type of alert:</span></span>

![의심스러운 프로세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a><span data-ttu-id="b52a9-197">여러 도메인 계정 쿼리</span><span class="sxs-lookup"><span data-stu-id="b52a9-197">Multiple domain accounts queried</span></span>
<span data-ttu-id="b52a9-198">Security Center는 Active Directory 도메인 계정을 쿼리하는 여러 시도를 감지할 수 있으며 이는 일반적으로 네트워크 정찰 중에 공격자에 의해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-198">Security Center can detect multiple attempts to query Active Directory domain accounts, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="b52a9-199">공격자는 이 기술을 활용하여 사용자를 식별하고 도메인 관리자 계정을 식별하고 도메인 컨트롤러인 컴퓨터를 식별하고 다른 도메인과 잠재적인 도메인 트러스트 관계가 있는지를 식별하는 도메인을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-199">Attackers can leverage this technique to query the domain to identify the users, identify the domain admin accounts, identify the computers that are domain controllers, and also identify the potential domain trust relationship with other domains.</span></span>

<span data-ttu-id="b52a9-200">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-200">This is an example of this type of alert:</span></span>

![여러 도메인 계정 경고](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a><span data-ttu-id="b52a9-202">로컬 관리자 그룹 구성원이 열거됨</span><span class="sxs-lookup"><span data-stu-id="b52a9-202">Local Administrators group members were enumerated</span></span>

<span data-ttu-id="b52a9-203">Security Center는 Windows Server 2016 및 Windows 10에서 보안 이벤트 4798이 트리거될 때 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-203">Security Center is going to trigger an alert when the security event 4798, in Windows Server 2016 and Windows 10, is trigged.</span></span> <span data-ttu-id="b52a9-204">로컬 관리자 그룹이 열거될 때 발생하며 이는 일반적으로 네트워크 정찰 중에 공격자에 의해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-204">This happens when local administrator groups are enumerated, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="b52a9-205">공격자는 이 기술을 활용하여 관리자 권한을 가진 사용자의 ID를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-205">Attackers can leverage this technique to query the identity of users with administrative privileges.</span></span>

<span data-ttu-id="b52a9-206">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-206">This is an example of this type of alert:</span></span>

![로컬 관리자](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a><span data-ttu-id="b52a9-208">대/소문자의 비정상적인 혼합</span><span class="sxs-lookup"><span data-stu-id="b52a9-208">Anomalous mix of upper and lower case characters</span></span>

<span data-ttu-id="b52a9-209">Security Center는 명령줄에서 대/소문자 혼합이 사용된 것을 감지하면 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-209">Security Center will trigger an alert when it detects the use of a mix of upper and lower case characters at the command line.</span></span> <span data-ttu-id="b52a9-210">일부 공격자는 이 기술을 사용하여 대/소문자 또는 해시 기반 컴퓨터 규칙을 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-210">Some attackers may use this technique to hide from case-sensitive or hash based machine rule.</span></span>

<span data-ttu-id="b52a9-211">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-211">This is an example of this type of alert:</span></span>

![비정상적인 혼합](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a><span data-ttu-id="b52a9-213">의심스러운 Kerberos Golden Ticket 공격</span><span class="sxs-lookup"><span data-stu-id="b52a9-213">Suspected Kerberos Golden Ticket attack</span></span>

<span data-ttu-id="b52a9-214">공격자는 Kerberos "Golden Ticket"을 만들기 위해 손상된 [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) 키를 사용하여 공격자가 원하는 사용자를 가장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-214">A compromised [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) key can be used by an attacker to create Kerberos "Golden Tickets," allowing the attacker to impersonate any user they wish.</span></span> <span data-ttu-id="b52a9-215">Security Center에서 이 활동 유형을 감지할 때 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-215">Security Center is going to trigger an alert when it detects this type of activity.</span></span>

> [!NOTE] 
> <span data-ttu-id="b52a9-216">Kerberos Golden Ticket에 대한 자세한 내용은 [Windows 10 자격 증명 도난 방지 가이드](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52a9-216">For more information about Kerberos Golden Ticket, read [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).</span></span>

<span data-ttu-id="b52a9-217">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-217">This is an example of this type of alert:</span></span>

![Golden ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a><span data-ttu-id="b52a9-219">의심스러운 계정 생성</span><span class="sxs-lookup"><span data-stu-id="b52a9-219">Suspicious account created</span></span>

<span data-ttu-id="b52a9-220">Security Center는 기존의 기본 제공 관리 권한 계정과 매우 유사한 계정을 만들 때 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-220">Security Center will trigger an alert when an account is created with close resemblance of an existing built in administrative privilege account.</span></span> <span data-ttu-id="b52a9-221">이 기술은 사용자 검증으로 알아 채지 못하도록 하기 위해 공격자가 악의적인 계정을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-221">This technique can be used by attackers to create a rogue account to avoid being noticed by human verification.</span></span>
 
<span data-ttu-id="b52a9-222">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-222">This is an example of this type of alert:</span></span>

![의심스러운 계정](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a><span data-ttu-id="b52a9-224">의심스러운 방화벽 규칙 생성됨</span><span class="sxs-lookup"><span data-stu-id="b52a9-224">Suspicious Firewall rule created</span></span>

<span data-ttu-id="b52a9-225">공격자는 악의적 응용 프로그램이 명령 및 컨트롤과 통신할 수 있도록 사용자 지정 방화벽 규칙을 만들어 호스트 보안을 우회하거나 손상된 호스트를 통해 네트워크로 공격을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-225">Attackers might try to circumvent host security by creating custom firewall rules to allow malicious applications to communicate with command and control, or to launch attacks through the network via the compromised host.</span></span> <span data-ttu-id="b52a9-226">Security Center는 의심스러운 위치의 실행 파일에서 새 방화벽 규칙이 생성된 것을 감지하면 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-226">Security Center will trigger an alert when it detects that a new firewall rule was created from an executable file in a suspicious location.</span></span>
 
<span data-ttu-id="b52a9-227">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-227">This is an example of this type of alert:</span></span>

![방화벽 규칙](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a><span data-ttu-id="b52a9-229">HTA 및 PowerShell의 의심스러운 조합</span><span class="sxs-lookup"><span data-stu-id="b52a9-229">Suspicious combination of HTA and PowerShell</span></span>

<span data-ttu-id="b52a9-230">Security Center는 Microsoft HTML Application Host(HTA)에서 PowerShell 명령이 실행되는 것을 감지하면 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-230">Security Center will trigger an alert when it detects that a Microsoft HTML Application Host (HTA) is launching PowerShell commands.</span></span> <span data-ttu-id="b52a9-231">공격자가 악의적인 PowerShell 스크립트를 실행하기 위해 사용하는 기법입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-231">This is a technique used by attackers to launch malicious PowerShell scripts.</span></span>
 
<span data-ttu-id="b52a9-232">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-232">This is an example of this type of alert:</span></span>

![HTA 및 PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a><span data-ttu-id="b52a9-234">네트워크 분석</span><span class="sxs-lookup"><span data-stu-id="b52a9-234">Network analysis</span></span>
<span data-ttu-id="b52a9-235">Security Center 네트워크 위협 감지는 Azure IPFIX(인터넷 프로토콜 흐름 정보 내보내기)에서 보안 정보를 자동으로 수집하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-235">Security Center network threat detection works by automatically collecting security information from your Azure IPFIX (Internet Protocol Flow Information Export) traffic.</span></span> <span data-ttu-id="b52a9-236">위협을 식별하도록 종종 여러 소스의 정보를 상호 연결하는 이 정보를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-236">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span>

### <a name="suspicious-outgoing-traffic-detected"></a><span data-ttu-id="b52a9-237">의심스러운 나가는 트래픽 감지</span><span class="sxs-lookup"><span data-stu-id="b52a9-237">Suspicious outgoing traffic detected</span></span>
<span data-ttu-id="b52a9-238">다른 유형의 시스템과 거의 동일한 방법으로 네트워크 장치를 검색하고 프로파일링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-238">Network devices can be discovered and profiled in much the same way as other types of systems.</span></span> <span data-ttu-id="b52a9-239">공격자는 일반적으로 포트 검색 또는 포트 비우기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-239">Attackers usually start with port scanning or port sweeping.</span></span> <span data-ttu-id="b52a9-240">다음 예제에서는 VM에서 의심스러운 SSH(Secure Shell) 트래픽을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-240">In the next example, you have suspicious Secure Shell (SSH) traffic from a VM.</span></span> <span data-ttu-id="b52a9-241">이 시나리오에서는 외부 리소스에 대한 SSH 무작위 공격 또는 포트 비우기 공격이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-241">In this scenario, SSH brute force or a port sweeping attack against an external resource is possible.</span></span>

![의심스러운 나가는 트래픽 경고](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

<span data-ttu-id="b52a9-243">이 경고는 이 공격을 시작하는 데 사용된 리소스를 식별하는 데 사용할 수 있는 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-243">This alert gives information that you can use to identify the resource that was used to initiate this attack.</span></span> <span data-ttu-id="b52a9-244">이 경고는 또한 손상된 컴퓨터, 검색 시간 및 사용된 프로토콜 및 포트를 식별하는 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-244">This alert also provides information to identify the compromised machine, the detection time, plus the protocol and port that was used.</span></span> <span data-ttu-id="b52a9-245">이 블레이드는 이 문제를 완화하기 위해 사용할 수 있는 수정 단계 목록도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-245">This blade also gives you a list of remediation steps that can be used to mitigate this issue.</span></span>

### <a name="network-communication-with-a-malicious-machine"></a><span data-ttu-id="b52a9-246">악의적인 컴퓨터와 네트워크 통신</span><span class="sxs-lookup"><span data-stu-id="b52a9-246">Network communication with a malicious machine</span></span>
<span data-ttu-id="b52a9-247">Azure Security Center는 Microsoft 위협 인텔리전스 피드를 활용하여 악성 IP 주소와 통신하는 손상된 컴퓨터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-247">By leveraging Microsoft threat intelligence feeds, Azure Security Center can detect compromised machines that communicate with malicious IP addresses.</span></span> <span data-ttu-id="b52a9-248">많은 경우 악성 주소는 명령 및 제어 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-248">In many cases, the malicious address is a command and control center.</span></span> <span data-ttu-id="b52a9-249">이 경우에 Security Center는 Pony Loader 맬웨어([Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)라고도 함)를 사용하여 실행된 통신을 감지했습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-249">In this case, Security Center detected that the communication was done by using Pony Loader malware (also known as [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).</span></span>

![네트워크 통신 경고](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

<span data-ttu-id="b52a9-251">이 경고는 이 공격을 시작하는 데 사용된 리소스, 공격을 받는 리소스, 공격 대상 IP, 공격자 IP 및 감지 시간을 식별할 수 있는 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-251">This alert gives information that enables you to identify the resource that was used to initiate this attack, the attacked resource, the victim IP, the attacker IP, and the detection time.</span></span>

> [!NOTE]
> <span data-ttu-id="b52a9-252">라이브 IP 주소는 개인 정보 보호 목적을 위해 이 스크린샷에서 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-252">Live IP addresses were removed from this screenshot for privacy purpose.</span></span>
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a><span data-ttu-id="b52a9-253">가능한 발신 서비스 거부 공격 감지</span><span class="sxs-lookup"><span data-stu-id="b52a9-253">Possible outgoing denial-of-service attack detected</span></span>
<span data-ttu-id="b52a9-254">하나의 가상 컴퓨터에서 발생하는 비정상적인 네트워크 트래픽으로 인해 Security Center에서 잠재적 서비스 거부 유형의 공격을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-254">Abnormal network traffic that originates from one virtual machine can cause Security Center to trigger a potential denial-of-service type of attack.</span></span>

<span data-ttu-id="b52a9-255">이러한 유형의 경고 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-255">This is an example of this type of alert:</span></span>

![발신 DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a><span data-ttu-id="b52a9-257">리소스 분석</span><span class="sxs-lookup"><span data-stu-id="b52a9-257">Resource analysis</span></span>
<span data-ttu-id="b52a9-258">Security Center 리소스 분석은 [Azure SQL Database 위협 요소 탐지](../sql-database/sql-database-threat-detection.md) 기능과의 통합 같은 PaaS(Platform as a Service) 서비스에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-258">Security Center resource analysis focuses on platform as a service (PaaS) services, such as the integration with the [Azure SQL Database threat detection](../sql-database/sql-database-threat-detection.md) feature.</span></span> <span data-ttu-id="b52a9-259">이러한 영역에서 분석의 결과에 따라 Security Center는 리소스 관련 경고를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-259">Based on the analysis’s results from these areas, Security Center triggers a resource-related alert.</span></span>

### <a name="potential-sql-injection"></a><span data-ttu-id="b52a9-260">잠재적인 SQL 삽입</span><span class="sxs-lookup"><span data-stu-id="b52a9-260">Potential SQL injection</span></span>
<span data-ttu-id="b52a9-261">SQL 삽입은 구문 분석 및 실행을 위해 나중에 SQL Server의 인스턴스로 전달된 문자열에 악성 코드를 삽입한 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-261">SQL injection is an attack where malicious code is inserted into strings that are later passed to an instance of SQL Server for parsing and execution.</span></span> <span data-ttu-id="b52a9-262">SQL Server가 수신하는 모든 구문상 유효한 쿼리를 실행하기 때문에 SQL 문을 생성하는 모든 프로시저에 삽입 취약성이 있는지 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-262">Because SQL Server executes all syntactically valid queries that it receives, any procedure that constructs SQL statements should be reviewed for injection vulnerabilities.</span></span> <span data-ttu-id="b52a9-263">SQL 위협 요소 탐지는 기계 학습, 동작 분석 및 이상 탐지를 사용하여 Azure SQL Databases에서 발생할 수 있는 의심스러운 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-263">SQL Threat Detection uses machine learning, behavioral analysis, and anomaly detection to determine suspicious events that might be taking place in your Azure SQL databases.</span></span> <span data-ttu-id="b52a9-264">예:</span><span class="sxs-lookup"><span data-stu-id="b52a9-264">For example:</span></span>

* <span data-ttu-id="b52a9-265">이전 직원이 데이터베이스 액세스 시도</span><span class="sxs-lookup"><span data-stu-id="b52a9-265">Attempted database access by a former employee</span></span>
* <span data-ttu-id="b52a9-266">SQL 삽입 공격</span><span class="sxs-lookup"><span data-stu-id="b52a9-266">SQL injection attacks</span></span>
* <span data-ttu-id="b52a9-267">집에 있는 사용자로부터 프로덕션 데이터베이스에 대한 비정상적인 액세스</span><span class="sxs-lookup"><span data-stu-id="b52a9-267">Unusual access to a production database from a user at home</span></span>

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

<span data-ttu-id="b52a9-269">공격을 받는 리소스, 감지 시간 및 공격의 상태를 식별하는 데 이 경고의 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-269">The information in this alert can be used to identify the attacked resource, the detection time, and the state of the attack.</span></span> <span data-ttu-id="b52a9-270">또한 추가 조사 단계에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-270">It also provides a link to further investigation steps.</span></span>

### <a name="vulnerability-to-sql-injection"></a><span data-ttu-id="b52a9-271">SQL 삽입에 대한 취약점</span><span class="sxs-lookup"><span data-stu-id="b52a9-271">Vulnerability to SQL Injection</span></span>
<span data-ttu-id="b52a9-272">데이터베이스에서 응용 프로그램 오류가 검색될 때 이 경고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-272">This alert is triggered when an application error is detected on a database.</span></span> <span data-ttu-id="b52a9-273">이 경고는 SQL 삽입 공격에 대한 가능한 취약점을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-273">This alert may indicate a possible vulnerability to SQL injection attacks.</span></span>

![잠재적인 SQL 삽입 경고](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a><span data-ttu-id="b52a9-275">알 수 없는 위치에서 비정상적인 액세스</span><span class="sxs-lookup"><span data-stu-id="b52a9-275">Unusual access from unfamiliar location</span></span>
<span data-ttu-id="b52a9-276">알 수 없는 IP 주소에서 액세스 이벤트가 서버에서 감지된 경우 이 경고가 트리거되며 이는 마지막 기간에서는 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-276">This alert is triggered when an access event from an unfamiliar IP address was detected on the server, which was not seen in the last period.</span></span>

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a><span data-ttu-id="b52a9-278">컨텍스트 정보</span><span class="sxs-lookup"><span data-stu-id="b52a9-278">Contextual information</span></span>
<span data-ttu-id="b52a9-279">조사 중 분석가는 위협의 원인 및 완화하는 방법에 대한 결과에 도달하기 위해 추가 컨텍스트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-279">During an investigation, analysts need extra context to reach a verdict about the nature of the threat and how to mitigate it.</span></span>  <span data-ttu-id="b52a9-280">예를 들어 네트워크가 변칙적으로 검색되었지만 네트워크에서 또는 대상 리소스와 관련하여 발생하는 다른 작업에 대한 이해 없이는 다음으로 수행할 작업을 이해하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-280">For example, a network anomaly was detected, but without understanding what else is happening on the network or with regard to the targeted resource it is every hard to understand what actions to take next.</span></span> <span data-ttu-id="b52a9-281">이를 방지하기 위해 보안 인시던트는 수집기에 도움을 줄 수 있는 아티팩트, 관련된 이벤트 및 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-281">To aid with that, a Security Incident may include artifacts, related events and information that may help the investigator.</span></span> <span data-ttu-id="b52a9-282">추가 정보의 가용성은 검색된 위협의 종류 및 사용자 환경의 구성에 따라 달라지며 모든 보안 인시던트에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-282">The availability of additional information will vary based on the type of threat detected and the configuration of your environment, and will not be available for all Security Incidents.</span></span>

<span data-ttu-id="b52a9-283">추가 정보를 사용할 수 있는 경우 경고 목록 아래의 보안 인시던트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-283">If additional information is available, it will be shown in the Security Incident below the list of alerts.</span></span> <span data-ttu-id="b52a9-284">이는 다음과 같은 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-284">This could contain information like:</span></span>

- <span data-ttu-id="b52a9-285">로그 지우기 이벤트</span><span class="sxs-lookup"><span data-stu-id="b52a9-285">Log clear events</span></span>
- <span data-ttu-id="b52a9-286">알 수 없는 장치에서 연결된 PNP 장치</span><span class="sxs-lookup"><span data-stu-id="b52a9-286">PNP device plugged from unknown device</span></span>
- <span data-ttu-id="b52a9-287">실행 가능하지 않은 경고</span><span class="sxs-lookup"><span data-stu-id="b52a9-287">Alerts which are not actionable</span></span> 

![비정상적인 액세스 경고](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a><span data-ttu-id="b52a9-289">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b52a9-289">See also</span></span>
<span data-ttu-id="b52a9-290">이 문서에서는 Security Center에서 발생하는 다양한 종류의 보안 경고에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-290">In this article, you learned about the different types of security alerts in Security Center.</span></span> <span data-ttu-id="b52a9-291">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52a9-291">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="b52a9-292">Azure Security Center에서 보안 인시던트 처리</span><span class="sxs-lookup"><span data-stu-id="b52a9-292">Handling security incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="b52a9-293">Azure Security Center 감지 기능</span><span class="sxs-lookup"><span data-stu-id="b52a9-293">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="b52a9-294">Azure Security Center 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="b52a9-294">Azure Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="b52a9-295">[Azure Security Center FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-295">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b52a9-296">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/): Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b52a9-296">[Azure security blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>
