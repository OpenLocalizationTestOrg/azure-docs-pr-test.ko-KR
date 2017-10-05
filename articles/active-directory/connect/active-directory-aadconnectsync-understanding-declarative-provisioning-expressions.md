---
title: "Azure AD Connect: 선언적 프로비전 식 | Microsoft Docs"
description: "선언적 프로비전 식에 대해 설명합니다."
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
ms.openlocfilehash: e3a03a97b10e04fb85261620879b2102e1db8465
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="98915-103">Azure AD Connect 동기화: 선언적 프로비전 식 이해</span><span class="sxs-lookup"><span data-stu-id="98915-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="98915-104">Azure AD Connect 동기화는 Forefront Identity Manager 2010에 처음 도입된 선언적 프로비전을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="98915-105">컴파일된 코드를 작성할 필요 없이 전체 ID 통합 비즈니스 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-105">It allows you to implement your complete identity integration business logic without the need to write compiled code.</span></span>

<span data-ttu-id="98915-106">선언적 프로비전의 핵심적인 부분은 특성 흐름에 사용되는 표현 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="98915-106">An essential part of declarative provisioning is the expression language used in attribute flows.</span></span> <span data-ttu-id="98915-107">사용 되는 언어는 VBA(Microsoft® Visual Basic® for Applications)의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="98915-107">The language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="98915-108">이 언어는 Microsoft Office에서 사용되며, VBScript 경험이 있는 사용자 또한 이 언어를 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="98915-109">선언적 프로비전 표현 언어는 함수만 사용하며 구조적 언어는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="98915-109">The Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="98915-110">메서드 또는 문이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-110">There are no methods or statements.</span></span> <span data-ttu-id="98915-111">대신, 빠른 프로그램 흐름에 함수가 중첩됩니다.</span><span class="sxs-lookup"><span data-stu-id="98915-111">Functions are instead nested to express program flow.</span></span>

<span data-ttu-id="98915-112">자세한 내용은 [Office 2013용 Visual Basic for Applications 언어 참조 시작](https://msdn.microsoft.com/library/gg264383.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98915-112">For more details, see [Welcome to the Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="98915-113">특성은 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="98915-113">The attributes are strongly typed.</span></span> <span data-ttu-id="98915-114">함수는 올바른 형식의 특성만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-114">A function only accepts attributes of the correct type.</span></span> <span data-ttu-id="98915-115">대/소문자를 구분하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-115">It is also case-sensitive.</span></span> <span data-ttu-id="98915-116">함수 이름과 특성 이름은 모두 적절한 대/소문자를 가지고 있어야 하며 그렇지 않으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="98915-117">언어 정의 및 식별자</span><span class="sxs-lookup"><span data-stu-id="98915-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="98915-118">함수는 다음과 같이 이름 뒤에 대괄호로 인수가 붙습니다. FunctionName(인수 1, 인수 N).</span><span class="sxs-lookup"><span data-stu-id="98915-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="98915-119">특성은 다음과 같이 대괄호로 식별됩니다. [attributeName]</span><span class="sxs-lookup"><span data-stu-id="98915-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="98915-120">매개 변수는 다음과 같이 백분율 기호로 식별됩니다. % ParameterName %</span><span class="sxs-lookup"><span data-stu-id="98915-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="98915-121">문자열 상수는 따옴표를 사용합니다(예: "Contoso"). (참고: 둥근 따옴표 “”가 아닌 직선 따옴표 ""를 사용)</span><span class="sxs-lookup"><span data-stu-id="98915-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="98915-122">숫자 값은 따옴표 없이 표현되고 10진수입니다.</span><span class="sxs-lookup"><span data-stu-id="98915-122">Numeric values are expressed without quotes and expected to be decimal.</span></span> <span data-ttu-id="98915-123">16진수 값은 접두사 &H가 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="98915-124">예: 98052, &HFF</span><span class="sxs-lookup"><span data-stu-id="98915-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="98915-125">부울 값은 다음과 같은 상수로 표시됩니다. True, False</span><span class="sxs-lookup"><span data-stu-id="98915-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="98915-126">기본 제공 상수 및 리터럴은 자신의 이름으로만 표현됩니다. NULL, CRLF, IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="98915-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="98915-127">함수</span><span class="sxs-lookup"><span data-stu-id="98915-127">Functions</span></span>
<span data-ttu-id="98915-128">선언적 프로비전은 여러 함수를 사용하여 특성 값을 변환할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-128">Declarative provisioning uses many functions to enable the possibility to transform attribute values.</span></span> <span data-ttu-id="98915-129">함수의 결과가 다른 함수로 전달되도록 이러한 함수는 중첩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-129">These functions can be nested so the result from one function is passed in to another function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="98915-130">전체 함수 목록은 [함수 참조](active-directory-aadconnectsync-functions-reference.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-130">The complete list of functions can be found in the [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="98915-131">매개 변수</span><span class="sxs-lookup"><span data-stu-id="98915-131">Parameters</span></span>
<span data-ttu-id="98915-132">매개 변수는 커넥터를 통해 또는 PowerShell을 사용하는 관리자에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="98915-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="98915-133">매개 변수는 일반적으로 시스템별로 다른 값을 포함합니다(예: 사용자가 위치한 도메인 이름).</span><span class="sxs-lookup"><span data-stu-id="98915-133">Parameters usually contain values that are different from system to system, for example the name of the domain the user is located in.</span></span> <span data-ttu-id="98915-134">이러한 매개 변수를 특성 흐름에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="98915-135">Active Directory Connector는 인바운드 동기화 규칙에 대해 다음 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-135">The Active Directory Connector provided the following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="98915-136">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="98915-136">Parameter Name</span></span> | <span data-ttu-id="98915-137">주석</span><span class="sxs-lookup"><span data-stu-id="98915-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="98915-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="98915-138">Domain.Netbios</span></span> |<span data-ttu-id="98915-139">현재 가져오는 도메인의 Netbios 형식(예: FABRIKAMSALES)</span><span class="sxs-lookup"><span data-stu-id="98915-139">Netbios format of the domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="98915-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="98915-140">Domain.FQDN</span></span> |<span data-ttu-id="98915-141">현재 가져오는 도메인의 FQDN 형식(예: sales.fabrikam.com)</span><span class="sxs-lookup"><span data-stu-id="98915-141">FQDN format of the domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="98915-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="98915-142">Domain.LDAP</span></span> |<span data-ttu-id="98915-143">현재 가져오는 도메인의 LDAP 형식(예: DC=sales,DC=fabrikam,DC=com)</span><span class="sxs-lookup"><span data-stu-id="98915-143">LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="98915-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="98915-144">Forest.Netbios</span></span> |<span data-ttu-id="98915-145">현재 가져오는 포리스트 이름의 Netbios 형식(예: FABRIKAMCORP)</span><span class="sxs-lookup"><span data-stu-id="98915-145">Netbios format of the forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="98915-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="98915-146">Forest.FQDN</span></span> |<span data-ttu-id="98915-147">현재 가져오는 포리스트 이름의 FQDN 형식(예: fabrikam.com)</span><span class="sxs-lookup"><span data-stu-id="98915-147">FQDN format of the forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="98915-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="98915-148">Forest.LDAP</span></span> |<span data-ttu-id="98915-149">현재 가져오는 포리스트 이름의 LDAP 형식(예: DC=fabrikam,DC=com)</span><span class="sxs-lookup"><span data-stu-id="98915-149">LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="98915-150">시스템은 현재 실행 중인 커넥터의 ID를 가져오는 데 사용되는 다음 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-150">The system provides the following parameter, which is used to get the identifier of the Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="98915-151">사용자가 위치한 도메인의 netbios 이름이 있는 메타버스 특성 도메인으로 채워지는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-151">Here is an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="98915-152">연산자</span><span class="sxs-lookup"><span data-stu-id="98915-152">Operators</span></span>
<span data-ttu-id="98915-153">다음과 같은 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-153">The following operators can be used:</span></span>

* <span data-ttu-id="98915-154">**비교**: <, <=, <>, =, >, >=</span><span class="sxs-lookup"><span data-stu-id="98915-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="98915-155">**수학**: +, -, \*, -</span><span class="sxs-lookup"><span data-stu-id="98915-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="98915-156">**문자열**: &(연결)</span><span class="sxs-lookup"><span data-stu-id="98915-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="98915-157">**논리**: &&(및), ||(또는)</span><span class="sxs-lookup"><span data-stu-id="98915-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="98915-158">**계산 순서**: ( )</span><span class="sxs-lookup"><span data-stu-id="98915-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="98915-159">연산자는 왼쪽에서 오른쪽으로 계산되며 계산 우선 순위가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-159">Operators are evaluated left to right and have the same evaluation priority.</span></span> <span data-ttu-id="98915-160">즉, \*(승수)는 -(빼기) 전에 계산되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-160">That is, the \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="98915-161">2\*(5+3)은 2\*5+3과 같지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-161">2\*(5+3) is not the same as 2\*5+3.</span></span> <span data-ttu-id="98915-162">대괄호 ()는 왼쪽에서 오른쪽 계산 순서가 적절하지 않을 때 계산 순서를 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98915-162">The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="98915-163">다중값 특성</span><span class="sxs-lookup"><span data-stu-id="98915-163">Multi-valued attributes</span></span>
<span data-ttu-id="98915-164">함수는 단일 값 및 다중값 특성에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98915-164">The functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="98915-165">다중값 특성의 경우 함수는 모든 값에 대해 작동하고 각 값에 동일한 함수를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-165">For multi-valued attributes, the function operates over every value and applies the same function to every value.</span></span>

<span data-ttu-id="98915-166">예를 들어 </span><span class="sxs-lookup"><span data-stu-id="98915-166">For example:</span></span>  
<span data-ttu-id="98915-167">`Trim([proxyAddresses])` proxyAddress 특성의 모든 값에 Trim을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-167">`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.</span></span>  
<span data-ttu-id="98915-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`와 모든 값에 대해는 @-sign, 대체 사용 하 여 도메인 @contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.</span></span>  
<span data-ttu-id="98915-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` SIP 주소를 찾아서 값을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="98915-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98915-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98915-170">Next steps</span></span>
* <span data-ttu-id="98915-171">[선언적 프로비전 이해](active-directory-aadconnectsync-understanding-declarative-provisioning.md)에서 구성 모델에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="98915-171">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="98915-172">[기본 구성 이해](active-directory-aadconnectsync-understanding-default-configuration.md)에서 선언적 프로비전이 기본으로 사용되는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98915-172">See how declarative provisioning is used out-of-box in [Understanding the default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="98915-173">[기본 구성으로 변경하는 방법](active-directory-aadconnectsync-change-the-configuration.md)에서 선언적 프로비전을 사용하여 실용적으로 변경하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98915-173">See how to make a practical change using declarative provisioning in [How to make a change to the default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="98915-174">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="98915-174">**Overview topics**</span></span>

* [<span data-ttu-id="98915-175">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="98915-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="98915-176">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="98915-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="98915-177">**참조 항목**</span><span class="sxs-lookup"><span data-stu-id="98915-177">**Reference topics**</span></span>

* [<span data-ttu-id="98915-178">Azure AD 동기화 연결: 함수 참조</span><span class="sxs-lookup"><span data-stu-id="98915-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)

