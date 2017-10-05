---
title: "Azure AD 동기화 연결: 함수 참조 | Microsoft Docs"
description: "Azure AD Connect 동기화의 선언적 프로비전 식을 참조하세요."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="d534a-103">Azure AD 동기화 연결: 함수 참조</span><span class="sxs-lookup"><span data-stu-id="d534a-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="d534a-104">Azure AD Connect에서 동기화 중에 특성 값을 조작하려면 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="d534a-105">함수의 구문은 다음 형식을 사용하여 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="d534a-106">함수가 과부하되거나 여러 구문을 허용한 경우, 모든 사용한 구문의 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="d534a-107">함수는 강력한 형식이며, 일치하는 문서 형식 안에 들어가는 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="d534a-108">형식이 일치하지 않는 경우 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="d534a-109">형식은 다음 구문을 사용하여 표현합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="d534a-110">**bin** -이진</span><span class="sxs-lookup"><span data-stu-id="d534a-110">**bin** – Binary</span></span>
* <span data-ttu-id="d534a-111">**bool** -부울</span><span class="sxs-lookup"><span data-stu-id="d534a-111">**bool** – Boolean</span></span>
* <span data-ttu-id="d534a-112">**dt** – UTC 날짜/시간</span><span class="sxs-lookup"><span data-stu-id="d534a-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="d534a-113">**enum** – 알려진 상수의 열거형</span><span class="sxs-lookup"><span data-stu-id="d534a-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="d534a-114">**exp** – 부울로 계산이 예상되는 식</span><span class="sxs-lookup"><span data-stu-id="d534a-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="d534a-115">**mvbin** – 다중값의 이진</span><span class="sxs-lookup"><span data-stu-id="d534a-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="d534a-116">**mvstr** – 다중 값 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="d534a-117">**mvref** – 다중 값 참조</span><span class="sxs-lookup"><span data-stu-id="d534a-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="d534a-118">**num** – 숫자</span><span class="sxs-lookup"><span data-stu-id="d534a-118">**num** – Numeric</span></span>
* <span data-ttu-id="d534a-119">**ref** – 참조</span><span class="sxs-lookup"><span data-stu-id="d534a-119">**ref** – Reference</span></span>
* <span data-ttu-id="d534a-120">**str** - 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-120">**str** – String</span></span>
* <span data-ttu-id="d534a-121">**var** – 거의 모든 다른 형식의 변수</span><span class="sxs-lookup"><span data-stu-id="d534a-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="d534a-122">**void** – 값을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="d534a-123">**mvbin**, **mvstr** 및 **mvref** 형식을 포함하는 함수는 다중값 특성에서만 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="d534a-124">**bin**, **str** 및 **ref**를 포함한 함수는 단일값 및 다중값 특성에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="d534a-125">함수 참조</span><span class="sxs-lookup"><span data-stu-id="d534a-125">Functions Reference</span></span>
| <span data-ttu-id="d534a-126">함수 목록</span><span class="sxs-lookup"><span data-stu-id="d534a-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d534a-127">**인증서**</span><span class="sxs-lookup"><span data-stu-id="d534a-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="d534a-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="d534a-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="d534a-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="d534a-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="d534a-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="d534a-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="d534a-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="d534a-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="d534a-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="d534a-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="d534a-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="d534a-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="d534a-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="d534a-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="d534a-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="d534a-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="d534a-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="d534a-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="d534a-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="d534a-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="d534a-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="d534a-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="d534a-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="d534a-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="d534a-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="d534a-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="d534a-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="d534a-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="d534a-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="d534a-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="d534a-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="d534a-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="d534a-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="d534a-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="d534a-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="d534a-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="d534a-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="d534a-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="d534a-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="d534a-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="d534a-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="d534a-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="d534a-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="d534a-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="d534a-150">**변환**</span><span class="sxs-lookup"><span data-stu-id="d534a-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="d534a-151">CBool</span><span class="sxs-lookup"><span data-stu-id="d534a-151">CBool</span></span>](#cbool) |[<span data-ttu-id="d534a-152">CDate</span><span class="sxs-lookup"><span data-stu-id="d534a-152">CDate</span></span>](#cdate) |[<span data-ttu-id="d534a-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="d534a-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="d534a-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="d534a-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="d534a-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="d534a-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="d534a-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d534a-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="d534a-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d534a-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="d534a-158">CNum</span><span class="sxs-lookup"><span data-stu-id="d534a-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="d534a-159">CRef</span><span class="sxs-lookup"><span data-stu-id="d534a-159">CRef</span></span>](#cref) |[<span data-ttu-id="d534a-160">CStr</span><span class="sxs-lookup"><span data-stu-id="d534a-160">CStr</span></span>](#cstr) |[<span data-ttu-id="d534a-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="d534a-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="d534a-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="d534a-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="d534a-163">**Date / Time**</span><span class="sxs-lookup"><span data-stu-id="d534a-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="d534a-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="d534a-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="d534a-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="d534a-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="d534a-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="d534a-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="d534a-167">Now</span><span class="sxs-lookup"><span data-stu-id="d534a-167">Now</span></span>](#now) | |
| [<span data-ttu-id="d534a-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="d534a-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="d534a-169">**디렉터리**</span><span class="sxs-lookup"><span data-stu-id="d534a-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="d534a-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="d534a-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="d534a-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="d534a-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="d534a-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="d534a-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="d534a-173">**평가**</span><span class="sxs-lookup"><span data-stu-id="d534a-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="d534a-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="d534a-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="d534a-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="d534a-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="d534a-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="d534a-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="d534a-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="d534a-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="d534a-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="d534a-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="d534a-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="d534a-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="d534a-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="d534a-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="d534a-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="d534a-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="d534a-182">IsString</span><span class="sxs-lookup"><span data-stu-id="d534a-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="d534a-183">**Math**</span><span class="sxs-lookup"><span data-stu-id="d534a-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="d534a-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="d534a-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="d534a-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="d534a-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="d534a-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="d534a-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="d534a-187">**다중값**</span><span class="sxs-lookup"><span data-stu-id="d534a-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="d534a-188">포함</span><span class="sxs-lookup"><span data-stu-id="d534a-188">Contains</span></span>](#contains) |[<span data-ttu-id="d534a-189">개수</span><span class="sxs-lookup"><span data-stu-id="d534a-189">Count</span></span>](#count) |[<span data-ttu-id="d534a-190">항목</span><span class="sxs-lookup"><span data-stu-id="d534a-190">Item</span></span>](#item) |[<span data-ttu-id="d534a-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="d534a-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="d534a-192">Join</span><span class="sxs-lookup"><span data-stu-id="d534a-192">Join</span></span>](#join) |[<span data-ttu-id="d534a-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="d534a-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="d534a-194">분할</span><span class="sxs-lookup"><span data-stu-id="d534a-194">Split</span></span>](#split) | | |
| <span data-ttu-id="d534a-195">**Program Flow**</span><span class="sxs-lookup"><span data-stu-id="d534a-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="d534a-196">오류</span><span class="sxs-lookup"><span data-stu-id="d534a-196">Error</span></span>](#error) |[<span data-ttu-id="d534a-197">IIF</span><span class="sxs-lookup"><span data-stu-id="d534a-197">IIF</span></span>](#iif) |[<span data-ttu-id="d534a-198">선택</span><span class="sxs-lookup"><span data-stu-id="d534a-198">Select</span></span>](#select) |[<span data-ttu-id="d534a-199">Switch</span><span class="sxs-lookup"><span data-stu-id="d534a-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="d534a-200">Where</span><span class="sxs-lookup"><span data-stu-id="d534a-200">Where</span></span>](#where) |[<span data-ttu-id="d534a-201">With</span><span class="sxs-lookup"><span data-stu-id="d534a-201">With</span></span>](#with) | | | |
| <span data-ttu-id="d534a-202">**Text**</span><span class="sxs-lookup"><span data-stu-id="d534a-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="d534a-203">GUID</span><span class="sxs-lookup"><span data-stu-id="d534a-203">GUID</span></span>](#guid) |[<span data-ttu-id="d534a-204">InStr</span><span class="sxs-lookup"><span data-stu-id="d534a-204">InStr</span></span>](#instr) |[<span data-ttu-id="d534a-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="d534a-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="d534a-206">LCase</span><span class="sxs-lookup"><span data-stu-id="d534a-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="d534a-207">Left</span><span class="sxs-lookup"><span data-stu-id="d534a-207">Left</span></span>](#left) |[<span data-ttu-id="d534a-208">Len</span><span class="sxs-lookup"><span data-stu-id="d534a-208">Len</span></span>](#len) |[<span data-ttu-id="d534a-209">LTrim.</span><span class="sxs-lookup"><span data-stu-id="d534a-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="d534a-210">Mid</span><span class="sxs-lookup"><span data-stu-id="d534a-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="d534a-211">padLeft</span><span class="sxs-lookup"><span data-stu-id="d534a-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="d534a-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="d534a-212">PadRight</span></span>](#padright) |[<span data-ttu-id="d534a-213">PCase</span><span class="sxs-lookup"><span data-stu-id="d534a-213">PCase</span></span>](#pcase) |[<span data-ttu-id="d534a-214">Replace</span><span class="sxs-lookup"><span data-stu-id="d534a-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="d534a-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="d534a-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="d534a-216">Right</span><span class="sxs-lookup"><span data-stu-id="d534a-216">Right</span></span>](#right) |[<span data-ttu-id="d534a-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="d534a-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="d534a-218">Trim</span><span class="sxs-lookup"><span data-stu-id="d534a-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="d534a-219">UCase</span><span class="sxs-lookup"><span data-stu-id="d534a-219">UCase</span></span>](#ucase) |[<span data-ttu-id="d534a-220">Word</span><span class="sxs-lookup"><span data-stu-id="d534a-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="d534a-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="d534a-221">BitAnd</span></span>
<span data-ttu-id="d534a-222">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-222">**Description:**</span></span>  
<span data-ttu-id="d534a-223">BitAnd 함수는 값에 지정된 비트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="d534a-224">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="d534a-225">value1, value2: 숫자 값은 AND와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="d534a-226">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-226">**Remarks:**</span></span>  
<span data-ttu-id="d534a-227">이 함수는 두 매개 변수를 전부 이진 표현으로 변환시키고 비트를 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="d534a-228">0 - *마스크* 및 *플래그* 내의 하나 혹은 둘 모두 해당하는 비트는 0입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="d534a-229">1 - 2개 모두 해당 비트일 경우 1입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="d534a-230">즉, 두 매개 변수의 해당 비트가 1일 경우를 제외하는 모든 경우에는 0을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="d534a-231">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="d534a-232">16진법 "F" AND "F7"로 이 값을 계산했기 때문에 7을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="d534a-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="d534a-233">BitOr</span></span>
<span data-ttu-id="d534a-234">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-234">**Description:**</span></span>  
<span data-ttu-id="d534a-235">BitOr 함수는 값에 지정된 비트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="d534a-236">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="d534a-237">value1, value2: 숫자 값은 OR과 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="d534a-238">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-238">**Remarks:**</span></span>  
<span data-ttu-id="d534a-239">이 함수는 두 개의 모든 매개 변수를 이진 표현으로 변환하고 마스크 및 플래그 내의 해당 비트가 둘 중에 하나 혹은 둘 다 1일 경우 1로, 해당 비트 모두 0일 경우 0으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="d534a-240">즉, 두 매개 변수의 해당 비트가 0일 경우를 제외하는 모든 경우에 1을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="d534a-241">CBool</span><span class="sxs-lookup"><span data-stu-id="d534a-241">CBool</span></span>
<span data-ttu-id="d534a-242">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-242">**Description:**</span></span>  
<span data-ttu-id="d534a-243">CBool 함수는 계산된 식에 따라 부울을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="d534a-244">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="d534a-245">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-245">**Remarks:**</span></span>  
<span data-ttu-id="d534a-246">수식이 0이 아닌 값으로 계산하는 경우 CBool은 True로, 그 외의 경우에는 False로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="d534a-247">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="d534a-248">두개의 속성이 같은 동일한 값을 가지면 True로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="d534a-249">CDate</span><span class="sxs-lookup"><span data-stu-id="d534a-249">CDate</span></span>
<span data-ttu-id="d534a-250">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-250">**Description:**</span></span>  
<span data-ttu-id="d534a-251">CDate 함수는 문자열에서 UTC 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="d534a-252">날짜/시간은 동기화 내의 네이티브 특성 형식이 아니지만 일부 함수에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="d534a-253">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="d534a-254">값: 날짜, 시간 및 임의적 시간대 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="d534a-255">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-255">**Remarks:**</span></span>  
<span data-ttu-id="d534a-256">반환되는 문자열은 항상 UTC로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="d534a-257">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="d534a-258">직원의 시작 시간을 기반으로 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="d534a-259">"2013-01-11 12:00 AM"을 나타내는 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="d534a-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="d534a-260">CertExtensionOids</span></span>
<span data-ttu-id="d534a-261">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-261">**Description:**</span></span>  
<span data-ttu-id="d534a-262">인증서 개체의 중요한 모든 확장의 Oid 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="d534a-263">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="d534a-264">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-265">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="d534a-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="d534a-266">CertFormat</span></span>
<span data-ttu-id="d534a-267">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-267">**Description:**</span></span>  
<span data-ttu-id="d534a-268">이 X.509v3 인증서의 형식 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="d534a-269">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="d534a-270">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-271">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="d534a-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="d534a-272">CertFriendlyName</span></span>
<span data-ttu-id="d534a-273">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-273">**Description:**</span></span>  
<span data-ttu-id="d534a-274">인증서와 관련된 별칭을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="d534a-275">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="d534a-276">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-277">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="d534a-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="d534a-278">CertHashString</span></span>
<span data-ttu-id="d534a-279">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-279">**Description:**</span></span>  
<span data-ttu-id="d534a-280">X.509v3 인증서의 SHA1 해시 값을 16진수 문자열로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="d534a-281">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="d534a-282">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-283">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="d534a-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="d534a-284">CertIssuer</span></span>
<span data-ttu-id="d534a-285">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-285">**Description:**</span></span>  
<span data-ttu-id="d534a-286">X.509v3 인증서를 발급한 인증 기관의 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="d534a-287">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="d534a-288">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-289">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="d534a-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="d534a-290">CertIssuerDN</span></span>
<span data-ttu-id="d534a-291">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-291">**Description:**</span></span>  
<span data-ttu-id="d534a-292">인증서 발급자의 고유 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="d534a-293">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="d534a-294">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-295">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="d534a-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="d534a-296">CertIssuerOid</span></span>
<span data-ttu-id="d534a-297">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-297">**Description:**</span></span>  
<span data-ttu-id="d534a-298">인증서 발급자의 Oid를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="d534a-299">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="d534a-300">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-301">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="d534a-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="d534a-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="d534a-303">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-303">**Description:**</span></span>  
<span data-ttu-id="d534a-304">이 X.509v3 인증서의 키 알고리즘 정보를 문자열로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="d534a-305">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="d534a-306">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-307">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="d534a-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="d534a-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="d534a-309">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-309">**Description:**</span></span>  
<span data-ttu-id="d534a-310">X.509v3 인증서의 키 알고리즘 매개 변수를 16진수 문자열로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="d534a-311">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="d534a-312">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-313">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="d534a-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="d534a-314">CertNameInfo</span></span>
<span data-ttu-id="d534a-315">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-315">**Description:**</span></span>  
<span data-ttu-id="d534a-316">인증서의 주체 및 발급자 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="d534a-317">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="d534a-318">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-319">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="d534a-320">X509NameType: 주체에 대한 X509NameType 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="d534a-321">includesIssuerName: 발급자 이름을 포함하면 true이고, 그렇지 않으면 false입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="d534a-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="d534a-322">CertNotAfter</span></span>
<span data-ttu-id="d534a-323">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-323">**Description:**</span></span>  
<span data-ttu-id="d534a-324">인증서가 더 이상 유효하지 않은 이후의 현지 시간으로 날짜를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="d534a-325">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="d534a-326">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-327">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="d534a-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="d534a-328">CertNotBefore</span></span>
<span data-ttu-id="d534a-329">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-329">**Description:**</span></span>  
<span data-ttu-id="d534a-330">인증서가 유효한 현지 시간으로 날짜를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="d534a-331">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="d534a-332">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-333">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="d534a-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="d534a-334">CertPublicKeyOid</span></span>
<span data-ttu-id="d534a-335">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-335">**Description:**</span></span>  
<span data-ttu-id="d534a-336">X.509v3 인증서에 대한 공개 키의 Oid를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="d534a-337">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="d534a-338">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-339">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="d534a-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="d534a-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="d534a-341">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-341">**Description:**</span></span>  
<span data-ttu-id="d534a-342">X.509v3 인증서에 대한 공개 키 매개 변수의 Oid를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="d534a-343">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="d534a-344">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-345">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="d534a-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="d534a-346">CertSerialNumber</span></span>
<span data-ttu-id="d534a-347">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-347">**Description:**</span></span>  
<span data-ttu-id="d534a-348">X.509v3 인증서의 일련 번호를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="d534a-349">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="d534a-350">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-351">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="d534a-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="d534a-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="d534a-353">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-353">**Description:**</span></span>  
<span data-ttu-id="d534a-354">인증서의 서명을 만드는 데 사용된 알고리즘의 Oid를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="d534a-355">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="d534a-356">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-357">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="d534a-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="d534a-358">CertSubject</span></span>
<span data-ttu-id="d534a-359">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-359">**Description:**</span></span>  
<span data-ttu-id="d534a-360">인증서의 고유한 주체 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="d534a-361">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="d534a-362">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-363">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="d534a-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="d534a-364">CertSubjectNameDN</span></span>
<span data-ttu-id="d534a-365">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-365">**Description:**</span></span>  
<span data-ttu-id="d534a-366">인증서의 고유한 주체 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="d534a-367">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="d534a-368">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-369">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="d534a-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="d534a-370">CertSubjectNameOid</span></span>
<span data-ttu-id="d534a-371">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-371">**Description:**</span></span>  
<span data-ttu-id="d534a-372">인증서의 주체 이름에 대한 Oid를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="d534a-373">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="d534a-374">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-375">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="d534a-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="d534a-376">CertThumbprint</span></span>
<span data-ttu-id="d534a-377">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-377">**Description:**</span></span>  
<span data-ttu-id="d534a-378">인증서의 지문을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="d534a-379">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="d534a-380">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-381">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="d534a-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="d534a-382">CertVersion</span></span>
<span data-ttu-id="d534a-383">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-383">**Description:**</span></span>  
<span data-ttu-id="d534a-384">인증서의 X.509 형식 버전을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="d534a-385">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="d534a-386">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-387">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="d534a-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="d534a-388">CGuid</span></span>
<span data-ttu-id="d534a-389">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-389">**Description:**</span></span>  
<span data-ttu-id="d534a-390">CGuid 함수는 GUID의 문자열 표현을 이진 표현으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="d534a-391">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="d534a-392">이 패턴에서 문자열 서식: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 또는 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="d534a-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="d534a-393">포함</span><span class="sxs-lookup"><span data-stu-id="d534a-393">Contains</span></span>
<span data-ttu-id="d534a-394">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-394">**Description:**</span></span>  
<span data-ttu-id="d534a-395">Contains 함수는 다중 값 특성에 포함된 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="d534a-396">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-396">**Syntax:**</span></span>  
<span data-ttu-id="d534a-397">`num Contains (mvstring attribute, str search)` - 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="d534a-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="d534a-398">`num Contains (mvref attribute, str search)` - 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="d534a-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="d534a-399">특성: 다중 값 특성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="d534a-400">검색: 특성에서 찾을 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="d534a-401">대소문자 유형: 대소문자를 구분하거나 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="d534a-402">문자열이 발견된 다중값 특성에 인덱스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="d534a-403">문자열을 찾을 수 없는 경우 0이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="d534a-404">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-404">**Remarks:**</span></span>  
<span data-ttu-id="d534a-405">다중값 문자열 특성에 대한 검색 값에서 부분 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="d534a-406">참조 특성에 대해 검색된 문자열은 일치하는 것으로 간주될 값에 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="d534a-407">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="d534a-408">proxyAddresses 특성이 기본 전자 메일 주소(대문자로 표시 “SMTP:”)를 가질 경우 proxyAddress 특성이 반환되며, 그 외에는 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="d534a-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="d534a-409">ConvertFromBase64</span></span>
<span data-ttu-id="d534a-410">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-410">**Description:**</span></span>  
<span data-ttu-id="d534a-411">ConvertFromBase64 함수는 지정된 base64 인코딩 값을 일반 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="d534a-412">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-412">**Syntax:**</span></span>  
<span data-ttu-id="d534a-413">`str ConvertFromBase64(str source)` - 인코딩에 유니코드 가정</span><span class="sxs-lookup"><span data-stu-id="d534a-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="d534a-414">원본: Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="d534a-415">인코딩: 유니코드, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="d534a-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="d534a-416">**예제**</span><span class="sxs-lookup"><span data-stu-id="d534a-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="d534a-417">두 예제 모두 "*Hello world!*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="d534a-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d534a-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="d534a-419">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-419">**Description:**</span></span>  
<span data-ttu-id="d534a-420">ConvertFromUTF8Hex 함수는 지정된 UTF8 16진수 인코딩 값을 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="d534a-421">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="d534a-422">원본: UTF8 2-바이트 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="d534a-423">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-423">**Remarks:**</span></span>  
<span data-ttu-id="d534a-424">이 함수와 ConvertFromBase64([],UTF8) 결과의 차이점은 DN 특성을 사용하기 쉽다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="d534a-425">이 형식은 DN으로 Azure Active Directory에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="d534a-426">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="d534a-427">"*Hello world!*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="d534a-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="d534a-428">ConvertToBase64</span></span>
<span data-ttu-id="d534a-429">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-429">**Description:**</span></span>  
<span data-ttu-id="d534a-430">ConvertToBase64 함수는 문자열을 유니코드 base64 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="d534a-431">정수 배열 값을 base 64 자릿수로 인코딩된 동등한 문자열 표현으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="d534a-432">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="d534a-433">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="d534a-434">"SABlAGwAbABvACAAdwBvAHIAbABkACEA"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="d534a-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d534a-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="d534a-436">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-436">**Description:**</span></span>  
<span data-ttu-id="d534a-437">ConvertToUTF8Hex 함수는 문자열을 UTF8 16진수 인코딩 값으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="d534a-438">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="d534a-439">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-439">**Remarks:**</span></span>  
<span data-ttu-id="d534a-440">이 함수의 출력 형식은 DN 특성 형식으로 Azure Active Directory에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="d534a-441">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="d534a-442">48656C6C6F20776F726C6421을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="d534a-443">개수</span><span class="sxs-lookup"><span data-stu-id="d534a-443">Count</span></span>
<span data-ttu-id="d534a-444">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-444">**Description:**</span></span>  
<span data-ttu-id="d534a-445">Count 함수는 다중값 특성의 요소 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="d534a-446">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="d534a-447">CNum</span><span class="sxs-lookup"><span data-stu-id="d534a-447">CNum</span></span>
<span data-ttu-id="d534a-448">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-448">**Description:**</span></span>  
<span data-ttu-id="d534a-449">CNum 함수는 문자열을 숫자 데이터 형식으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="d534a-450">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="d534a-451">CRef</span><span class="sxs-lookup"><span data-stu-id="d534a-451">CRef</span></span>
<span data-ttu-id="d534a-452">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-452">**Description:**</span></span>  
<span data-ttu-id="d534a-453">문자열을 참조 특성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="d534a-454">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="d534a-455">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="d534a-456">CStr</span><span class="sxs-lookup"><span data-stu-id="d534a-456">CStr</span></span>
<span data-ttu-id="d534a-457">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-457">**Description:**</span></span>  
<span data-ttu-id="d534a-458">CStr 함수는 문자열 데이터 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="d534a-459">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="d534a-460">값: 숫자 값, 참조 특성 또는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="d534a-461">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="d534a-462">"cn=Joe,dc=contoso,dc=com"을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="d534a-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="d534a-463">DateAdd</span></span>
<span data-ttu-id="d534a-464">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-464">**Description:**</span></span>  
<span data-ttu-id="d534a-465">지정된 시간 간격이 추가된 날짜를 포함하는 날짜를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="d534a-466">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="d534a-467">간격: 추가하고자 하는 시간 간격에 해당하는 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="d534a-468">문자열은 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="d534a-469">yyyy 년</span><span class="sxs-lookup"><span data-stu-id="d534a-469">yyyy Year</span></span>
  * <span data-ttu-id="d534a-470">q 분기</span><span class="sxs-lookup"><span data-stu-id="d534a-470">q Quarter</span></span>
  * <span data-ttu-id="d534a-471">m 월</span><span class="sxs-lookup"><span data-stu-id="d534a-471">m Month</span></span>
  * <span data-ttu-id="d534a-472">y 연간 일자</span><span class="sxs-lookup"><span data-stu-id="d534a-472">y Day of year</span></span>
  * <span data-ttu-id="d534a-473">d 일</span><span class="sxs-lookup"><span data-stu-id="d534a-473">d Day</span></span>
  * <span data-ttu-id="d534a-474">w 요일</span><span class="sxs-lookup"><span data-stu-id="d534a-474">w Weekday</span></span>
  * <span data-ttu-id="d534a-475">ww 주</span><span class="sxs-lookup"><span data-stu-id="d534a-475">ww Week</span></span>
  * <span data-ttu-id="d534a-476">h 시간</span><span class="sxs-lookup"><span data-stu-id="d534a-476">h Hour</span></span>
  * <span data-ttu-id="d534a-477">n 분</span><span class="sxs-lookup"><span data-stu-id="d534a-477">n Minute</span></span>
  * <span data-ttu-id="d534a-478">s 초</span><span class="sxs-lookup"><span data-stu-id="d534a-478">s Second</span></span>
* <span data-ttu-id="d534a-479">값: 추가하고자 하는 단위 수 입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-479">value: The number of units you want to add.</span></span> <span data-ttu-id="d534a-480">양수(미래 날짜) 또는 음수(과거 날짜)가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="d534a-481">날짜: 날짜/시간은 간격이 추가된 날짜로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="d534a-482">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="d534a-483">3개월을 추가하고 "2001-04-01"을 나타내는 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="d534a-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="d534a-484">DateFromNum</span></span>
<span data-ttu-id="d534a-485">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-485">**Description:**</span></span>  
<span data-ttu-id="d534a-486">DateFromNum 함수는 AD의 날짜 값 형식을 날짜/시간 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="d534a-487">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="d534a-488">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="d534a-489">2012-01-01 23:00:00을 나타내는 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="d534a-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="d534a-490">DNComponent</span></span>
<span data-ttu-id="d534a-491">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-491">**Description:**</span></span>  
<span data-ttu-id="d534a-492">DNComponent 함수는 왼쪽부터 지정된 DN 구성 요소의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="d534a-493">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="d534a-494">dn: 참조 특성 해석</span><span class="sxs-lookup"><span data-stu-id="d534a-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="d534a-495">ComponentNumber: 반환할 DN 내의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="d534a-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="d534a-496">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="d534a-497">dn이 "cn=Joe,ou=…"인 경우 Joe를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="d534a-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="d534a-498">DNComponentRev</span></span>
<span data-ttu-id="d534a-499">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-499">**Description:**</span></span>  
<span data-ttu-id="d534a-500">DNComponentRev 함수는 오른쪽(끝)부터 지정된 DN 구성 요소의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="d534a-501">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="d534a-502">dn: 참조 특성 해석</span><span class="sxs-lookup"><span data-stu-id="d534a-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="d534a-503">ComponentNumber-반환할 DN 내의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="d534a-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="d534a-504">옵션: DC –"dc ="가 있는 모든 구성 요소를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="d534a-505">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-505">**Example:**</span></span>  
<span data-ttu-id="d534a-506">dn이 "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"인 경우</span><span class="sxs-lookup"><span data-stu-id="d534a-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="d534a-507">모두 US를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="d534a-508">오류</span><span class="sxs-lookup"><span data-stu-id="d534a-508">Error</span></span>
<span data-ttu-id="d534a-509">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-509">**Description:**</span></span>  
<span data-ttu-id="d534a-510">Error 함수는 사용자 지정 오류를 반환하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="d534a-511">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="d534a-512">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="d534a-513">accountName 특성이 없는 경우 개체에서 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="d534a-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="d534a-514">EscapeDNComponent</span></span>
<span data-ttu-id="d534a-515">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-515">**Description:**</span></span>  
<span data-ttu-id="d534a-516">EscapeDNComponent 함수는 DN의 한 구성 요소를 받고 LDAP에 나타낼 수 있도록 이스케이프합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="d534a-517">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="d534a-518">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="d534a-519">LDAP 디렉터리 내에서, displayName 특성에 LDAP에서 이스케이프된 문자가 포함된 경우에도 개체가 생성될 수 있음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="d534a-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="d534a-520">FormatDateTime</span></span>
<span data-ttu-id="d534a-521">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-521">**Description:**</span></span>  
<span data-ttu-id="d534a-522">FormatDateTime 함수는 날짜/시간을 지정된 형식의 문자열로 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="d534a-523">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="d534a-524">value: 날짜/시간 형식의 값</span><span class="sxs-lookup"><span data-stu-id="d534a-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="d534a-525">형식: 변환할 형식을 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="d534a-526">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-526">**Remarks:**</span></span>  
<span data-ttu-id="d534a-527">형식에 대해 가능한 값은 [사용자 정의 날짜/시간 형식(Format 함수)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="d534a-528">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="d534a-529">"2007-12-25"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="d534a-530">"20140905081453.0Z"를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="d534a-531">GUID</span><span class="sxs-lookup"><span data-stu-id="d534a-531">GUID</span></span>
<span data-ttu-id="d534a-532">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-532">**Description:**</span></span>  
<span data-ttu-id="d534a-533">함수 GUID는 임의의 GUID를 새로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="d534a-534">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="d534a-535">IIF</span><span class="sxs-lookup"><span data-stu-id="d534a-535">IIF</span></span>
<span data-ttu-id="d534a-536">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-536">**Description:**</span></span>  
<span data-ttu-id="d534a-537">IIF 함수는 지정된 조건에 따라 가능한 값 집합 중 하나를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="d534a-538">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="d534a-539">조건: true 또는 false로 계산될 수 있는 임의의 값 또는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="d534a-540">valueIfTrue: 조건이 true로 평가되는 경우 반환된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="d534a-541">valueIfFalse: 조건이 false로 평가되는 경우 반환된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="d534a-542">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="d534a-543">사용자가 인턴일 경우 사용자 별칭 앞에 “t-”를 추가하여 반환하고, 그 외의 경우에는 본래의 별칭 그대로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="d534a-544">InStr</span><span class="sxs-lookup"><span data-stu-id="d534a-544">InStr</span></span>
<span data-ttu-id="d534a-545">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-545">**Description:**</span></span>  
<span data-ttu-id="d534a-546">InStr 함수는 문자열에서 부분 문자열이 처음 나오는 경우를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="d534a-547">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="d534a-548">stringcheck: 검색할 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="d534a-549">stringmatch: 찾을 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="d534a-550">start: 부분 문자열을 찾을 시작 위치</span><span class="sxs-lookup"><span data-stu-id="d534a-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="d534a-551">compare: vbTextCompare 또는 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="d534a-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="d534a-552">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-552">**Remarks:**</span></span>  
<span data-ttu-id="d534a-553">부분 문자열을 찾으면 위치가 반환되고, 찾지 못할 경우 0이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="d534a-554">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="d534a-555">5로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="d534a-556">7로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="d534a-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="d534a-557">InStrRev</span></span>
<span data-ttu-id="d534a-558">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-558">**Description:**</span></span>  
<span data-ttu-id="d534a-559">InStrRev 함수는 문자열에서 부분 문자열이 마지막으로 나오는 경우를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="d534a-560">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="d534a-561">stringcheck: 검색할 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="d534a-562">stringmatch: 찾을 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="d534a-563">start: 부분 문자열을 찾을 시작 위치</span><span class="sxs-lookup"><span data-stu-id="d534a-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="d534a-564">compare: vbTextCompare 또는 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="d534a-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="d534a-565">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-565">**Remarks:**</span></span>  
<span data-ttu-id="d534a-566">부분 문자열을 찾으면 위치가 반환되고, 찾지 못할 경우 0이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="d534a-567">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="d534a-568">7을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="d534a-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="d534a-569">IsBitSet</span></span>
<span data-ttu-id="d534a-570">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-570">**Description:**</span></span>  
<span data-ttu-id="d534a-571">IsBitSet 함수는 비트 설정 여부를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="d534a-572">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="d534a-573">값: 숫자 값은 evaluated.flag: 숫자 값은 계산할 수 있는 숫자 값을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="d534a-574">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="d534a-575">비트 "4"는 16진수 값 "F" 안에 설정되어 있으므로 True를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="d534a-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="d534a-576">IsDate</span></span>
<span data-ttu-id="d534a-577">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-577">**Description:**</span></span>  
<span data-ttu-id="d534a-578">식이 날짜/시간 형식으로 계산될 경우 IsDate 함수는 True로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="d534a-579">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="d534a-580">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-580">**Remarks:**</span></span>  
<span data-ttu-id="d534a-581">CDate()가 정상적으로 수행될 수 있는지 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="d534a-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="d534a-582">IsCert</span></span>
<span data-ttu-id="d534a-583">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-583">**Description:**</span></span>  
<span data-ttu-id="d534a-584">원시 데이터를 .NET X509Certificate2 인증서 개체로 직렬화할 수 있으면 true를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="d534a-585">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="d534a-586">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d534a-587">바이트 배열은 DER(이진) 또는 Base64로 인코딩된 X.509 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="d534a-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="d534a-588">IsEmpty</span></span>
<span data-ttu-id="d534a-589">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-589">**Description:**</span></span>  
<span data-ttu-id="d534a-590">특성이 CS 또는 MV에서 나타나지만 빈 문자열로 계산될 경우 IsEmpty 함수는 True로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="d534a-591">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="d534a-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="d534a-592">IsGuid</span></span>
<span data-ttu-id="d534a-593">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-593">**Description:**</span></span>  
<span data-ttu-id="d534a-594">문자열을 GUID로 변환할 수 있는 경우 IsGuid 함수는 True로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="d534a-595">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="d534a-596">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-596">**Remarks:**</span></span>  
<span data-ttu-id="d534a-597">GUID는 다음 패턴 중 하나로 정의됩니다. xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 또는 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="d534a-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="d534a-598">CGuid()가 성공적으로 수행될 수 있는지 여부를 결정하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="d534a-599">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="d534a-600">StrAttribute가 GUID 형식을 가질 경우, 이진 표현으로 반환되며, 아닐 경우 Null을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="d534a-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="d534a-601">IsNull</span></span>
<span data-ttu-id="d534a-602">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-602">**Description:**</span></span>  
<span data-ttu-id="d534a-603">식이 Null로 계산되면 IsNull 함수는 true를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="d534a-604">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="d534a-605">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-605">**Remarks:**</span></span>  
<span data-ttu-id="d534a-606">특성이 없는 경우 Null로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="d534a-607">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="d534a-608">CS 또는 MV에 특성이 없을 경우 True를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="d534a-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="d534a-609">IsNullOrEmpty</span></span>
<span data-ttu-id="d534a-610">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-610">**Description:**</span></span>  
<span data-ttu-id="d534a-611">식이 null 또는 빈 문자열일 경우 IsNullOrEmpty 함수는 true를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="d534a-612">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="d534a-613">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-613">**Remarks:**</span></span>  
<span data-ttu-id="d534a-614">특성이 없거나, 빈 문자열로 존재하는 경우 True로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="d534a-615">이 함수의 역원을 IsPresnt라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="d534a-616">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="d534a-617">특성이 없거나 CS 또는 MV에서 빈 문자열인 경우 True를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="d534a-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="d534a-618">IsNumeric</span></span>
<span data-ttu-id="d534a-619">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-619">**Description:**</span></span>  
<span data-ttu-id="d534a-620">IsNumeric 함수에는 숫자 형식으로 식이 계산될 수 있는지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="d534a-621">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="d534a-622">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-622">**Remarks:**</span></span>  
<span data-ttu-id="d534a-623">CNum()이 식을 구문 분석하는 데 성공할 수 있는지 여부를 결정할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="d534a-624">IsString</span><span class="sxs-lookup"><span data-stu-id="d534a-624">IsString</span></span>
<span data-ttu-id="d534a-625">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-625">**Description:**</span></span>  
<span data-ttu-id="d534a-626">식이 문자열 형식으로 계산될 수 있는 경우 IsString 함수는 True로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="d534a-627">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="d534a-628">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-628">**Remarks:**</span></span>  
<span data-ttu-id="d534a-629">CStr()이 식을 구문 분석하는 데 성공할 수 있는지 여부를 결정할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="d534a-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="d534a-630">IsPresent</span></span>
<span data-ttu-id="d534a-631">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-631">**Description:**</span></span>  
<span data-ttu-id="d534a-632">식이 Null이 아니고 비어 있지 않은 문자열로 계산되는 경우 IsPresent 함수는 true를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="d534a-633">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="d534a-634">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-634">**Remarks:**</span></span>  
<span data-ttu-id="d534a-635">이 함수의 역함수는 IsNullOrEmpty으로 지칭됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="d534a-636">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="d534a-637">항목</span><span class="sxs-lookup"><span data-stu-id="d534a-637">Item</span></span>
<span data-ttu-id="d534a-638">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-638">**Description:**</span></span>  
<span data-ttu-id="d534a-639">Item 함수는 다중값 문자열/특성에서 하나의 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="d534a-640">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="d534a-641">attribute: 다중값 특성</span><span class="sxs-lookup"><span data-stu-id="d534a-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="d534a-642">인덱스: 다중값 문자열에 있는 항목에 대한 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="d534a-643">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-643">**Remarks:**</span></span>  
<span data-ttu-id="d534a-644">Item 함수는 다중값 특성의 항목에 대한 인덱스를 반환하는 Contains 함수와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="d534a-645">인덱스가 범위를 초과하는 경우 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="d534a-646">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="d534a-647">기본 전자 메일 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="d534a-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="d534a-648">ItemOrNull</span></span>
<span data-ttu-id="d534a-649">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-649">**Description:**</span></span>  
<span data-ttu-id="d534a-650">ItemOrNull 함수는 다중값 문자열/특성에서 하나의 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="d534a-651">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="d534a-652">attribute: 다중값 특성</span><span class="sxs-lookup"><span data-stu-id="d534a-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="d534a-653">인덱스: 다중값 문자열에 있는 항목에 대한 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="d534a-654">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-654">**Remarks:**</span></span>  
<span data-ttu-id="d534a-655">ItemOrNull 함수는 다중값 특성의 항목에 대한 인덱스를 반환하는 Contains 함수와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="d534a-656">인덱스가 범위를 초과하는 경우 Null 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="d534a-657">Join</span><span class="sxs-lookup"><span data-stu-id="d534a-657">Join</span></span>
<span data-ttu-id="d534a-658">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-658">**Description:**</span></span>  
<span data-ttu-id="d534a-659">Join 함수는 다중값 문자열을 사용하여 각 항목 사이에 지정된 구분 기호를 삽입하여 단일 값 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="d534a-660">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="d534a-661">attribute: 연결할 문자열을 포함하는 다중값 특성</span><span class="sxs-lookup"><span data-stu-id="d534a-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="d534a-662">구분 기호: 반환된 문자열의 부분 문자열을 구분하는데 사용되는 모든 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="d534a-663">생략하면 공백(" ")이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="d534a-664">구분 기호가 길이가 0인 문자열(“”)또는 없을 경우 ,목록에서 모든 항목이 구분 기호 없이 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="d534a-665">**주의**</span><span class="sxs-lookup"><span data-stu-id="d534a-665">**Remarks**</span></span>  
<span data-ttu-id="d534a-666">Join 및 Split 함수 사이에 패리티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="d534a-667">Join 함수는 단일 문자열을 반환하기 위해 문자열의 배열을 채택하고  구분 기호 문자열을 사용하여 배열을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="d534a-668">Split 함수는 문자열의 배열을 반환하기 위해 문자열을 채택하고 구분 기호로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="d534a-669">그러나 Join 함수는 모든 구분 기호 문자열을 사용하여 문자열을 연결할 수 있지만, Split 함수는 단일 문자 구분 기호를 사용하여 오직 문자열을 나눌 수만 있다는 것이 가장 중요한 차이점입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="d534a-670">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="d534a-671">"SMTP:john.doe@contoso.com,smtp:jd@contoso.com"을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="d534a-672">LCase</span><span class="sxs-lookup"><span data-stu-id="d534a-672">LCase</span></span>
<span data-ttu-id="d534a-673">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-673">**Description:**</span></span>  
<span data-ttu-id="d534a-674">LCase 함수는 문자열의 모든 문자를 소문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="d534a-675">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="d534a-676">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="d534a-677">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="d534a-678">Left</span><span class="sxs-lookup"><span data-stu-id="d534a-678">Left</span></span>
<span data-ttu-id="d534a-679">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-679">**Description:**</span></span>  
<span data-ttu-id="d534a-680">Left 함수는 문자열 왼쪽부터 지정된 수의 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="d534a-681">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="d534a-682">string: 문자로 반환될 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-682">string: the string to return characters from</span></span>
* <span data-ttu-id="d534a-683">NumChars: 문자열의 시작(왼쪽)에서 반환될 문자의 개수를 식별하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="d534a-684">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-684">**Remarks:**</span></span>  
<span data-ttu-id="d534a-685">문자열의 첫 번째 numChars 문자를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="d534a-686">numChars = 0 인 경우, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="d534a-687">numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="d534a-688">문자열이 null이면 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-688">If string is null, return empty string.</span></span>

<span data-ttu-id="d534a-689">문자열이 numChars 내에서 숫자가 지정한 문자보다 적은 문자를 포함하는 경우, 문자열과 동일한 문자열(즉, 매개 변수 1의 모든 문자가 포함)이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="d534a-690">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="d534a-691">"Joh"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="d534a-692">Len</span><span class="sxs-lookup"><span data-stu-id="d534a-692">Len</span></span>
<span data-ttu-id="d534a-693">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-693">**Description:**</span></span>  
<span data-ttu-id="d534a-694">Len 함수는 문자열의 문자 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="d534a-695">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="d534a-696">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="d534a-697">8을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="d534a-698">LTrim.</span><span class="sxs-lookup"><span data-stu-id="d534a-698">LTrim</span></span>
<span data-ttu-id="d534a-699">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-699">**Description:**</span></span>  
<span data-ttu-id="d534a-700">LTrim 함수는 문자열에서 선행 공백을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="d534a-701">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="d534a-702">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="d534a-703">"Test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="d534a-704">Mid</span><span class="sxs-lookup"><span data-stu-id="d534a-704">Mid</span></span>
<span data-ttu-id="d534a-705">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-705">**Description:**</span></span>  
<span data-ttu-id="d534a-706">Mid 함수는 문자열의 지정된 위치부터 지정된 수의 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="d534a-707">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="d534a-708">string: 문자로 반환될 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-708">string: the string to return characters from</span></span>
* <span data-ttu-id="d534a-709">start : 문자열 내의 시작지점에서 반환할 문자를 식별하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="d534a-710">NumChars: 문자열의 위치에서 반환될 문자의 수를 식별하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="d534a-711">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-711">**Remarks:**</span></span>  
<span data-ttu-id="d534a-712">문자열의 시작 위치에서 시작되는 numChars 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="d534a-713">문자열의 start 위치에서 numChars 문자를 포함하는 문자열:</span><span class="sxs-lookup"><span data-stu-id="d534a-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="d534a-714">numChars = 0 인 경우, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="d534a-715">numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="d534a-716">start > 문자열의 길이인 경우, 입력된 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="d534a-717">start < = 0 인 경우, 입력된 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="d534a-718">문자열이 null이면 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-718">If string is null, return empty string.</span></span>

<span data-ttu-id="d534a-719">시작 위치에서 문자열의 numChar 문자가 남아있지 않는 경우, 가능한 많은 문자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="d534a-720">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="d534a-721">"hn Do"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="d534a-722">"Doe"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="d534a-723">Now</span><span class="sxs-lookup"><span data-stu-id="d534a-723">Now</span></span>
<span data-ttu-id="d534a-724">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-724">**Description:**</span></span>  
<span data-ttu-id="d534a-725">Now 함수는 컴퓨터의 시스템 날짜 및 시간에 따라 현재 날짜 및 시간을 지정하는 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="d534a-726">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="d534a-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="d534a-727">NumFromDate</span></span>
<span data-ttu-id="d534a-728">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-728">**Description:**</span></span>  
<span data-ttu-id="d534a-729">NumFromDate 함수는 AD 날짜 형식으로 날짜를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="d534a-730">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="d534a-731">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="d534a-732">129699324000000000을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="d534a-733">padLeft</span><span class="sxs-lookup"><span data-stu-id="d534a-733">PadLeft</span></span>
<span data-ttu-id="d534a-734">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-734">**Description:**</span></span>  
<span data-ttu-id="d534a-735">PadLeft 함수는 제공된 채움 문자를 사용하여 문자열을 지정된 길이로 왼쪽 채움합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="d534a-736">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="d534a-737">문자열: 문자열을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-737">string: the string to pad.</span></span>
* <span data-ttu-id="d534a-738">길이: 원하는 문자열의 길이를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="d534a-739">padCharacter: 채움 문자를 사용하여 단일 문자로 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="d534a-740">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-740">**Remarks:**</span></span>

* <span data-ttu-id="d534a-741">문자열의 길이가 본래의 길이보다 짧을 경우, 길이가 같아질때가지 문자열의 시작 부분(왼쪽)에 padCharacter를 반복적으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="d534a-742">PadCharacter는 공백 문자가 될 수 있지만, null 값은 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="d534a-743">문자열이 길이가 본래의 길이보다 같거나 클 경우, 문자열은 변함이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="d534a-744">문자열 길이가 크거나 같을 경우, 문자열과 동일한 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="d534a-745">문자열의 길이가 본래의 길이보다 작은 경우, 채움 문자로 채워진 문자열이 포함된 원하는 길이의 새 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="d534a-746">문자열이 null이면, 함수는 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="d534a-747">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="d534a-748">"000000User"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="d534a-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="d534a-749">PadRight</span></span>
<span data-ttu-id="d534a-750">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-750">**Description:**</span></span>  
<span data-ttu-id="d534a-751">PadRight 함수는 제공된 채움 문자를 사용하여 지정된 길이로 문자열을 오른쪽 채움합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="d534a-752">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="d534a-753">문자열: 문자열을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-753">string: the string to pad.</span></span>
* <span data-ttu-id="d534a-754">길이: 원하는 문자열의 길이를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="d534a-755">padCharacter: 채움 문자를 사용하여 단일 문자로 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="d534a-756">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-756">**Remarks:**</span></span>

* <span data-ttu-id="d534a-757">문자열의 길이가 본래의 길이보다 짧을 경우, 길이가 같아질때까지 문자열의 끝(오른쪽)에 padCharacter를 반복적으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="d534a-758">PadCharacter는 공백 문자가 될 수 있지만, null 값은 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="d534a-759">문자열이 길이가 본래의 길이보다 같거나 클 경우, 문자열은 변함이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="d534a-760">문자열 길이가 크거나 같을 경우, 문자열과 동일한 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="d534a-761">문자열의 길이가 본래의 길이보다 작은 경우, 채움 문자로 채워진 문자열이 포함된 원하는 길이의 새 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="d534a-762">문자열이 null이면, 함수는 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="d534a-763">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="d534a-764">"User000000"을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="d534a-765">PCase</span><span class="sxs-lookup"><span data-stu-id="d534a-765">PCase</span></span>
<span data-ttu-id="d534a-766">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-766">**Description:**</span></span>  
<span data-ttu-id="d534a-767">PCase 함수는 문자열내의 각 공백으로 구분된 단어의 첫 문자를 대문자로 변환하고 다른 모든 문자를 소문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="d534a-768">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="d534a-769">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-769">**Remarks:**</span></span>

* <span data-ttu-id="d534a-770">이 기능은 현재 머리글자어와 같이 전체적으로 대문자인 단어를 변경할 적절한 대/소문자 구분을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="d534a-771">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="d534a-772">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="d534a-773">"Test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="d534a-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="d534a-774">RandomNum</span></span>
<span data-ttu-id="d534a-775">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-775">**Description:**</span></span>  
<span data-ttu-id="d534a-776">RandomNum 함수는 지정된 간격 사이의 난수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="d534a-777">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="d534a-778">start: 생성할 난수 값의 하한을 식별하는 번호</span><span class="sxs-lookup"><span data-stu-id="d534a-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="d534a-779">끝: 난수 값의 상한값을 식별 하는 번호를 생성</span><span class="sxs-lookup"><span data-stu-id="d534a-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="d534a-780">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="d534a-781">734를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="d534a-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="d534a-782">RemoveDuplicates</span></span>
<span data-ttu-id="d534a-783">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-783">**Description:**</span></span>  
<span data-ttu-id="d534a-784">RemoveDuplicates 함수는 다중값 문자열을 사용하여 개별 값을 고유하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="d534a-785">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="d534a-786">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="d534a-787">모든 중복 값을 제거한 삭제된 proxyAddress 특성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="d534a-788">Replace</span><span class="sxs-lookup"><span data-stu-id="d534a-788">Replace</span></span>
<span data-ttu-id="d534a-789">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-789">**Description:**</span></span>  
<span data-ttu-id="d534a-790">Replace 함수는 한 문자열이 나오는 모든 경우를 다른 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="d534a-791">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="d534a-792">string: 값을 바꿀 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="d534a-793">OldValue: 검색한 후 바꿀 문자열</span><span class="sxs-lookup"><span data-stu-id="d534a-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="d534a-794">NewValue: 문자열을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="d534a-795">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-795">**Remarks:**</span></span>  
<span data-ttu-id="d534a-796">이 함수는 다음의 특별한 모니커를 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="d534a-797">\n – 새로운 줄</span><span class="sxs-lookup"><span data-stu-id="d534a-797">\n – New Line</span></span>
* <span data-ttu-id="d534a-798">\r – 캐리지 반환</span><span class="sxs-lookup"><span data-stu-id="d534a-798">\r – Carriage Return</span></span>
* <span data-ttu-id="d534a-799">\t – 탭</span><span class="sxs-lookup"><span data-stu-id="d534a-799">\t – Tab</span></span>

<span data-ttu-id="d534a-800">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="d534a-801">CRLF를 쉼표와 공백으로 바꾸고 "One Microsoft Way, Redmond, WA, USA"로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="d534a-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="d534a-802">ReplaceChars</span></span>
<span data-ttu-id="d534a-803">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-803">**Description:**</span></span>  
<span data-ttu-id="d534a-804">ReplaceChars 함수는 ReplacePattern 문자열에 해당 문자가 나오는 모든 경우를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="d534a-805">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="d534a-806">string: 문자를 대체하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="d534a-807">ReplacePattern: 바꿀 문자를 사용하여 사전에 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="d534a-808">형식은 {source1}: {target1} {source2}: {target2} {sourceN} {targetN} 원본은 찾을 문자열이고 대상은 대체할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="d534a-809">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-809">**Remarks:**</span></span>

* <span data-ttu-id="d534a-810">함수는 정의된 원본의 각 항목을 사용하여 대상의 항목을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="d534a-811">원본은 하나의 문자만(유니코드) 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="d534a-812">원본은 공백이거나 한글자 이상일 수 없습니다(구문 분석 오류).</span><span class="sxs-lookup"><span data-stu-id="d534a-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="d534a-813">대상에는 여러 문자가 있을 수 있습니다(예: ö:oe, β:ss).</span><span class="sxs-lookup"><span data-stu-id="d534a-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="d534a-814">문자가 제거되어야 하는 경우 대상은 비어있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="d534a-815">원본은 대소문자를 구분하며 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="d534a-816">,(쉼표) 및: (콜론)은 지정된 문자이며 이 함수를 사용하여 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="d534a-817">ReplacePattern의 공백 및 white character는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="d534a-818">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="d534a-819">Raksmorgas를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="d534a-820">"ONeil"을 반환합니다. 단일 틱이 제거 대상으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="d534a-821">Right</span><span class="sxs-lookup"><span data-stu-id="d534a-821">Right</span></span>
<span data-ttu-id="d534a-822">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-822">**Description:**</span></span>  
<span data-ttu-id="d534a-823">Right 함수는 문자열의 오른쪽(끝)부터 지정된 수의 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="d534a-824">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="d534a-825">string: 문자로 반환될 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-825">string: the string to return characters from</span></span>
* <span data-ttu-id="d534a-826">NumChars: 숫자는 문자열의 끝(오른쪽)에서 반환될 문자열의 수를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="d534a-827">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-827">**Remarks:**</span></span>  
<span data-ttu-id="d534a-828">문자열의 마지막 위치부터 NumChars 문자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="d534a-829">문자열의 마지막 numChars 문자를 포함 하는 문자열:</span><span class="sxs-lookup"><span data-stu-id="d534a-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="d534a-830">numChars = 0 인 경우, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="d534a-831">numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="d534a-832">문자열이 null이면 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-832">If string is null, return empty string.</span></span>

<span data-ttu-id="d534a-833">문자열의 문자가 NumChars의 지정된 숫자보다 적은 경우, 문자열과 동일한 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="d534a-834">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="d534a-835">"Doe"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="d534a-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="d534a-836">RTrim</span></span>
<span data-ttu-id="d534a-837">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-837">**Description:**</span></span>  
<span data-ttu-id="d534a-838">RTrim 함수는 문자열에서 후행 공백을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="d534a-839">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="d534a-840">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="d534a-841">"Test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="d534a-842">여기서</span><span class="sxs-lookup"><span data-stu-id="d534a-842">Select</span></span>
<span data-ttu-id="d534a-843">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-843">**Description:**</span></span>  
<span data-ttu-id="d534a-844">지정된 함수에 기반하여 다중값 특성(또는 식 출력)의 모든 값을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="d534a-845">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="d534a-846">item: 다중값 특성의 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="d534a-847">attribute: 다중값 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="d534a-848">expression: 값의 컬렉션을 반환하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="d534a-849">condition: 특성의 한 항목을 처리할 수 있는 모든 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="d534a-850">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="d534a-851">하이픈(-)을 제거한 후에 otherPhone 다중값 특성의 모든 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="d534a-852">분할</span><span class="sxs-lookup"><span data-stu-id="d534a-852">Split</span></span>
<span data-ttu-id="d534a-853">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-853">**Description:**</span></span>  
<span data-ttu-id="d534a-854">Split 함수는 구분 기호로 구분된 문자열을 다중값 문자열로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="d534a-855">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="d534a-856">value: 구분할 구분 기호 문자를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="d534a-857">delimiter: 구분 기호로 사용할 수 있는 단일 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="d534a-858">limit: 반환될 수 있는 값의 최대 갯수입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="d534a-859">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="d534a-860">proxyAddress 특성에 유용한 2개 이상의 요소가 있는 다중값 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="d534a-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="d534a-861">StringFromGuid</span></span>
<span data-ttu-id="d534a-862">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-862">**Description:**</span></span>  
<span data-ttu-id="d534a-863">StringFromGuid 함수는 이진 GUID를 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="d534a-864">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="d534a-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="d534a-865">StringFromSid</span></span>
<span data-ttu-id="d534a-866">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-866">**Description:**</span></span>  
<span data-ttu-id="d534a-867">StringFromSid 함수는 보안 식별자를 포함한 바이트 배열을 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="d534a-868">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="d534a-869">Switch</span><span class="sxs-lookup"><span data-stu-id="d534a-869">Switch</span></span>
<span data-ttu-id="d534a-870">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-870">**Description:**</span></span>  
<span data-ttu-id="d534a-871">Switch 함수는 계산 조건에 따라 단일 값을 반환하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="d534a-872">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="d534a-873">expr: 계산하고자 하는 변형 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="d534a-874">value: 해당 식이 True일 경우 반환될 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="d534a-875">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-875">**Remarks:**</span></span>  
<span data-ttu-id="d534a-876">Switch 함수 인수 목록은 식과 값의 쌍으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="d534a-877">식은 왼쪽에서 오른쪽으로 계산되며, True로 계산되는 첫 번째 식과 연결된 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="d534a-878">파트가 적절한 쌍으로 연결되지 않으면, 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="d534a-879">예를들어, expr1이 True면, Switch는 value1을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="d534a-880">expr-1이 False이고, expr-2가 True면 Switch는 Value-2로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="d534a-881">다음의 경우 Switch는 Nothing을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="d534a-882">어떤 식도 True가 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="d534a-882">None of the expressions are True.</span></span>
* <span data-ttu-id="d534a-883">첫 번째 True 식의 해당 값이 Null인 경우</span><span class="sxs-lookup"><span data-stu-id="d534a-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="d534a-884">그 중 하나만 반환되더라도, Switch는 모든 식을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="d534a-885">그렇기 때문에 원하지 않는 결과가 나타나지 않도록 주의해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="d534a-886">예를 들어, 어떤 식의 계산이 division by zero 오류로 나올 경우, 오류가 발생한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="d534a-887">값은 사용자 지정 문자열을 반환하는 오류 함수가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="d534a-888">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="d534a-889">일부 주요 도시에서 사용하는 언어를 반환하지만 그 외의 경우에는 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="d534a-890">Trim</span><span class="sxs-lookup"><span data-stu-id="d534a-890">Trim</span></span>
<span data-ttu-id="d534a-891">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-891">**Description:**</span></span>  
<span data-ttu-id="d534a-892">Trim 함수는 선행 및 후행 공백을 문자열에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="d534a-893">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="d534a-894">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="d534a-895">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="d534a-896">proxyAddress 특성의 각 값에 대한 선행 및 후행 공백을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="d534a-897">UCase</span><span class="sxs-lookup"><span data-stu-id="d534a-897">UCase</span></span>
<span data-ttu-id="d534a-898">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-898">**Description:**</span></span>  
<span data-ttu-id="d534a-899">UCase 함수는 문자열의 모든 문자를 대문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="d534a-900">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="d534a-901">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="d534a-902">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="d534a-903">Where</span><span class="sxs-lookup"><span data-stu-id="d534a-903">Where</span></span>

<span data-ttu-id="d534a-904">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-904">**Description:**</span></span>  
<span data-ttu-id="d534a-905">특정 조건에 기반하여 다중값 특성(또는 식 출력)의 값에 대한 하위 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="d534a-906">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="d534a-907">item: 다중값 특성의 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="d534a-908">attribute: 다중값 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="d534a-909">condition: true 또는 false로 평가될 수 있는 모든 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="d534a-910">expression: 값의 컬렉션을 반환하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="d534a-911">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="d534a-912">만료되지 않은 userCertificate 다중값 특성의 인증서 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="d534a-913">With</span><span class="sxs-lookup"><span data-stu-id="d534a-913">With</span></span>
<span data-ttu-id="d534a-914">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-914">**Description:**</span></span>  
<span data-ttu-id="d534a-915">With 함수는 복합 식에서 한 번 이상 나타나는 하위 식을 변수로 표현하여 복합 식을 단순화하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="d534a-916">**구문:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="d534a-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="d534a-917">variable: 하위 식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="d534a-918">subExpression: 변수로 표현되는 하위 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="d534a-919">complexExpression: 복합 식입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="d534a-920">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="d534a-921">기능적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="d534a-922">userCertificate 특성에서 만료되지 않은 인증서 값만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="d534a-923">Word</span><span class="sxs-lookup"><span data-stu-id="d534a-923">Word</span></span>
<span data-ttu-id="d534a-924">**설명:**</span><span class="sxs-lookup"><span data-stu-id="d534a-924">**Description:**</span></span>  
<span data-ttu-id="d534a-925">Word 함수는 사용할 구분 기호를 설명하는 매개 변수에 따라 문자열 내에 포함된 단어와 반환할 단어 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="d534a-926">**구문:**</span><span class="sxs-lookup"><span data-stu-id="d534a-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="d534a-927">string: 단어를 반환할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="d534a-928">WordNumber: 반환해야 하는 단어 수를 식별하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="d534a-929">delimiters : 단어를 식별하는데 사용될 구분 기호를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="d534a-930">**설명**</span><span class="sxs-lookup"><span data-stu-id="d534a-930">**Remarks:**</span></span>  
<span data-ttu-id="d534a-931">구분 기호 내의 문자 중 하나로 구분되는 전체 문자열의 각 문자열은 단어로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="d534a-932">숫자가 < 1인경우 , 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="d534a-933">문자열이 null이면, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="d534a-934">문자열이 단어 수보다 적거나, 구분 기호로 식별되는 단어를 포함할 경우, 빈 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="d534a-935">**예제:**</span><span class="sxs-lookup"><span data-stu-id="d534a-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="d534a-936">"brown"을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="d534a-937">"has"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d534a-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d534a-938">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d534a-938">Additional Resources</span></span>
* [<span data-ttu-id="d534a-939">선언적 프로비전 식 이해</span><span class="sxs-lookup"><span data-stu-id="d534a-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="d534a-940">Azure AD Connect Sync: 사용자 지정 동기화 옵션</span><span class="sxs-lookup"><span data-stu-id="d534a-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="d534a-941">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="d534a-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
