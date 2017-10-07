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
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="4aa0b-103">Azure AD 동기화 연결: 함수 참조</span><span class="sxs-lookup"><span data-stu-id="4aa0b-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="4aa0b-104">Azure AD Connect의 기능은 동기화 하는 동안 사용 되는 toomanipulate 특성 값에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="4aa0b-105">hello hello 함수의 구문 형식에 따라 hello를 사용 하 여 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="4aa0b-106">함수가 과부하되거나 여러 구문을 허용한 경우, 모든 사용한 구문의 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="4aa0b-107">hello 함수는 강력한 형식이 지정 하 고 일치 하는 항목 hello 설명 형식에 전달 된 hello 형식 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="4aa0b-108">Hello 형식이 일치 하지 않는 경우 오류가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="4aa0b-109">hello 형식이 구문 다음 hello로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="4aa0b-110">**bin** -이진</span><span class="sxs-lookup"><span data-stu-id="4aa0b-110">**bin** – Binary</span></span>
* <span data-ttu-id="4aa0b-111">**bool** -부울</span><span class="sxs-lookup"><span data-stu-id="4aa0b-111">**bool** – Boolean</span></span>
* <span data-ttu-id="4aa0b-112">**dt** – UTC 날짜/시간</span><span class="sxs-lookup"><span data-stu-id="4aa0b-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="4aa0b-113">**enum** – 알려진 상수의 열거형</span><span class="sxs-lookup"><span data-stu-id="4aa0b-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="4aa0b-114">**exp** – 식을 tooevaluate tooa 부울 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="4aa0b-115">**mvbin** – 다중값의 이진</span><span class="sxs-lookup"><span data-stu-id="4aa0b-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="4aa0b-116">**mvstr** – 다중 값 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="4aa0b-117">**mvref** – 다중 값 참조</span><span class="sxs-lookup"><span data-stu-id="4aa0b-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="4aa0b-118">**num** – 숫자</span><span class="sxs-lookup"><span data-stu-id="4aa0b-118">**num** – Numeric</span></span>
* <span data-ttu-id="4aa0b-119">**ref** – 참조</span><span class="sxs-lookup"><span data-stu-id="4aa0b-119">**ref** – Reference</span></span>
* <span data-ttu-id="4aa0b-120">**str** - 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-120">**str** – String</span></span>
* <span data-ttu-id="4aa0b-121">**var** – 거의 모든 다른 형식의 변수</span><span class="sxs-lookup"><span data-stu-id="4aa0b-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="4aa0b-122">**void** – 값을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="4aa0b-123">hello 형식과 함수 hello **mvbin**, **mvstr**, 및 **mvref** 다중 값된 특성에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="4aa0b-124">**bin**, **str** 및 **ref**를 포함한 함수는 단일값 및 다중값 특성에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="4aa0b-125">함수 참조</span><span class="sxs-lookup"><span data-stu-id="4aa0b-125">Functions Reference</span></span>
| <span data-ttu-id="4aa0b-126">함수 목록</span><span class="sxs-lookup"><span data-stu-id="4aa0b-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4aa0b-127">**인증서**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="4aa0b-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="4aa0b-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="4aa0b-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="4aa0b-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="4aa0b-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="4aa0b-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="4aa0b-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="4aa0b-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="4aa0b-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="4aa0b-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="4aa0b-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="4aa0b-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="4aa0b-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="4aa0b-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="4aa0b-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="4aa0b-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="4aa0b-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="4aa0b-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="4aa0b-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="4aa0b-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="4aa0b-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="4aa0b-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="4aa0b-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="4aa0b-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="4aa0b-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="4aa0b-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="4aa0b-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="4aa0b-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="4aa0b-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="4aa0b-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="4aa0b-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="4aa0b-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="4aa0b-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="4aa0b-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="4aa0b-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="4aa0b-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="4aa0b-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="4aa0b-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="4aa0b-150">**변환**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-151">CBool</span><span class="sxs-lookup"><span data-stu-id="4aa0b-151">CBool</span></span>](#cbool) |[<span data-ttu-id="4aa0b-152">CDate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-152">CDate</span></span>](#cdate) |[<span data-ttu-id="4aa0b-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="4aa0b-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="4aa0b-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="4aa0b-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="4aa0b-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="4aa0b-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4aa0b-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="4aa0b-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4aa0b-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="4aa0b-158">CNum</span><span class="sxs-lookup"><span data-stu-id="4aa0b-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="4aa0b-159">CRef</span><span class="sxs-lookup"><span data-stu-id="4aa0b-159">CRef</span></span>](#cref) |[<span data-ttu-id="4aa0b-160">CStr</span><span class="sxs-lookup"><span data-stu-id="4aa0b-160">CStr</span></span>](#cstr) |[<span data-ttu-id="4aa0b-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="4aa0b-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="4aa0b-163">**Date / Time**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="4aa0b-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="4aa0b-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="4aa0b-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="4aa0b-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="4aa0b-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="4aa0b-167">Now</span><span class="sxs-lookup"><span data-stu-id="4aa0b-167">Now</span></span>](#now) | |
| [<span data-ttu-id="4aa0b-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="4aa0b-169">**디렉터리**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="4aa0b-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="4aa0b-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="4aa0b-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="4aa0b-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="4aa0b-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="4aa0b-173">**평가**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="4aa0b-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="4aa0b-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="4aa0b-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="4aa0b-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="4aa0b-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="4aa0b-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="4aa0b-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="4aa0b-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="4aa0b-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="4aa0b-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="4aa0b-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="4aa0b-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="4aa0b-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="4aa0b-182">IsString</span><span class="sxs-lookup"><span data-stu-id="4aa0b-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="4aa0b-183">**Math**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="4aa0b-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="4aa0b-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="4aa0b-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="4aa0b-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="4aa0b-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="4aa0b-187">**다중값**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-188">포함</span><span class="sxs-lookup"><span data-stu-id="4aa0b-188">Contains</span></span>](#contains) |[<span data-ttu-id="4aa0b-189">개수</span><span class="sxs-lookup"><span data-stu-id="4aa0b-189">Count</span></span>](#count) |[<span data-ttu-id="4aa0b-190">항목</span><span class="sxs-lookup"><span data-stu-id="4aa0b-190">Item</span></span>](#item) |[<span data-ttu-id="4aa0b-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="4aa0b-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="4aa0b-192">Join</span><span class="sxs-lookup"><span data-stu-id="4aa0b-192">Join</span></span>](#join) |[<span data-ttu-id="4aa0b-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="4aa0b-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="4aa0b-194">분할</span><span class="sxs-lookup"><span data-stu-id="4aa0b-194">Split</span></span>](#split) | | |
| <span data-ttu-id="4aa0b-195">**Program Flow**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-196">오류</span><span class="sxs-lookup"><span data-stu-id="4aa0b-196">Error</span></span>](#error) |[<span data-ttu-id="4aa0b-197">IIF</span><span class="sxs-lookup"><span data-stu-id="4aa0b-197">IIF</span></span>](#iif) |[<span data-ttu-id="4aa0b-198">선택</span><span class="sxs-lookup"><span data-stu-id="4aa0b-198">Select</span></span>](#select) |[<span data-ttu-id="4aa0b-199">Switch</span><span class="sxs-lookup"><span data-stu-id="4aa0b-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="4aa0b-200">Where</span><span class="sxs-lookup"><span data-stu-id="4aa0b-200">Where</span></span>](#where) |[<span data-ttu-id="4aa0b-201">With</span><span class="sxs-lookup"><span data-stu-id="4aa0b-201">With</span></span>](#with) | | | |
| <span data-ttu-id="4aa0b-202">**Text**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="4aa0b-203">GUID</span><span class="sxs-lookup"><span data-stu-id="4aa0b-203">GUID</span></span>](#guid) |[<span data-ttu-id="4aa0b-204">InStr</span><span class="sxs-lookup"><span data-stu-id="4aa0b-204">InStr</span></span>](#instr) |[<span data-ttu-id="4aa0b-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="4aa0b-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="4aa0b-206">LCase</span><span class="sxs-lookup"><span data-stu-id="4aa0b-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="4aa0b-207">Left</span><span class="sxs-lookup"><span data-stu-id="4aa0b-207">Left</span></span>](#left) |[<span data-ttu-id="4aa0b-208">Len</span><span class="sxs-lookup"><span data-stu-id="4aa0b-208">Len</span></span>](#len) |[<span data-ttu-id="4aa0b-209">LTrim.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="4aa0b-210">Mid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="4aa0b-211">padLeft</span><span class="sxs-lookup"><span data-stu-id="4aa0b-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="4aa0b-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="4aa0b-212">PadRight</span></span>](#padright) |[<span data-ttu-id="4aa0b-213">PCase</span><span class="sxs-lookup"><span data-stu-id="4aa0b-213">PCase</span></span>](#pcase) |[<span data-ttu-id="4aa0b-214">Replace</span><span class="sxs-lookup"><span data-stu-id="4aa0b-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="4aa0b-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="4aa0b-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="4aa0b-216">Right</span><span class="sxs-lookup"><span data-stu-id="4aa0b-216">Right</span></span>](#right) |[<span data-ttu-id="4aa0b-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="4aa0b-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="4aa0b-218">Trim</span><span class="sxs-lookup"><span data-stu-id="4aa0b-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="4aa0b-219">UCase</span><span class="sxs-lookup"><span data-stu-id="4aa0b-219">UCase</span></span>](#ucase) |[<span data-ttu-id="4aa0b-220">Word</span><span class="sxs-lookup"><span data-stu-id="4aa0b-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="4aa0b-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="4aa0b-221">BitAnd</span></span>
<span data-ttu-id="4aa0b-222">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-222">**Description:**</span></span>  
<span data-ttu-id="4aa0b-223">hello BitAnd 함수는 값에 지정 된 비트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="4aa0b-224">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="4aa0b-225">value1, value2: 숫자 값은 AND와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="4aa0b-226">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-226">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-227">이 함수는 두 매개 변수 toohello 이진 표현을 변환 하 고 비트를 설정:</span><span class="sxs-lookup"><span data-stu-id="4aa0b-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="4aa0b-228">0-하나 또는 둘 다의 해당 비트 hello *마스크* 및 *플래그* 0</span><span class="sxs-lookup"><span data-stu-id="4aa0b-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="4aa0b-229">1-경우 hello 해당 비트가 모두 1입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="4aa0b-230">즉, 두 매개 변수의 해당 비트가 hello 1 경우를 제외 하 고 모든 경우에 0을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="4aa0b-231">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="4aa0b-232">16 진수 "F"와 "F7" toothis 값을 계산 하기 때문에 7을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="4aa0b-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="4aa0b-233">BitOr</span></span>
<span data-ttu-id="4aa0b-234">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-234">**Description:**</span></span>  
<span data-ttu-id="4aa0b-235">hello BitOr 함수는 값에 지정 된 비트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="4aa0b-236">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="4aa0b-237">value1, value2: 숫자 값은 OR과 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="4aa0b-238">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-238">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-239">이 함수는 두 매개 변수 toohello 이진 표현으로 변환 하며 하나 이상이 포인터인 경우 hello 마스크 및 플래그의 해당 비트의 1 세대 및 too0 hello 해당 비트의 둘 다 0 인 경우 비트 too1를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="4aa0b-240">즉, 두 매개 변수의 해당 비트가 hello는 0을 제외한 모든 경우에 1을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="4aa0b-241">CBool</span><span class="sxs-lookup"><span data-stu-id="4aa0b-241">CBool</span></span>
<span data-ttu-id="4aa0b-242">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-242">**Description:**</span></span>  
<span data-ttu-id="4aa0b-243">CBool 함수 hello hello 평가 식을 기반으로 하는 부울을 반환</span><span class="sxs-lookup"><span data-stu-id="4aa0b-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="4aa0b-244">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="4aa0b-245">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-245">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-246">Hello 식이 계산 되 면 tooa 0이 아닌 값을 다음 CBool 반환 True, 그렇지 않으면 False를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="4aa0b-247">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="4aa0b-248">True 이면 두 특성에는 반환 hello 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="4aa0b-249">CDate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-249">CDate</span></span>
<span data-ttu-id="4aa0b-250">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-250">**Description:**</span></span>  
<span data-ttu-id="4aa0b-251">hello CDate 함수는 문자열에서 UTC 날짜 및 시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="4aa0b-252">날짜/시간은 동기화 내의 네이티브 특성 형식이 아니지만 일부 함수에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="4aa0b-253">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="4aa0b-254">값: 날짜, 시간 및 임의적 시간대 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="4aa0b-255">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-255">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-256">hello 반환 문자열은 항상 utc에서입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="4aa0b-257">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="4aa0b-258">Hello 직원의 시작 시간을 기반으로 날짜/시간을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="4aa0b-259">"2013-01-11 12:00 AM"을 나타내는 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="4aa0b-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="4aa0b-260">CertExtensionOids</span></span>
<span data-ttu-id="4aa0b-261">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-261">**Description:**</span></span>  
<span data-ttu-id="4aa0b-262">반환 hello 인증서 개체의 모든 hello 중요 한 확장의 Oid 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="4aa0b-263">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-264">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-265">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="4aa0b-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="4aa0b-266">CertFormat</span></span>
<span data-ttu-id="4aa0b-267">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-267">**Description:**</span></span>  
<span data-ttu-id="4aa0b-268">반환 hello hello 형식이 X.509v3 인증서의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="4aa0b-269">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-270">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-271">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="4aa0b-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="4aa0b-272">CertFriendlyName</span></span>
<span data-ttu-id="4aa0b-273">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-273">**Description:**</span></span>  
<span data-ttu-id="4aa0b-274">인증서에 대 한 별칭에 연결 하는 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="4aa0b-275">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-276">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-277">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="4aa0b-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="4aa0b-278">CertHashString</span></span>
<span data-ttu-id="4aa0b-279">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-279">**Description:**</span></span>  
<span data-ttu-id="4aa0b-280">Hello X.509v3 인증서에 대 한 SHA1 해시 값을 16 진 문자열로 hello 하는 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="4aa0b-281">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-282">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-283">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="4aa0b-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="4aa0b-284">CertIssuer</span></span>
<span data-ttu-id="4aa0b-285">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-285">**Description:**</span></span>  
<span data-ttu-id="4aa0b-286">반환 hello hello X.509v3 인증서를 발급 한 hello 인증 기관의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="4aa0b-287">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-288">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-289">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="4aa0b-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="4aa0b-290">CertIssuerDN</span></span>
<span data-ttu-id="4aa0b-291">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-291">**Description:**</span></span>  
<span data-ttu-id="4aa0b-292">반환 hello hello 인증서 발급자의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="4aa0b-293">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-294">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-295">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="4aa0b-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-296">CertIssuerOid</span></span>
<span data-ttu-id="4aa0b-297">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-297">**Description:**</span></span>  
<span data-ttu-id="4aa0b-298">반환 hello hello 인증서 발급자의 Oid 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="4aa0b-299">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-300">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-301">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="4aa0b-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="4aa0b-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="4aa0b-303">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-303">**Description:**</span></span>  
<span data-ttu-id="4aa0b-304">이 X.509v3 인증서에 대 한 문자열 hello 키 알고리즘 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="4aa0b-305">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-306">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-307">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="4aa0b-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="4aa0b-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="4aa0b-309">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-309">**Description:**</span></span>  
<span data-ttu-id="4aa0b-310">16 진 문자열 hello X.509v3 인증서에 대 한 hello 키 알고리즘 매개 변수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="4aa0b-311">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-312">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-313">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="4aa0b-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="4aa0b-314">CertNameInfo</span></span>
<span data-ttu-id="4aa0b-315">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-315">**Description:**</span></span>  
<span data-ttu-id="4aa0b-316">Hello 제목과 발급자 이름을 반환 인증서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="4aa0b-317">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="4aa0b-318">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-319">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="4aa0b-320">X509NameType: hello hello 주체에 대 한 X509NameType 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="4aa0b-321">includesIssuerName: true tooinclude hello 발급자 이름입니다. 그렇지 않으면 false입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="4aa0b-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="4aa0b-322">CertNotAfter</span></span>
<span data-ttu-id="4aa0b-323">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-323">**Description:**</span></span>  
<span data-ttu-id="4aa0b-324">Hello 날짜 이후에 인증서가 더 이상 유효 현지 시간으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="4aa0b-325">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-326">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-327">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="4aa0b-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="4aa0b-328">CertNotBefore</span></span>
<span data-ttu-id="4aa0b-329">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-329">**Description:**</span></span>  
<span data-ttu-id="4aa0b-330">인증서가 유효 하는 현지 시간으로 hello 날짜를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="4aa0b-331">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-332">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-333">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="4aa0b-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-334">CertPublicKeyOid</span></span>
<span data-ttu-id="4aa0b-335">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-335">**Description:**</span></span>  
<span data-ttu-id="4aa0b-336">반환 hello hello hello X.509v3 인증서에 대 한 공개 키의 Oid 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="4aa0b-337">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-338">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-339">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="4aa0b-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="4aa0b-341">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-341">**Description:**</span></span>  
<span data-ttu-id="4aa0b-342">반환 hello hello 공개 키 매개 변수 hello X.509v3 인증서에 대 한 Oid 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="4aa0b-343">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-344">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-345">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="4aa0b-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="4aa0b-346">CertSerialNumber</span></span>
<span data-ttu-id="4aa0b-347">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-347">**Description:**</span></span>  
<span data-ttu-id="4aa0b-348">Hello X.509v3 인증서의 hello 일련 번호를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="4aa0b-349">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-350">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-351">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="4aa0b-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="4aa0b-353">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-353">**Description:**</span></span>  
<span data-ttu-id="4aa0b-354">반환 hello hello 알고리즘의 Oid는 인증서의 toocreate hello 서명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="4aa0b-355">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-356">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-357">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="4aa0b-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="4aa0b-358">CertSubject</span></span>
<span data-ttu-id="4aa0b-359">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-359">**Description:**</span></span>  
<span data-ttu-id="4aa0b-360">가져옵니다 hello 인증서에서 주체 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="4aa0b-361">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-362">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-363">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="4aa0b-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="4aa0b-364">CertSubjectNameDN</span></span>
<span data-ttu-id="4aa0b-365">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-365">**Description:**</span></span>  
<span data-ttu-id="4aa0b-366">반환 hello 인증서에서 주체 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="4aa0b-367">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-368">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-369">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="4aa0b-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-370">CertSubjectNameOid</span></span>
<span data-ttu-id="4aa0b-371">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-371">**Description:**</span></span>  
<span data-ttu-id="4aa0b-372">반환 hello Oid hello 인증서 주체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="4aa0b-373">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-374">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-375">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="4aa0b-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="4aa0b-376">CertThumbprint</span></span>
<span data-ttu-id="4aa0b-377">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-377">**Description:**</span></span>  
<span data-ttu-id="4aa0b-378">인증서의 hello 지문을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="4aa0b-379">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-380">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-381">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="4aa0b-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="4aa0b-382">CertVersion</span></span>
<span data-ttu-id="4aa0b-383">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-383">**Description:**</span></span>  
<span data-ttu-id="4aa0b-384">반환 되는 인증서의 X.509 형식 버전을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="4aa0b-385">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-386">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-387">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="4aa0b-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-388">CGuid</span></span>
<span data-ttu-id="4aa0b-389">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-389">**Description:**</span></span>  
<span data-ttu-id="4aa0b-390">CGuid 함수 hello tooits 이진 표현 GUID의 hello 문자열 표현으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="4aa0b-391">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="4aa0b-392">이 패턴에서 문자열 서식: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 또는 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="4aa0b-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="4aa0b-393">포함</span><span class="sxs-lookup"><span data-stu-id="4aa0b-393">Contains</span></span>
<span data-ttu-id="4aa0b-394">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-394">**Description:**</span></span>  
<span data-ttu-id="4aa0b-395">hello Contains 함수는 다중값된 특성 안에서 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="4aa0b-396">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-396">**Syntax:**</span></span>  
<span data-ttu-id="4aa0b-397">`num Contains (mvstring attribute, str search)` - 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="4aa0b-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="4aa0b-398">`num Contains (mvref attribute, str search)` - 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="4aa0b-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="4aa0b-399">특성: hello 다중값된 특성 toosearch 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="4aa0b-400">검색: toofind hello 특성에는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="4aa0b-401">대소문자 유형: 대소문자를 구분하거나 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="4aa0b-402">Hello 문자열을 찾을 수 hello 다중값된 특성의 인덱스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="4aa0b-403">hello 문자열을 찾을 수 없는 경우 0이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="4aa0b-404">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-404">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-405">다중값된 문자열 특성에 대 한 hello 검색 hello 값에서 부분 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="4aa0b-406">참조 특성에 대 한 hello 검색된 되는 문자열 정확히 일치 해야 hello 값 toobe 일치로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="4aa0b-407">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="4aa0b-408">Hello / / proxyAddresses 특성에 기본 전자 메일 주소가 있는 경우 (가리키는 대문자 "SMTP:"), 돌아 오세요 hello / / proxyAddress 특성, 그렇지 않으면 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="4aa0b-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="4aa0b-409">ConvertFromBase64</span></span>
<span data-ttu-id="4aa0b-410">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-410">**Description:**</span></span>  
<span data-ttu-id="4aa0b-411">hello ConvertFromBase64 함수 변환 hello는 base64 인코딩 값 tooa 일반 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="4aa0b-412">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-412">**Syntax:**</span></span>  
<span data-ttu-id="4aa0b-413">`str ConvertFromBase64(str source)` - 인코딩에 유니코드 가정</span><span class="sxs-lookup"><span data-stu-id="4aa0b-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="4aa0b-414">원본: Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="4aa0b-415">인코딩: 유니코드, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="4aa0b-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="4aa0b-416">**예제**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="4aa0b-417">두 예제 모두 "*Hello world!*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="4aa0b-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4aa0b-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="4aa0b-419">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-419">**Description:**</span></span>  
<span data-ttu-id="4aa0b-420">hello ConvertFromUTF8Hex 함수 변환 hello는 UTF8 16 진수 인코딩 값 tooa 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="4aa0b-421">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="4aa0b-422">원본: UTF8 2-바이트 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="4aa0b-423">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-423">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-424">해당 hello 결과에서이 함수와 ConvertFromBase64([],UTF8) hello 차이점은 hello DN 특성에 대 한 친숙 한입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="4aa0b-425">이 형식은 DN으로 Azure Active Directory에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="4aa0b-426">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="4aa0b-427">"*Hello world!*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="4aa0b-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="4aa0b-428">ConvertToBase64</span></span>
<span data-ttu-id="4aa0b-429">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-429">**Description:**</span></span>  
<span data-ttu-id="4aa0b-430">ConvertToBase64 함수 hello 문자열 tooa 유니코드 base64 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="4aa0b-431">Hello 값 배열 base-64 숫자로 인코딩된 정수 tooits 문자열 표현으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="4aa0b-432">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="4aa0b-433">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="4aa0b-434">"SABlAGwAbABvACAAdwBvAHIAbABkACEA"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="4aa0b-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4aa0b-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="4aa0b-436">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-436">**Description:**</span></span>  
<span data-ttu-id="4aa0b-437">ConvertToUTF8Hex 함수 hello 문자열 tooa UTF8 16 진수 인코딩 값으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="4aa0b-438">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="4aa0b-439">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-439">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-440">이 함수의 hello 출력 형식은 DN 특성 형식으로 Azure Active Directory에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="4aa0b-441">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="4aa0b-442">48656C6C6F20776F726C6421을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="4aa0b-443">개수</span><span class="sxs-lookup"><span data-stu-id="4aa0b-443">Count</span></span>
<span data-ttu-id="4aa0b-444">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-444">**Description:**</span></span>  
<span data-ttu-id="4aa0b-445">Count 함수 hello 다중 값된 특성에 hello 수의 요소를 반환</span><span class="sxs-lookup"><span data-stu-id="4aa0b-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="4aa0b-446">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="4aa0b-447">CNum</span><span class="sxs-lookup"><span data-stu-id="4aa0b-447">CNum</span></span>
<span data-ttu-id="4aa0b-448">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-448">**Description:**</span></span>  
<span data-ttu-id="4aa0b-449">hello CNum 함수는 문자열을 숫자 데이터 형식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="4aa0b-450">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="4aa0b-451">CRef</span><span class="sxs-lookup"><span data-stu-id="4aa0b-451">CRef</span></span>
<span data-ttu-id="4aa0b-452">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-452">**Description:**</span></span>  
<span data-ttu-id="4aa0b-453">문자열 tooa 참조 특성으로 변환</span><span class="sxs-lookup"><span data-stu-id="4aa0b-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="4aa0b-454">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="4aa0b-455">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="4aa0b-456">CStr</span><span class="sxs-lookup"><span data-stu-id="4aa0b-456">CStr</span></span>
<span data-ttu-id="4aa0b-457">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-457">**Description:**</span></span>  
<span data-ttu-id="4aa0b-458">CStr 함수 hello tooa 문자열 데이터 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="4aa0b-459">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="4aa0b-460">값: 숫자 값, 참조 특성 또는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="4aa0b-461">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="4aa0b-462">"cn=Joe,dc=contoso,dc=com"을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="4aa0b-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="4aa0b-463">DateAdd</span></span>
<span data-ttu-id="4aa0b-464">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-464">**Description:**</span></span>  
<span data-ttu-id="4aa0b-465">지정 된 시간 간격이 추가 된 날짜 toowhich를 포함 하는 날짜를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="4aa0b-466">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="4aa0b-467">간격: hello 간격 tooadd 시간에 해당 하는 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="4aa0b-468">hello 문자열 hello를 다음 값 중 하나에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="4aa0b-469">yyyy 년</span><span class="sxs-lookup"><span data-stu-id="4aa0b-469">yyyy Year</span></span>
  * <span data-ttu-id="4aa0b-470">q 분기</span><span class="sxs-lookup"><span data-stu-id="4aa0b-470">q Quarter</span></span>
  * <span data-ttu-id="4aa0b-471">m 월</span><span class="sxs-lookup"><span data-stu-id="4aa0b-471">m Month</span></span>
  * <span data-ttu-id="4aa0b-472">y 연간 일자</span><span class="sxs-lookup"><span data-stu-id="4aa0b-472">y Day of year</span></span>
  * <span data-ttu-id="4aa0b-473">d 일</span><span class="sxs-lookup"><span data-stu-id="4aa0b-473">d Day</span></span>
  * <span data-ttu-id="4aa0b-474">w 요일</span><span class="sxs-lookup"><span data-stu-id="4aa0b-474">w Weekday</span></span>
  * <span data-ttu-id="4aa0b-475">ww 주</span><span class="sxs-lookup"><span data-stu-id="4aa0b-475">ww Week</span></span>
  * <span data-ttu-id="4aa0b-476">h 시간</span><span class="sxs-lookup"><span data-stu-id="4aa0b-476">h Hour</span></span>
  * <span data-ttu-id="4aa0b-477">n 분</span><span class="sxs-lookup"><span data-stu-id="4aa0b-477">n Minute</span></span>
  * <span data-ttu-id="4aa0b-478">s 초</span><span class="sxs-lookup"><span data-stu-id="4aa0b-478">s Second</span></span>
* <span data-ttu-id="4aa0b-479">값: 수 hello 원하는 tooadd 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="4aa0b-480">양수 수 있습니다 (tooget 날짜 이후 hello) 또는 음수 (과거 hello tooget 날짜).</span><span class="sxs-lookup"><span data-stu-id="4aa0b-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="4aa0b-481">날짜: 날짜/시간을 나타내는 날짜 toowhich hello 간격은 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="4aa0b-482">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="4aa0b-483">3개월을 추가하고 "2001-04-01"을 나타내는 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="4aa0b-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="4aa0b-484">DateFromNum</span></span>
<span data-ttu-id="4aa0b-485">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-485">**Description:**</span></span>  
<span data-ttu-id="4aa0b-486">DateFromNum 함수 hello AD의 날짜 형식 tooa DateTime 형식 값으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="4aa0b-487">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="4aa0b-488">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="4aa0b-489">2012-01-01 23:00:00을 나타내는 날짜/시간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="4aa0b-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="4aa0b-490">DNComponent</span></span>
<span data-ttu-id="4aa0b-491">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-491">**Description:**</span></span>  
<span data-ttu-id="4aa0b-492">hello DNComponent 함수는 지정된 된 DN 구성 왼쪽에서의 hello 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="4aa0b-493">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="4aa0b-494">dn: hello 참조 특성 toointerpret</span><span class="sxs-lookup"><span data-stu-id="4aa0b-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="4aa0b-495">Hello DN tooreturn ComponentNumber: hello 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4aa0b-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="4aa0b-496">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="4aa0b-497">dn이 "cn=Joe,ou=…"인 경우 Joe를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="4aa0b-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="4aa0b-498">DNComponentRev</span></span>
<span data-ttu-id="4aa0b-499">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-499">**Description:**</span></span>  
<span data-ttu-id="4aa0b-500">hello DNComponentRev 함수는 지정된 된 DN 구성 오른쪽 (끝 hello)에서 hello 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="4aa0b-501">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="4aa0b-502">dn: hello 참조 특성 toointerpret</span><span class="sxs-lookup"><span data-stu-id="4aa0b-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="4aa0b-503">ComponentNumber-hello DN tooreturn의 hello 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4aa0b-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="4aa0b-504">옵션: DC –"dc ="가 있는 모든 구성 요소를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="4aa0b-505">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-505">**Example:**</span></span>  
<span data-ttu-id="4aa0b-506">dn이 "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"인 경우</span><span class="sxs-lookup"><span data-stu-id="4aa0b-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="4aa0b-507">모두 US를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="4aa0b-508">오류</span><span class="sxs-lookup"><span data-stu-id="4aa0b-508">Error</span></span>
<span data-ttu-id="4aa0b-509">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-509">**Description:**</span></span>  
<span data-ttu-id="4aa0b-510">hello 오차 함수는 사용 되는 tooreturn 사용자 지정 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="4aa0b-511">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="4aa0b-512">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="4aa0b-513">Hello / / accountName 특성이 없는 경우 hello 개체에서 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="4aa0b-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="4aa0b-514">EscapeDNComponent</span></span>
<span data-ttu-id="4aa0b-515">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-515">**Description:**</span></span>  
<span data-ttu-id="4aa0b-516">hello EscapeDNComponent 함수는 DN 중 하나의 구성 요소를 받아서 LDAP에 나타낼 수 있도록 이스케이프 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="4aa0b-517">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="4aa0b-518">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="4aa0b-519">실행 하면 hello / / displayName 특성에 문자가 LDAP에서 이스케이프 해야 하는 경우에 LDAP 디렉터리에서 hello 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="4aa0b-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="4aa0b-520">FormatDateTime</span></span>
<span data-ttu-id="4aa0b-521">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-521">**Description:**</span></span>  
<span data-ttu-id="4aa0b-522">hello FormatDateTime 함수는 사용 되는 tooformat 지정 된 형식으로 DateTime tooa 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="4aa0b-523">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="4aa0b-524">값: hello 날짜/시간 형식의 값을</span><span class="sxs-lookup"><span data-stu-id="4aa0b-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="4aa0b-525">형식: hello 형식 tooconvert를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="4aa0b-526">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-526">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-527">hello 형식을 확인할 수 있습니다에 대 한 가능한 값을 hello: [사용자 정의 날짜/시간 형식 (Format 함수)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="4aa0b-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="4aa0b-528">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="4aa0b-529">"2007-12-25"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="4aa0b-530">"20140905081453.0Z"를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="4aa0b-531">GUID</span><span class="sxs-lookup"><span data-stu-id="4aa0b-531">GUID</span></span>
<span data-ttu-id="4aa0b-532">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-532">**Description:**</span></span>  
<span data-ttu-id="4aa0b-533">새로운 임의 GUID를 생성 하는 hello 함수 GUID</span><span class="sxs-lookup"><span data-stu-id="4aa0b-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="4aa0b-534">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="4aa0b-535">IIF</span><span class="sxs-lookup"><span data-stu-id="4aa0b-535">IIF</span></span>
<span data-ttu-id="4aa0b-536">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-536">**Description:**</span></span>  
<span data-ttu-id="4aa0b-537">IIF 함수 hello 지정된 된 조건에 따라 가능한 값의 집합 중 하나를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="4aa0b-538">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="4aa0b-539">조건: tootrue 또는 false 값 이나 일 수 있는 식을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="4aa0b-540">valueIfTrue: hello hello 조건이 tootrue, 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="4aa0b-541">valueIfFalse: hello hello 조건이 toofalse, 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="4aa0b-542">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="4aa0b-543">Hello 사용자가 intern 인 경우 hello 별칭 "t-"로 사용자의 추가 toohello의 시작 부분을 다른 반환 hello 사용자의 별칭을 있는 그대로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="4aa0b-544">InStr</span><span class="sxs-lookup"><span data-stu-id="4aa0b-544">InStr</span></span>
<span data-ttu-id="4aa0b-545">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-545">**Description:**</span></span>  
<span data-ttu-id="4aa0b-546">hello InStr 함수는 문자열에서 부분 문자열의 첫 번째를 hello 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="4aa0b-547">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="4aa0b-548">stringcheck: toobe 검색 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="4aa0b-549">stringmatch: toobe 찾을 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="4aa0b-550">시작: 위치 toofind hello 부분 문자열 시작</span><span class="sxs-lookup"><span data-stu-id="4aa0b-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="4aa0b-551">compare: vbTextCompare 또는 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="4aa0b-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="4aa0b-552">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-552">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-553">Hello 부분 문자열이 있는 반환 hello 위치 또는 인 경우 0 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="4aa0b-554">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="4aa0b-555">Evalues too5</span><span class="sxs-lookup"><span data-stu-id="4aa0b-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="4aa0b-556">Too7 평가</span><span class="sxs-lookup"><span data-stu-id="4aa0b-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="4aa0b-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="4aa0b-557">InStrRev</span></span>
<span data-ttu-id="4aa0b-558">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-558">**Description:**</span></span>  
<span data-ttu-id="4aa0b-559">hello InStrRev 함수는 문자열에서 하위 문자열의 마지막 항목과를 hello 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="4aa0b-560">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="4aa0b-561">stringcheck: toobe 검색 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="4aa0b-562">stringmatch: toobe 찾을 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="4aa0b-563">시작: 위치 toofind hello 부분 문자열 시작</span><span class="sxs-lookup"><span data-stu-id="4aa0b-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="4aa0b-564">compare: vbTextCompare 또는 vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="4aa0b-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="4aa0b-565">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-565">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-566">Hello 부분 문자열이 있는 반환 hello 위치 또는 인 경우 0 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="4aa0b-567">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="4aa0b-568">7을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="4aa0b-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="4aa0b-569">IsBitSet</span></span>
<span data-ttu-id="4aa0b-570">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-570">**Description:**</span></span>  
<span data-ttu-id="4aa0b-571">hello 약간 설정 되었는지 아닌지를 테스트 IsBitSet 함수</span><span class="sxs-lookup"><span data-stu-id="4aa0b-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="4aa0b-572">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="4aa0b-573">값: flag 하는 숫자 값: hello 있는 숫자 값을 비트 toobe 평가</span><span class="sxs-lookup"><span data-stu-id="4aa0b-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="4aa0b-574">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="4aa0b-575">"4" 비트가 16 진수 값 hello "F"으로 설정 되어 있으므로 True를 반환</span><span class="sxs-lookup"><span data-stu-id="4aa0b-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="4aa0b-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-576">IsDate</span></span>
<span data-ttu-id="4aa0b-577">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-577">**Description:**</span></span>  
<span data-ttu-id="4aa0b-578">Hello 식 수 있으면 hello IsDate 함수 평가 tooTrue 날짜/시간 형식으로 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="4aa0b-579">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="4aa0b-580">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-580">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-581">Cdate ()이 성공 될 수 있도록 toodetermine를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="4aa0b-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="4aa0b-582">IsCert</span></span>
<span data-ttu-id="4aa0b-583">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-583">**Description:**</span></span>  
<span data-ttu-id="4aa0b-584">.NET X509Certificate2 인증서 개체에 hello 원시 데이터를 serialize 할 수 있으면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="4aa0b-585">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="4aa0b-586">certificateRawData: X.509 인증서의 바이트 배열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4aa0b-587">인코딩된 이진 (DER) 또는 Base64 인코딩된 X.509 데이터 hello 바이트 배열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="4aa0b-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="4aa0b-588">IsEmpty</span></span>
<span data-ttu-id="4aa0b-589">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-589">**Description:**</span></span>  
<span data-ttu-id="4aa0b-590">Hello 특성은 hello CS 또는 MV에에서 존재 하지만 tooan 빈 문자열을 계산을 hello IsEmpty 함수 tooTrue를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="4aa0b-591">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="4aa0b-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-592">IsGuid</span></span>
<span data-ttu-id="4aa0b-593">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-593">**Description:**</span></span>  
<span data-ttu-id="4aa0b-594">Hello 문자열 변환된 tooa GUID 수을 hello IsGuid 함수 tootrue를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="4aa0b-595">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="4aa0b-596">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-596">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-597">GUID는 다음 패턴 중 하나로 정의됩니다. xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 또는 {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="4aa0b-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="4aa0b-598">CGuid() 성공 수 있으면 toodetermine를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="4aa0b-599">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="4aa0b-600">Hello StrAttribute GUID 형식이 있으면 이진 표현을 반환, 그렇지 않으면 Null을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="4aa0b-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="4aa0b-601">IsNull</span></span>
<span data-ttu-id="4aa0b-602">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-602">**Description:**</span></span>  
<span data-ttu-id="4aa0b-603">Hello 식이 tooNull 이면 hello IsNull 함수는 true을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="4aa0b-604">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="4aa0b-605">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-605">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-606">특성에 대 한 Null hello 없을 경우 hello 특성으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="4aa0b-607">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="4aa0b-608">Hello CS 또는 MV에 hello 특성이 없을 경우 True를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="4aa0b-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="4aa0b-609">IsNullOrEmpty</span></span>
<span data-ttu-id="4aa0b-610">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-610">**Description:**</span></span>  
<span data-ttu-id="4aa0b-611">Hello 식이 null 또는 빈 문자열이 면 hello IsNullOrEmpty 함수 true 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="4aa0b-612">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="4aa0b-613">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-613">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-614">특성의 경우이 평가 tooTrue hello 특성이 없는 없거나 있지만 빈 문자열인 경우 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="4aa0b-615">이 함수의 hello 역은 ispresent 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="4aa0b-616">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="4aa0b-617">Hello 특성이 없거나 hello CS 또는 MV에서 빈 문자열인 경우 True를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="4aa0b-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="4aa0b-618">IsNumeric</span></span>
<span data-ttu-id="4aa0b-619">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-619">**Description:**</span></span>  
<span data-ttu-id="4aa0b-620">IsNumeric 함수 hello 숫자 형식으로 식이 계산 될 수 있는지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="4aa0b-621">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="4aa0b-622">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-622">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-623">CNum() 성공 tooparse hello 식 수 있으면 toodetermine를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="4aa0b-624">IsString</span><span class="sxs-lookup"><span data-stu-id="4aa0b-624">IsString</span></span>
<span data-ttu-id="4aa0b-625">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-625">**Description:**</span></span>  
<span data-ttu-id="4aa0b-626">Hello 식 수 있는 경우 수 계산된 tooa 문자열 형식, tooTrue을 평가 하는 hello IsString 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="4aa0b-627">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="4aa0b-628">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-628">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-629">있을지를 성공 tooparse hello 식 수 있으면 toodetermine를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="4aa0b-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="4aa0b-630">IsPresent</span></span>
<span data-ttu-id="4aa0b-631">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-631">**Description:**</span></span>  
<span data-ttu-id="4aa0b-632">Hello 식이 tooa 문자열을 Null이 아니고 비어 있지 않은 이면 IsPresent 함수는 true를 반환 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="4aa0b-633">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="4aa0b-634">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-634">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-635">이 함수의 hello 역은 isnullorempty 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="4aa0b-636">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="4aa0b-637">항목</span><span class="sxs-lookup"><span data-stu-id="4aa0b-637">Item</span></span>
<span data-ttu-id="4aa0b-638">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-638">**Description:**</span></span>  
<span data-ttu-id="4aa0b-639">hello Item 함수는 다중값된 문자열/특성에서 하나의 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="4aa0b-640">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="4aa0b-641">attribute: 다중값 특성</span><span class="sxs-lookup"><span data-stu-id="4aa0b-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="4aa0b-642">인덱스: hello 다중값된 문자열의 인덱스 tooan 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="4aa0b-643">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-643">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-644">hello Item 함수는 두 함수 hello hello 다중 값된 특성에 hello 인덱스 tooan 항목을 반환 하므로 hello Contains 함수와 함께 사용 하면 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="4aa0b-645">인덱스가 범위를 초과하는 경우 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="4aa0b-646">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="4aa0b-647">반환 hello 기본 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="4aa0b-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="4aa0b-648">ItemOrNull</span></span>
<span data-ttu-id="4aa0b-649">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-649">**Description:**</span></span>  
<span data-ttu-id="4aa0b-650">hello ItemOrNull 함수는 다중값된 문자열/특성에서 하나의 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="4aa0b-651">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="4aa0b-652">attribute: 다중값 특성</span><span class="sxs-lookup"><span data-stu-id="4aa0b-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="4aa0b-653">인덱스: hello 다중값된 문자열의 인덱스 tooan 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="4aa0b-654">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-654">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-655">hello ItemOrNull 함수는 두 함수 hello hello 다중 값된 특성에 hello 인덱스 tooan 항목을 반환 하므로 hello Contains 함수와 함께 사용 하면 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="4aa0b-656">인덱스가 범위를 초과하는 경우 Null 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="4aa0b-657">Join</span><span class="sxs-lookup"><span data-stu-id="4aa0b-657">Join</span></span>
<span data-ttu-id="4aa0b-658">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-658">**Description:**</span></span>  
<span data-ttu-id="4aa0b-659">hello 조인 함수는 다중값된 문자열을 지정된 구분 기호 각 항목 사이 삽입 된 단일 값 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="4aa0b-660">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="4aa0b-661">특성: toobe 조인할 문자열 포함 하는 다중 값된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="4aa0b-662">구분 기호: 모든 문자열을 사용 하는 tooseparate hello 부분 문자열이 hello 문자열을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="4aa0b-663">생략 하면 hello 공백 문자 ("") 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="4aa0b-664">경우 구분 기호가 빈 문자열 ("") 또는 없음으로 hello 목록의 모든 항목이 구분 기호 없이 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="4aa0b-665">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-665">**Remarks**</span></span>  
<span data-ttu-id="4aa0b-666">조인 hello 및 Split 함수 간에 패리티가 유지가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="4aa0b-667">hello Join 함수는 문자열의 배열을 사용 하 고 tooreturn 단일 문자열 구분 기호 문자열을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="4aa0b-668">hello Split 함수는 문자열을 구분 기호로 구분 hello, tooreturn 문자열 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="4aa0b-669">그러나 Join 함수는 모든 구분 기호 문자열을 사용하여 문자열을 연결할 수 있지만, Split 함수는 단일 문자 구분 기호를 사용하여 오직 문자열을 나눌 수만 있다는 것이 가장 중요한 차이점입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="4aa0b-670">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="4aa0b-671">"SMTP:john.doe@contoso.com,smtp:jd@contoso.com"을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="4aa0b-672">LCase</span><span class="sxs-lookup"><span data-stu-id="4aa0b-672">LCase</span></span>
<span data-ttu-id="4aa0b-673">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-673">**Description:**</span></span>  
<span data-ttu-id="4aa0b-674">LCase 함수 hello 문자열 toolower 대/소문자의 모든 문자를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="4aa0b-675">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="4aa0b-676">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="4aa0b-677">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="4aa0b-678">Left</span><span class="sxs-lookup"><span data-stu-id="4aa0b-678">Left</span></span>
<span data-ttu-id="4aa0b-679">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-679">**Description:**</span></span>  
<span data-ttu-id="4aa0b-680">hello Left 함수는 문자열의 hello 왼쪽에서 지정한 개수의 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="4aa0b-681">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="4aa0b-682">문자열: 문자열 tooreturn 문자를 hello</span><span class="sxs-lookup"><span data-stu-id="4aa0b-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="4aa0b-683">Hello (왼쪽) 문자열의 시작 부분에서 문자 tooreturn hello 수를 나타내는 숫자 NumChars:</span><span class="sxs-lookup"><span data-stu-id="4aa0b-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="4aa0b-684">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-684">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-685">Hello 문자열의 첫 번째 numChars 문자를 포함 하는 문자열:</span><span class="sxs-lookup"><span data-stu-id="4aa0b-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="4aa0b-686">numChars = 0 인 경우, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="4aa0b-687">numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="4aa0b-688">문자열이 null이면 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-688">If string is null, return empty string.</span></span>

<span data-ttu-id="4aa0b-689">문자열에 numChars에서 지정한 hello 숫자 보다 적은 문자가 포함 된, 문자열 동일한 toostring (즉, 매개 변수 1의에서 모든 문자 포함)이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="4aa0b-690">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="4aa0b-691">"Joh"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="4aa0b-692">Len</span><span class="sxs-lookup"><span data-stu-id="4aa0b-692">Len</span></span>
<span data-ttu-id="4aa0b-693">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-693">**Description:**</span></span>  
<span data-ttu-id="4aa0b-694">hello Len 함수는 문자열의 문자 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="4aa0b-695">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="4aa0b-696">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="4aa0b-697">8을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="4aa0b-698">LTrim.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-698">LTrim</span></span>
<span data-ttu-id="4aa0b-699">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-699">**Description:**</span></span>  
<span data-ttu-id="4aa0b-700">hello LTrim 함수는 문자열에서 선행 공백을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="4aa0b-701">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="4aa0b-702">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="4aa0b-703">"Test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="4aa0b-704">Mid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-704">Mid</span></span>
<span data-ttu-id="4aa0b-705">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-705">**Description:**</span></span>  
<span data-ttu-id="4aa0b-706">Mid hello 함수는 문자열의 지정된 된 위치에서 지정한 개수의 문자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="4aa0b-707">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="4aa0b-708">문자열: 문자열 tooreturn 문자를 hello</span><span class="sxs-lookup"><span data-stu-id="4aa0b-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="4aa0b-709">시작: 위치 문자열 tooreturn 문자에서 시작 하는 hello를 식별 하는 번호</span><span class="sxs-lookup"><span data-stu-id="4aa0b-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="4aa0b-710">문자열의 위치에서 문자 tooreturn hello 수를 나타내는 숫자 NumChars:</span><span class="sxs-lookup"><span data-stu-id="4aa0b-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="4aa0b-711">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-711">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-712">문자열의 시작 위치에서 시작되는 numChars 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="4aa0b-713">문자열의 start 위치에서 numChars 문자를 포함하는 문자열:</span><span class="sxs-lookup"><span data-stu-id="4aa0b-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="4aa0b-714">numChars = 0 인 경우, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="4aa0b-715">numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="4aa0b-716">하는 경우 시작 > 문자열의 길이 hello, 입력된 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="4aa0b-717">start < = 0 인 경우, 입력된 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="4aa0b-718">문자열이 null이면 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-718">If string is null, return empty string.</span></span>

<span data-ttu-id="4aa0b-719">시작 위치에서 문자열의 numChar 문자가 남아있지 않는 경우, 가능한 많은 문자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="4aa0b-720">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="4aa0b-721">"hn Do"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="4aa0b-722">"Doe"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="4aa0b-723">Now</span><span class="sxs-lookup"><span data-stu-id="4aa0b-723">Now</span></span>
<span data-ttu-id="4aa0b-724">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-724">**Description:**</span></span>  
<span data-ttu-id="4aa0b-725">hello 이제 함수 반환 tooyour 컴퓨터의 시스템 날짜 및 시간에 따라 DateTime hello 현재 날짜와 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="4aa0b-726">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="4aa0b-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-727">NumFromDate</span></span>
<span data-ttu-id="4aa0b-728">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-728">**Description:**</span></span>  
<span data-ttu-id="4aa0b-729">NumFromDate 함수 hello AD의 날짜 형식으로 날짜를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="4aa0b-730">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="4aa0b-731">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="4aa0b-732">129699324000000000을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="4aa0b-733">padLeft</span><span class="sxs-lookup"><span data-stu-id="4aa0b-733">PadLeft</span></span>
<span data-ttu-id="4aa0b-734">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-734">**Description:**</span></span>  
<span data-ttu-id="4aa0b-735">hello PadLeft 함수 왼쪽 패드 지정 된 문자열 tooa 지정된 된 패드 문자를 사용 하 여 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="4aa0b-736">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="4aa0b-737">문자열: 문자열 toopad hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-737">string: hello string toopad.</span></span>
* <span data-ttu-id="4aa0b-738">길이: 문자열의 길이 원하는 hello를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="4aa0b-739">padCharacter:는 단일 문자 toouse hello 패드 문자로 구성 된 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="4aa0b-740">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-740">**Remarks:**</span></span>

* <span data-ttu-id="4aa0b-741">Hello 길이 문자열의 길이 보다 작은 경우, 다음 padCharacter를 반복적으로 추가 된 toohello (왼쪽) 문자열의 시작 부분 길이 같으면 toolength 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="4aa0b-742">PadCharacter는 공백 문자가 될 수 있지만, null 값은 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="4aa0b-743">문자열의 길이 hello 같은 tooor 길이 보다 큰 경우 문자열이 변경 되지 않은 상태로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="4aa0b-744">문자열 길이 보다 큰 또는 같은 toolength 있으면 문자열 동일한 toostring 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="4aa0b-745">Hello 길이 문자열의 길이 보다 작은 경우 hello의 새 문자열 길이는 padCharacter로 채워진 문자열을 포함 된 원하는 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="4aa0b-746">문자열이 null 인 경우 hello 함수는 빈 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="4aa0b-747">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="4aa0b-748">"000000User"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="4aa0b-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="4aa0b-749">PadRight</span></span>
<span data-ttu-id="4aa0b-750">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-750">**Description:**</span></span>  
<span data-ttu-id="4aa0b-751">hello PadRight 함수 오른쪽 패드 지정 된 문자열 tooa 지정된 된 패드 문자를 사용 하 여 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="4aa0b-752">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="4aa0b-753">문자열: 문자열 toopad hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-753">string: hello string toopad.</span></span>
* <span data-ttu-id="4aa0b-754">길이: 문자열의 길이 원하는 hello를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="4aa0b-755">padCharacter:는 단일 문자 toouse hello 패드 문자로 구성 된 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="4aa0b-756">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-756">**Remarks:**</span></span>

* <span data-ttu-id="4aa0b-757">Hello 길이 문자열의 길이 보다 작은 경우 다음 padCharacter를 반복적으로 추가 된 toohello 끝 (오른쪽) 문자열 길이 같으면 toolength 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="4aa0b-758">PadCharacter는 공백 문자가 될 수 있지만, null 값은 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="4aa0b-759">문자열의 길이 hello 같은 tooor 길이 보다 큰 경우 문자열이 변경 되지 않은 상태로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="4aa0b-760">문자열 길이 보다 큰 또는 같은 toolength 있으면 문자열 동일한 toostring 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="4aa0b-761">Hello 길이 문자열의 길이 보다 작은 경우 hello의 새 문자열 길이는 padCharacter로 채워진 문자열을 포함 된 원하는 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="4aa0b-762">문자열이 null 인 경우 hello 함수는 빈 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="4aa0b-763">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="4aa0b-764">"User000000"을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="4aa0b-765">PCase</span><span class="sxs-lookup"><span data-stu-id="4aa0b-765">PCase</span></span>
<span data-ttu-id="4aa0b-766">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-766">**Description:**</span></span>  
<span data-ttu-id="4aa0b-767">PCase 함수 hello hello 문자열 tooupper 경우에서 각 공백으로 구분 된 단어의 첫 번째 문자를 변환 하 고 다른 모든 문자를 변환할지 toolower 대/소문자입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="4aa0b-768">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="4aa0b-769">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-769">**Remarks:**</span></span>

* <span data-ttu-id="4aa0b-770">이 함수 현재 제공 하지 않습니다 적절 한 대/소문자 tooconvert 단어에는 약어와 같은 전체적으로 대문자입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="4aa0b-771">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="4aa0b-772">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="4aa0b-773">"Test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="4aa0b-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="4aa0b-774">RandomNum</span></span>
<span data-ttu-id="4aa0b-775">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-775">**Description:**</span></span>  
<span data-ttu-id="4aa0b-776">hello RandomNum 함수는 지정된 된 간격 사이의 난수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="4aa0b-777">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="4aa0b-778">시작: 숫자 식별 hello 하한값 hello 임의 값 toogenerate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="4aa0b-779">끝:는 숫자 식별 hello의 상한값 hello 임의 값 toogenerate</span><span class="sxs-lookup"><span data-stu-id="4aa0b-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="4aa0b-780">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="4aa0b-781">734를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="4aa0b-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="4aa0b-782">RemoveDuplicates</span></span>
<span data-ttu-id="4aa0b-783">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-783">**Description:**</span></span>  
<span data-ttu-id="4aa0b-784">hello RemoveDuplicates 함수는 다중값된 문자열을 사용 하 고 각 값은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="4aa0b-785">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="4aa0b-786">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="4aa0b-787">모든 중복 값을 제거한 삭제된 proxyAddress 특성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="4aa0b-788">Replace</span><span class="sxs-lookup"><span data-stu-id="4aa0b-788">Replace</span></span>
<span data-ttu-id="4aa0b-789">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-789">**Description:**</span></span>  
<span data-ttu-id="4aa0b-790">Replace 함수 hello 문자열 tooanother 문자열로 모두 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="4aa0b-791">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="4aa0b-792">문자열: 문자열 tooreplace 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="4aa0b-793">OldValue:에 대 한 문자열 toosearch hello 및 tooreplace 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="4aa0b-794">NewValue: hello 문자열을 tooreplace 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="4aa0b-795">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-795">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-796">hello 함수 hello 다음 특별 한 모니터를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="4aa0b-797">\n – 새로운 줄</span><span class="sxs-lookup"><span data-stu-id="4aa0b-797">\n – New Line</span></span>
* <span data-ttu-id="4aa0b-798">\r – 캐리지 반환</span><span class="sxs-lookup"><span data-stu-id="4aa0b-798">\r – Carriage Return</span></span>
* <span data-ttu-id="4aa0b-799">\t – 탭</span><span class="sxs-lookup"><span data-stu-id="4aa0b-799">\t – Tab</span></span>

<span data-ttu-id="4aa0b-800">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="4aa0b-801">CRLF를 쉼표와 공백을로 바꾸고 너무 발생할 수 있습니다 "1 Microsoft 방식으로, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="4aa0b-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="4aa0b-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="4aa0b-802">ReplaceChars</span></span>
<span data-ttu-id="4aa0b-803">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-803">**Description:**</span></span>  
<span data-ttu-id="4aa0b-804">ReplaceChars 함수 hello hello ReplacePattern 문자열에서에서 발견 되는 문자의 모두 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="4aa0b-805">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="4aa0b-806">문자열: 문자열 tooreplace에 문자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="4aa0b-807">ReplacePattern: tooreplace 문자를 사용 하 여 사전에 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="4aa0b-808">hello 형식은 {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetn 이며} 여기서 소스는 hello 문자 toofind 및 대상 hello 문자열 tooreplace 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="4aa0b-809">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-809">**Remarks:**</span></span>

* <span data-ttu-id="4aa0b-810">hello 함수는 정의 된 소스의 각 항목을 사용 하 고 hello 대상이 있는 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="4aa0b-811">hello 소스에는 정확히 하나의 (유니코드) 문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="4aa0b-812">hello 소스는 비어 있거나 (구문 분석 오류)는 하나의 문자 보다 길 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="4aa0b-813">hello 대상 oe, β:ss 예를 들어 여러 문자를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="4aa0b-814">hello 대상 hello 문자를 제거 하도록 나타내는 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="4aa0b-815">hello 대/소문자 구분 원본과 정확히 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="4aa0b-816">hello, (쉼표) 및: (콜론) 예약 된 문자 이며이 함수를 사용 하 여 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="4aa0b-817">공백 및 hello ReplacePattern 문자열에서에서 기타 공백 문자는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="4aa0b-818">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="4aa0b-819">Raksmorgas를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="4aa0b-820">/ / "ONeil", 단일 틱 hello 반환은 정의 toobe 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="4aa0b-821">Right</span><span class="sxs-lookup"><span data-stu-id="4aa0b-821">Right</span></span>
<span data-ttu-id="4aa0b-822">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-822">**Description:**</span></span>  
<span data-ttu-id="4aa0b-823">Right 함수 hello hello 오른쪽 (끝) 문자열에서 지정한 개수의 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="4aa0b-824">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="4aa0b-825">문자열: 문자열 tooreturn 문자를 hello</span><span class="sxs-lookup"><span data-stu-id="4aa0b-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="4aa0b-826">Hello 끝 (오른쪽) 문자열에서에서 문자 tooreturn hello 수를 나타내는 숫자 NumChars:</span><span class="sxs-lookup"><span data-stu-id="4aa0b-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="4aa0b-827">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-827">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-828">Hello 문자열의 마지막 위치부터 numchars 개의 문자가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="4aa0b-829">Hello 문자열의 마지막 numChars 문자를 포함 하는 문자열:</span><span class="sxs-lookup"><span data-stu-id="4aa0b-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="4aa0b-830">numChars = 0 인 경우, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="4aa0b-831">numCahrs < 0,인 경우, 입력된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="4aa0b-832">문자열이 null이면 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-832">If string is null, return empty string.</span></span>

<span data-ttu-id="4aa0b-833">문자열에 NumChars에서 지정한 숫자 hello 보다 적은 문자가 포함 된, 문자열 동일한 toostring 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="4aa0b-834">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="4aa0b-835">"Doe"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="4aa0b-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="4aa0b-836">RTrim</span></span>
<span data-ttu-id="4aa0b-837">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-837">**Description:**</span></span>  
<span data-ttu-id="4aa0b-838">RTrim 함수 hello 문자열에서 후행 공백을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="4aa0b-839">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="4aa0b-840">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="4aa0b-841">"Test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="4aa0b-842">여기서</span><span class="sxs-lookup"><span data-stu-id="4aa0b-842">Select</span></span>
<span data-ttu-id="4aa0b-843">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-843">**Description:**</span></span>  
<span data-ttu-id="4aa0b-844">지정된 함수에 기반하여 다중값 특성(또는 식 출력)의 모든 값을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="4aa0b-845">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="4aa0b-846">항목: hello 다중값된 특성의 요소를 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="4aa0b-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="4aa0b-847">특성: hello 다중값된 특성</span><span class="sxs-lookup"><span data-stu-id="4aa0b-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="4aa0b-848">expression: 값의 컬렉션을 반환하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="4aa0b-849">조건: hello 특성에 있는 항목을 처리할 수 있는 모든 함수</span><span class="sxs-lookup"><span data-stu-id="4aa0b-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="4aa0b-850">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="4aa0b-851">Hello 다중값된 특성 otherPhone 하이픈 (-)를 제거한 후 모든 hello 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="4aa0b-852">분할</span><span class="sxs-lookup"><span data-stu-id="4aa0b-852">Split</span></span>
<span data-ttu-id="4aa0b-853">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-853">**Description:**</span></span>  
<span data-ttu-id="4aa0b-854">hello Split 함수는 구분 기호로 구분 된 문자열 다중값된 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="4aa0b-855">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="4aa0b-856">값: 문자열 구분 기호 문자 tooseparate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="4aa0b-857">구분 기호: 단일 문자 toobe 구분 기호를 hello로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="4aa0b-858">limit: 반환될 수 있는 값의 최대 갯수입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="4aa0b-859">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="4aa0b-860">Hello / / proxyAddress 특성에 대 한 유용한 2 개의 요소가 있는 다중값된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="4aa0b-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-861">StringFromGuid</span></span>
<span data-ttu-id="4aa0b-862">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-862">**Description:**</span></span>  
<span data-ttu-id="4aa0b-863">hello StringFromGuid 함수는 이진 guid 및 tooa 문자열 변환</span><span class="sxs-lookup"><span data-stu-id="4aa0b-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="4aa0b-864">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="4aa0b-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="4aa0b-865">StringFromSid</span></span>
<span data-ttu-id="4aa0b-866">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-866">**Description:**</span></span>  
<span data-ttu-id="4aa0b-867">StringFromSid 함수 hello 식별자 tooa 보안 문자열을 포함 하는 바이트 배열을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="4aa0b-868">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="4aa0b-869">Switch</span><span class="sxs-lookup"><span data-stu-id="4aa0b-869">Switch</span></span>
<span data-ttu-id="4aa0b-870">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-870">**Description:**</span></span>  
<span data-ttu-id="4aa0b-871">hello 스위치 함수는 사용 되는 tooreturn 평가 대상된 조건에 따라 단일 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="4aa0b-872">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="4aa0b-873">expr: tooevaluate 원하는 변형 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="4aa0b-874">값: 값 toobe hello 해당 식이 True 인 경우 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="4aa0b-875">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-875">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-876">hello 스위치 함수 인수 목록 식 및 값의 쌍으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="4aa0b-877">hello 식은 왼쪽된 tooright에서 평가 됩니다 하 고 첫 번째 식 tooevaluate tooTrue hello와 연결 된 hello 값 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="4aa0b-878">Hello 부분 적절 하 게 쌍을 이루지 않으면 런타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="4aa0b-879">예를들어, expr1이 True면, Switch는 value1을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="4aa0b-880">expr-1이 False이고, expr-2가 True면 Switch는 Value-2로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="4aa0b-881">다음의 경우 Switch는 Nothing을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="4aa0b-882">Hello 식이 True가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="4aa0b-883">hello 첫 번째 True 식의 해당 값은 Null입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="4aa0b-884">그 중 하나만 반환되더라도, Switch는 모든 식을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="4aa0b-885">그렇기 때문에 원하지 않는 결과가 나타나지 않도록 주의해야합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="4aa0b-886">예를 들어 식 계산한 hello 0으로 나누기의 결과 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="4aa0b-887">값에는 사용자 지정 문자열을 반환 하는 hello 오류 함수를 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="4aa0b-888">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="4aa0b-889">그렇지 않으면 오류가 반환, 일부 주요 도시의 통용 hello 언어를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="4aa0b-890">Trim</span><span class="sxs-lookup"><span data-stu-id="4aa0b-890">Trim</span></span>
<span data-ttu-id="4aa0b-891">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-891">**Description:**</span></span>  
<span data-ttu-id="4aa0b-892">hello Trim 함수는 선행 및 후행 공백이 문자열에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="4aa0b-893">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="4aa0b-894">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="4aa0b-895">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="4aa0b-896">선행 및 후행 hello / / proxyAddress 특성의 각 값에 대 한 공백을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="4aa0b-897">UCase</span><span class="sxs-lookup"><span data-stu-id="4aa0b-897">UCase</span></span>
<span data-ttu-id="4aa0b-898">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-898">**Description:**</span></span>  
<span data-ttu-id="4aa0b-899">UCase 함수 hello 문자열 tooupper 대/소문자의 모든 문자를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="4aa0b-900">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="4aa0b-901">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="4aa0b-902">"test"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="4aa0b-903">Where</span><span class="sxs-lookup"><span data-stu-id="4aa0b-903">Where</span></span>

<span data-ttu-id="4aa0b-904">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-904">**Description:**</span></span>  
<span data-ttu-id="4aa0b-905">특정 조건에 기반하여 다중값 특성(또는 식 출력)의 값에 대한 하위 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="4aa0b-906">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="4aa0b-907">항목: hello 다중값된 특성의 요소를 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="4aa0b-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="4aa0b-908">특성: hello 다중값된 특성</span><span class="sxs-lookup"><span data-stu-id="4aa0b-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="4aa0b-909">조건: tootrue 또는 false 일 수 있는 모든 식 평가</span><span class="sxs-lookup"><span data-stu-id="4aa0b-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="4aa0b-910">expression: 값의 컬렉션을 반환하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="4aa0b-911">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="4aa0b-912">만료 되지 않습니다는 hello 다중값된 특성 userCertificate hello 인증서 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="4aa0b-913">With</span><span class="sxs-lookup"><span data-stu-id="4aa0b-913">With</span></span>
<span data-ttu-id="4aa0b-914">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-914">**Description:**</span></span>  
<span data-ttu-id="4aa0b-915">함수로 hello 변수 toorepresent 하나 표시 되는 하위 식을 사용 하 여 또는 번 더 hello 복잡 한 식에 복잡 한 식 방식으로 toosimplify를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="4aa0b-916">**구문:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="4aa0b-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="4aa0b-917">변수: 나타냅니다 hello 하위 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="4aa0b-918">subExpression: 변수로 표현되는 하위 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="4aa0b-919">complexExpression: 복합 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="4aa0b-920">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="4aa0b-921">기능적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="4aa0b-922">hello userCertificate 특성에 인증서 만료 되지 않은 값만을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="4aa0b-923">Word</span><span class="sxs-lookup"><span data-stu-id="4aa0b-923">Word</span></span>
<span data-ttu-id="4aa0b-924">**설명:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-924">**Description:**</span></span>  
<span data-ttu-id="4aa0b-925">Word 함수 hello hello 구분 기호 toouse 및 hello 단어 번호 tooreturn 설명 하는 매개 변수를 기반 하는 문자열 내에 포함 된 단어를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="4aa0b-926">**구문:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="4aa0b-927">문자열: 문자열 tooreturn 단어 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="4aa0b-928">WordNumber: 반환해야 하는 단어 수를 식별하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="4aa0b-929">구분 기호: 사용된 tooidentify 단어 되어야 하는 hello 구분 기호를 나타내는 문자열</span><span class="sxs-lookup"><span data-stu-id="4aa0b-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="4aa0b-930">**설명**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-930">**Remarks:**</span></span>  
<span data-ttu-id="4aa0b-931">구분 기호로 hello 문자 중 하나가 hello로 구분 된 문자열의 각 문자열은 단어로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="4aa0b-932">숫자가 < 1인경우 , 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="4aa0b-933">문자열이 null이면, 빈 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="4aa0b-934">문자열이 단어 수보다 적거나, 구분 기호로 식별되는 단어를 포함할 경우, 빈 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="4aa0b-935">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4aa0b-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="4aa0b-936">"brown"을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="4aa0b-937">"has"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4aa0b-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4aa0b-938">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4aa0b-938">Additional Resources</span></span>
* [<span data-ttu-id="4aa0b-939">선언적 프로비전 식 이해</span><span class="sxs-lookup"><span data-stu-id="4aa0b-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="4aa0b-940">Azure AD Connect Sync: 사용자 지정 동기화 옵션</span><span class="sxs-lookup"><span data-stu-id="4aa0b-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4aa0b-941">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="4aa0b-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
