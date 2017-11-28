---
title: "Azure AD Connect: 선언적 프로비전 식 | Microsoft Docs"
description: "Hello 선언적 프로비저닝 식에 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="4fe9d-103">Azure AD Connect 동기화: 선언적 프로비전 식 이해</span><span class="sxs-lookup"><span data-stu-id="4fe9d-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="4fe9d-104">Azure AD Connect 동기화는 Forefront Identity Manager 2010에 처음 도입된 선언적 프로비전을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="4fe9d-105">Tooimplement 허용 hello 필요 toowrite 없이 완전 한 id 통합 비즈니스 논리 컴파일된 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-105">It allows you tooimplement your complete identity integration business logic without hello need toowrite compiled code.</span></span>

<span data-ttu-id="4fe9d-106">선언적 프로비저닝의 핵심 부분은 특성 흐름에 사용 되는 hello 식 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-106">An essential part of declarative provisioning is hello expression language used in attribute flows.</span></span> <span data-ttu-id="4fe9d-107">사용 되는 hello 언어는 Microsoft® Visual Basic®에 대 한 VBA의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-107">hello language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="4fe9d-108">이 언어는 Microsoft Office에서 사용되며, VBScript 경험이 있는 사용자 또한 이 언어를 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="4fe9d-109">hello 선언적 프로비저닝 표현 언어는 함수만 사용 및 구조적 언어가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-109">hello Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="4fe9d-110">메서드 또는 문이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-110">There are no methods or statements.</span></span> <span data-ttu-id="4fe9d-111">함수는 중첩 대신 tooexpress 흐름을 프로그래밍 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-111">Functions are instead nested tooexpress program flow.</span></span>

<span data-ttu-id="4fe9d-112">자세한 내용은 참조 하십시오. [toohello Visual Basic for Applications 언어 참조 Office 2013에 대 한 시작](https://msdn.microsoft.com/library/gg264383.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-112">For more details, see [Welcome toohello Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="4fe9d-113">hello 특성은 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-113">hello attributes are strongly typed.</span></span> <span data-ttu-id="4fe9d-114">함수는 hello 올바른 형식의 특성만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-114">A function only accepts attributes of hello correct type.</span></span> <span data-ttu-id="4fe9d-115">대/소문자를 구분하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-115">It is also case-sensitive.</span></span> <span data-ttu-id="4fe9d-116">함수 이름과 특성 이름은 모두 적절한 대/소문자를 가지고 있어야 하며 그렇지 않으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="4fe9d-117">언어 정의 및 식별자</span><span class="sxs-lookup"><span data-stu-id="4fe9d-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="4fe9d-118">함수는 다음과 같이 이름 뒤에 대괄호로 인수가 붙습니다. FunctionName(인수 1, 인수 N).</span><span class="sxs-lookup"><span data-stu-id="4fe9d-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="4fe9d-119">특성은 다음과 같이 대괄호로 식별됩니다. [attributeName]</span><span class="sxs-lookup"><span data-stu-id="4fe9d-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="4fe9d-120">매개 변수는 다음과 같이 백분율 기호로 식별됩니다. % ParameterName %</span><span class="sxs-lookup"><span data-stu-id="4fe9d-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="4fe9d-121">문자열 상수는 따옴표를 사용합니다(예: "Contoso"). (참고: 둥근 따옴표 “”가 아닌 직선 따옴표 ""를 사용)</span><span class="sxs-lookup"><span data-stu-id="4fe9d-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="4fe9d-122">숫자 값은 10 진수 예상된 toobe 및 따옴표 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-122">Numeric values are expressed without quotes and expected toobe decimal.</span></span> <span data-ttu-id="4fe9d-123">16진수 값은 접두사 &H가 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="4fe9d-124">예: 98052, &HFF</span><span class="sxs-lookup"><span data-stu-id="4fe9d-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="4fe9d-125">부울 값은 다음과 같은 상수로 표시됩니다. True, False</span><span class="sxs-lookup"><span data-stu-id="4fe9d-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="4fe9d-126">기본 제공 상수 및 리터럴은 자신의 이름으로만 표현됩니다. NULL, CRLF, IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="4fe9d-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="4fe9d-127">함수</span><span class="sxs-lookup"><span data-stu-id="4fe9d-127">Functions</span></span>
<span data-ttu-id="4fe9d-128">선언적 프로비저닝이 많은 함수 tooenable hello 가능성 tootransform 특성 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-128">Declarative provisioning uses many functions tooenable hello possibility tootransform attribute values.</span></span> <span data-ttu-id="4fe9d-129">한 함수의 결과 hello tooanother 함수에 전달 되는 하므로 이러한 함수를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-129">These functions can be nested so hello result from one function is passed in tooanother function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="4fe9d-130">hello에 hello 전체 함수 목록은 있습니다 [함수 참조](active-directory-aadconnectsync-functions-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-130">hello complete list of functions can be found in hello [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="4fe9d-131">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4fe9d-131">Parameters</span></span>
<span data-ttu-id="4fe9d-132">매개 변수는 커넥터를 통해 또는 PowerShell을 사용하는 관리자에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="4fe9d-133">Hello 도메인 hello 사용자의 hello 이름에 있는 예를 들어와 매개 변수는 일반적으로 시스템 toosystem에서 다른 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-133">Parameters usually contain values that are different from system toosystem, for example hello name of hello domain hello user is located in.</span></span> <span data-ttu-id="4fe9d-134">이러한 매개 변수를 특성 흐름에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="4fe9d-135">인바운드 동기화 규칙에 대 한 매개 변수 뒤 Active Directory Connector 제공 된 hello을 hello:</span><span class="sxs-lookup"><span data-stu-id="4fe9d-135">hello Active Directory Connector provided hello following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="4fe9d-136">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="4fe9d-136">Parameter Name</span></span> | <span data-ttu-id="4fe9d-137">주석</span><span class="sxs-lookup"><span data-stu-id="4fe9d-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="4fe9d-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="4fe9d-138">Domain.Netbios</span></span> |<span data-ttu-id="4fe9d-139">Netbios 형식의 hello 도메인 현재 가져오기 예를 들어 FABRIKAMSALES</span><span class="sxs-lookup"><span data-stu-id="4fe9d-139">Netbios format of hello domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="4fe9d-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="4fe9d-140">Domain.FQDN</span></span> |<span data-ttu-id="4fe9d-141">Hello 도메인 현재 가져오기 예를 들어 sales.fabrikam.com의 FQDN 형식</span><span class="sxs-lookup"><span data-stu-id="4fe9d-141">FQDN format of hello domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="4fe9d-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="4fe9d-142">Domain.LDAP</span></span> |<span data-ttu-id="4fe9d-143">Hello 도메인 현재 가져오기 예를 들어 DC의 LDAP 형식을 판매, DC = = fabrikam, DC = com</span><span class="sxs-lookup"><span data-stu-id="4fe9d-143">LDAP format of hello domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="4fe9d-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="4fe9d-144">Forest.Netbios</span></span> |<span data-ttu-id="4fe9d-145">Hello 포리스트 이름 현재 가져오기 예를 들어 FABRIKAMCORP Netbios 형식</span><span class="sxs-lookup"><span data-stu-id="4fe9d-145">Netbios format of hello forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="4fe9d-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="4fe9d-146">Forest.FQDN</span></span> |<span data-ttu-id="4fe9d-147">Hello 포리스트 이름 현재 가져오기 예를 들어 fabrikam.com FQDN 형식</span><span class="sxs-lookup"><span data-stu-id="4fe9d-147">FQDN format of hello forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="4fe9d-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="4fe9d-148">Forest.LDAP</span></span> |<span data-ttu-id="4fe9d-149">LDAP 이름의 형식이 hello 포리스트 현재 가져오기 예를 들어 DC = fabrikam, DC = com</span><span class="sxs-lookup"><span data-stu-id="4fe9d-149">LDAP format of hello forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="4fe9d-150">hello 시스템 제공 hello 매개 변수를 다음 실행 되는 hello 커넥터의 hello 식별자를 사용 하는 tooget 현재:</span><span class="sxs-lookup"><span data-stu-id="4fe9d-150">hello system provides hello following parameter, which is used tooget hello identifier of hello Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="4fe9d-151">Hello 사용자가 있는 hello 도메인의 netbios 이름 hello 사용 하 여 hello 메타 버스 특성 도메인을 채우는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-151">Here is an example that populates hello metaverse attribute domain with hello netbios name of hello domain where hello user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="4fe9d-152">연산자</span><span class="sxs-lookup"><span data-stu-id="4fe9d-152">Operators</span></span>
<span data-ttu-id="4fe9d-153">hello 다음 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-153">hello following operators can be used:</span></span>

* <span data-ttu-id="4fe9d-154">**비교**: <, <=, <>, =, >, >=</span><span class="sxs-lookup"><span data-stu-id="4fe9d-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="4fe9d-155">**수학**: +, -, \*, -</span><span class="sxs-lookup"><span data-stu-id="4fe9d-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="4fe9d-156">**문자열**: &(연결)</span><span class="sxs-lookup"><span data-stu-id="4fe9d-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="4fe9d-157">**논리**: &&(및), ||(또는)</span><span class="sxs-lookup"><span data-stu-id="4fe9d-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="4fe9d-158">**계산 순서**: ( )</span><span class="sxs-lookup"><span data-stu-id="4fe9d-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="4fe9d-159">연산자는 왼쪽된 tooright 평가 하며 hello 동일한 평가 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-159">Operators are evaluated left tooright and have hello same evaluation priority.</span></span> <span data-ttu-id="4fe9d-160">즉, hello \* (승수) 하기 전에-(빼기) 계산 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-160">That is, hello \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="4fe9d-161">2\*(5 + 3) 하지 2로 동일 hello은\*5 + 3입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-161">2\*(5+3) is not hello same as 2\*5+3.</span></span> <span data-ttu-id="4fe9d-162">hello 괄호 () 사용 되 toochange hello 평가 순서 두면 tooright 평가 순서 적절 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-162">hello brackets ( ) are used toochange hello evaluation order when left tooright evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="4fe9d-163">다중값 특성</span><span class="sxs-lookup"><span data-stu-id="4fe9d-163">Multi-valued attributes</span></span>
<span data-ttu-id="4fe9d-164">hello 함수는 단일 값 및 다중값 특성에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-164">hello functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="4fe9d-165">다중 값된 특성에 대 한 hello 모든 값에 대해 작동 하 고 적용 합니다 hello tooevery 값 함수 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-165">For multi-valued attributes, hello function operates over every value and applies hello same function tooevery value.</span></span>

<span data-ttu-id="4fe9d-166">예:</span><span class="sxs-lookup"><span data-stu-id="4fe9d-166">For example:</span></span>  
<span data-ttu-id="4fe9d-167">`Trim([proxyAddresses])`Hello / / proxyAddress 특성의 각 값의 Trim을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-167">`Trim([proxyAddresses])` Do a Trim of every value in hello proxyAddress attribute.</span></span>  
<span data-ttu-id="4fe9d-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`와 모든 값에 대해는 @-sign, 대체 hello 도메인을 @contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace hello domain with @contoso.com.</span></span>  
<span data-ttu-id="4fe9d-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Hello SIP 주소 찾아서 hello 값에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for hello SIP-address and remove it from hello values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fe9d-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4fe9d-170">Next steps</span></span>
* <span data-ttu-id="4fe9d-171">Hello 구성 모델에 대해 자세히 읽어보세요 [이해 선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-171">Read more about hello configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="4fe9d-172">참조 방식을 선언적 사용된의 기본의 프로 비전은 [hello 기본 구성 이해](active-directory-aadconnectsync-understanding-default-configuration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-172">See how declarative provisioning is used out-of-box in [Understanding hello default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="4fe9d-173">선언적 프로비저닝을 사용 하 여 실제 toomake을 변경 하는 방법을 확인할 [어떻게 변경 toohello toomake 기본 구성을](active-directory-aadconnectsync-change-the-configuration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe9d-173">See how toomake a practical change using declarative provisioning in [How toomake a change toohello default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="4fe9d-174">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="4fe9d-174">**Overview topics**</span></span>

* [<span data-ttu-id="4fe9d-175">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4fe9d-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4fe9d-176">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="4fe9d-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="4fe9d-177">**참조 항목**</span><span class="sxs-lookup"><span data-stu-id="4fe9d-177">**Reference topics**</span></span>

* [<span data-ttu-id="4fe9d-178">Azure AD 동기화 연결: 함수 참조</span><span class="sxs-lookup"><span data-stu-id="4fe9d-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)

