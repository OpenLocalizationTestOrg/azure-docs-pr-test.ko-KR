---
title: "Azure Active Directory B2C: 언어 사용자 지정 사용 | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a><span data-ttu-id="a48ff-102">Azure Active Directory B2C: 언어 사용자 지정 사용</span><span class="sxs-lookup"><span data-stu-id="a48ff-102">Azure Active Directory B2C: Using language customization</span></span>

>[!NOTE] 
><span data-ttu-id="a48ff-103">이 기능은 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-103">This feature is in public preview.</span></span>  <span data-ttu-id="a48ff-104">이 기능을 사용할 때 테스트 테넌트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-104">It is recommended that you use a test tenant when using this feature.</span></span>  <span data-ttu-id="a48ff-105">Hello 미리 보기 toohello 일반 공급 릴리스의 주요 변경 내용에 않으려고 예정 이지만 hello 오른쪽 toomake 이러한 변경 내용 tooimprove hello 기능.</span><span class="sxs-lookup"><span data-stu-id="a48ff-105">We don't plan on any breaking changes from hello preview toohello general availability release, but we reserve hello right toomake such changes tooimprove hello feature.</span></span>  <span data-ttu-id="a48ff-106">기회 tootry 기능을 설치한 후에 경험에 대 한 피드백 및 어떻게 म 수 완성도 높이도록 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="a48ff-106">Once you've had a chance tootry feature, please provide feedback on your experiences and how we can make it better.</span></span>  <span data-ttu-id="a48ff-107">오른쪽 위를 hello에 hello 웃는 얼굴 도구로 hello Azure 포털을 통해 피드백을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-107">You can provide feedback through hello Azure portal with hello smiley face tool on hello top right.</span></span>   <span data-ttu-id="a48ff-108">Hello 미리 보기 단계 중에이 기능을 사용 하 여 라이브 toogo 있습니다에 대 한 비즈니스 요구 사항인 경우 알려주시면 시나리오 및 hello 적절 한 지침과 지원을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-108">If there is a business requirement for you toogo live using this feature during hello preview phase, let us know your scenarios and we can provide you with hello proper guidance and assistance.</span></span>  <span data-ttu-id="a48ff-109">[aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)으로 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-109">You can contact us at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>

<span data-ttu-id="a48ff-110">언어의 사용자 지정 사용자 tooa 다양 한 언어 toosuit 고객이 필요한 여행 toochange가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-110">Language customization allows you toochange your user journey tooa different language toosuit your customer needs.</span></span>  <span data-ttu-id="a48ff-111">36개 언어에 대한 번역이 제공됩니다([추가 정보](#additional-information) 참조).</span><span class="sxs-lookup"><span data-stu-id="a48ff-111">We provide translations for 36 languages (see [Additional information](#additional-information)).</span></span>  <span data-ttu-id="a48ff-112">단일 언어에 대 한 환경을 제공 하는 경우에 요구 사항 페이지 toosuit hello에서 모든 텍스트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-112">Even if your experience is only provided for a single language, you can customize any text on hello pages toosuit your needs.</span></span>  

## <a name="how-does-language-customization-work"></a><span data-ttu-id="a48ff-113">언어 사용자 지정이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="a48ff-113">How does Language customization work?</span></span>
<span data-ttu-id="a48ff-114">사용자 지정 언어 tooselect을 언어로 된 사용자 여행은에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-114">Language customization allows you tooselect which languages your user journey is available in.</span></span>  <span data-ttu-id="a48ff-115">Hello 기능이 활성화 되 면 hello 쿼리 문자열 매개 변수, ui_locales, 응용 프로그램에서 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-115">Once hello feature is enabled, you can provide hello query string parameter, ui_locales, from your application.</span></span>  <span data-ttu-id="a48ff-116">Azure AD B2C을 호출할 때 사용자가 지정한 페이지 toohello 로캘에서으로 변환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-116">When you call into Azure AD B2C, we translate your page toohello locale that you have indicated.</span></span>  <span data-ttu-id="a48ff-117">구성 유형을 사용 하 여 사용자 작업의 완전히 제어할 hello 언어를 제공 하 고 hello 고객의 브라우저의 언어 설정 hello를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-117">Using type of configuration gives you complete control over hello languages in your user journey and ignores hello language settings of hello customer's browser.</span></span> <span data-ttu-id="a48ff-118">또는 고객이 볼 수 있는 언어에 대한 제어 수준이 필요하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-118">Alternatively, you may not need that level of control over what languages your customer see.</span></span>  <span data-ttu-id="a48ff-119">Ui_locales 매개 변수를 제공 하지 않으면 hello 고객의 경험은 브라우저의 설정에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-119">If you don't provide a ui_locales parameter, hello customer's experience is dictated by their browser's settings.</span></span>  <span data-ttu-id="a48ff-120">여전히 제어 하는 사용자 작업은 언어 번역 tooby 지원 되는 언어로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-120">You can still control which languages your user journey is translated tooby adding it as a supported language.</span></span>  <span data-ttu-id="a48ff-121">고객의 브라우저 집합 tooshow 있으면 언어 원하지 toosupport, 다음 hello 언어를 지원 되는 culture의 기본값 대신 표시 된 대로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-121">If a customer's browser is set tooshow a language you don't want toosupport, then hello language you selected as a default in supported cultures is shown instead.</span></span>

1. <span data-ttu-id="a48ff-122">**언어를 지정 하는 ui 로캘에서** -사용자 작업은 여기에서 지정 된 하는 번역 된 toohello 언어 언어 사용자 지정을 사용 하도록 설정 하면</span><span class="sxs-lookup"><span data-stu-id="a48ff-122">**ui-locales specified language** - Once you enable Language customization, your user journey is translated toohello language specified here</span></span>
2. <span data-ttu-id="a48ff-123">**브라우저 언어를 요청 했습니다.** -toohello 변환 없는 ui 로캘에 지정 된 경우 브라우저 언어에서 요청한 **지원 되는 언어에 포함 된 경우**</span><span class="sxs-lookup"><span data-stu-id="a48ff-123">**Browser requested language** - If no ui-locales was specified, it translates toohello browser requested language, **if it was included in Supported languages**</span></span>
3. <span data-ttu-id="a48ff-124">**기본 언어 정책** -toohello 정책 기본 언어 hello 브라우저 언어를 지정 하지 않거나 지원 되지 않는 하나 지정, 변환</span><span class="sxs-lookup"><span data-stu-id="a48ff-124">**Policy default language** - If hello browser doesn't specify a language, or it specifies one that is not supported, it translates toohello policy default language</span></span>

>[!NOTE]
><span data-ttu-id="a48ff-125">사용자 지정 특성을 사용 하는 경우 사용자 고유의 번역 tooprovide 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-125">If you are using custom user attributes, you need tooprovide your own translations.</span></span> <span data-ttu-id="a48ff-126">자세한 내용은 '[문자열 사용자 지정](#customize-your-strings)'을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a48ff-126">See '[Customize your strings](#customize-your-strings)' for details.</span></span>
>

## <a name="support-uilocales-requested-languages"></a><span data-ttu-id="a48ff-127">ui_locales 요청 언어 지원</span><span class="sxs-lookup"><span data-stu-id="a48ff-127">Support ui_locales requested languages</span></span> 
<span data-ttu-id="a48ff-128">정책에 ' 언어 사용자 지정'를 사용 하 여 hello ui_locales 매개 변수를 추가 하 여 이제 hello 사용자 여행의 hello 언어를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-128">By enabling 'Language customization' on a policy, you can now control hello language of hello user journey by adding hello ui_locales parameter.</span></span>
1. [<span data-ttu-id="a48ff-129">Hello Azure 포털에 이러한 단계 toonavigate toohello B2C 기능 블레이드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-129">Follow these steps toonavigate toohello B2C features blade on hello Azure portal.</span></span>](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. <span data-ttu-id="a48ff-130">번역에 대 한 tooenable 되도록 tooa 정책을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-130">Navigate tooa policy that you want tooenable for translations.</span></span>
3. <span data-ttu-id="a48ff-131">**언어 사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-131">Click **Language customization**.</span></span>
4. <span data-ttu-id="a48ff-132">읽기 hello 신중 하 게 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-132">Read hello warning carefully.</span></span>  <span data-ttu-id="a48ff-133">사용하도록 설정된 후에는 '언어 사용자 지정'을 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-133">Once enabled, you cannot turn off 'Language customization'.</span></span>
5. <span data-ttu-id="a48ff-134">Hello 기능을 설정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-134">Turn on hello feature and click **OK**.</span></span>
6. <span data-ttu-id="a48ff-135">Hello의 왼쪽된 위 모서리에서 사용자 정책을 저장 하면 **정책 편집** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-135">Save your policy on hello upper left corner of your **Edit policy** blade.</span></span>

## <a name="select-which-languages-your-user-journey-supports"></a><span data-ttu-id="a48ff-136">사용자 경험에서 지원하는 언어 선택</span><span class="sxs-lookup"><span data-stu-id="a48ff-136">Select which languages your user journey supports</span></span> 
<span data-ttu-id="a48ff-137">프로그램 사용자의 여행 toobe hello ui_locales 매개 변수는 제공 되지 않은 경우에 변환에 대 한 허용 된 언어의 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-137">Create a list of allowed languages for your user journey toobe translated in when hello ui_locales parameter is not provided.</span></span>
1. <span data-ttu-id="a48ff-138">이전 지침에서 정책에 '언어 사용자 지정'이 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-138">Ensure your policy has 'Language customization' enabled from previous instructions.</span></span>
2. <span data-ttu-id="a48ff-139">**정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-139">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="a48ff-140">Tooyour 취해집니다 **지원 되는 언어** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-140">You are taken tooyour **Supported languages** blade.</span></span>  <span data-ttu-id="a48ff-141">여기에서 **언어 추가**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-141">From here, you can select **Add language**.</span></span>
4. <span data-ttu-id="a48ff-142">지원 되는 toobe 원하는 모든 hello 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-142">Select all hello languages that you would like toobe supported.</span></span>  

>[!NOTE]
><span data-ttu-id="a48ff-143">Ui_locales 매개 변수가 제공 되지 않은 경우 다음 hello 페이지는 브라우저 언어 번역 된 toohello 고객의 경우에이 목록에 있음</span><span class="sxs-lookup"><span data-stu-id="a48ff-143">If a ui_locales parameter is not provided, then hello page is translated toohello customer's browser language only if it is on this list</span></span>
>

5. <span data-ttu-id="a48ff-144">클릭 **확인** hello 맨 아래에</span><span class="sxs-lookup"><span data-stu-id="a48ff-144">Click **Ok** at hello bottom</span></span>
6. <span data-ttu-id="a48ff-145">닫기 hello **사용자 지정 언어** 블레이드 및 **저장** 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-145">Close hello **Language customization** blade and **save** your policy.</span></span>

## <a name="customize-your-strings"></a><span data-ttu-id="a48ff-146">문자열 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a48ff-146">Customize your strings</span></span>
<span data-ttu-id="a48ff-147">'Language 사용자 지정을' 모든 사용자 여정에서 문자열 toocustomize 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-147">'Language customization' allows you toocustomize any string in your user journey.</span></span>
1. <span data-ttu-id="a48ff-148">정책에 '언어 사용자 지정' hello 이전 명령에서 사용 하도록 설정할 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-148">Ensure your policy has 'Language customization' enabled from hello previous instructions.</span></span>
2. <span data-ttu-id="a48ff-149">**정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-149">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="a48ff-150">Hello 왼쪽 탐색 메뉴에서 선택 **콘텐츠 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-150">From hello left-hand navigation menu, select **Download content**.</span></span>
4. <span data-ttu-id="a48ff-151">Tooedit hello 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-151">Select hello page you want tooedit.</span></span>
5. <span data-ttu-id="a48ff-152">Hello 드롭다운에서 tooedit에 대 한 hello 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-152">In hello dropdown, select hello language you want tooedit for.</span></span>
6. <span data-ttu-id="a48ff-153">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-153">Click **Download**.</span></span> 

<span data-ttu-id="a48ff-154">이러한 단계는 사용자 문자열 편집 toostart를 사용할 수 있는 JSON 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-154">These steps give you a JSON file that you can use toostart editing your strings.</span></span>

### <a name="changing-any-string-on-hello-page"></a><span data-ttu-id="a48ff-155">Hello 페이지에서 모든 문자열을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-155">Changing any string on hello page</span></span>
1. <span data-ttu-id="a48ff-156">JSON 파일 열기 hello JSON 편집기의 이전 지침에서 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-156">Open hello JSON file downloaded from previous instructions in a JSON editor.</span></span>
2. <span data-ttu-id="a48ff-157">원하는 toochange 찾기 hello 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-157">Find hello element you want toochange.</span></span>  <span data-ttu-id="a48ff-158">Hello를 찾을 수 있습니다 `StringId` 찾고 아니면 hello 찾을 hello 문자열의 `Value` toochange 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-158">You can find hello `StringId` of hello string you are looking for, or look for hello `Value` you want toochange.</span></span>
3. <span data-ttu-id="a48ff-159">업데이트 hello `Value` 특성으로 표시 하려는 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-159">Update hello `Value` attribute with what you want displayed.</span></span>
4. <span data-ttu-id="a48ff-160">Hello 파일을 저장 하 고 변경 내용을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-160">Save hello file and upload your changes.</span></span>

### <a name="changing-extension-attributes"></a><span data-ttu-id="a48ff-161">확장 특성 변경</span><span class="sxs-lookup"><span data-stu-id="a48ff-161">Changing extension attributes</span></span>
<span data-ttu-id="a48ff-162">사용자 지정 특성에 대 한 toochange hello 문자열을 찾고 또는 tooadd 하나 toohello JSON 원하는 형식에 따라 hello 됨:</span><span class="sxs-lookup"><span data-stu-id="a48ff-162">If you are looking toochange hello string for a custom user attribute, or want tooadd one toohello JSON, it is in hello following format:</span></span>
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
><span data-ttu-id="a48ff-163">Toooverride 문자열, 필요한 경우 확인 되었는지 tooset hello `Override` 너무 값`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-163">If you need toooverride a string, make sure tooset hello `Override` value too`true`.</span></span>  <span data-ttu-id="a48ff-164">Hello 값 변경 되지 않고 hello 항목이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-164">If hello value isn't changed, hello entry is ignored.</span></span> 
>

<span data-ttu-id="a48ff-165">대체 `<ExtensionAttribute>` 사용자 지정 특성의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-165">Replace `<ExtensionAttribute>` with hello name of your custom user attribute.</span></span>  
<span data-ttu-id="a48ff-166">대체 `<ExtensionAttributeValue>` hello 새 문자열 toobe 표시를 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-166">Replace `<ExtensionAttributeValue>` with hello new string toobe displayed.</span></span>

### <a name="using-localizedcollections"></a><span data-ttu-id="a48ff-167">LocalizedCollections 사용</span><span class="sxs-lookup"><span data-stu-id="a48ff-167">Using LocalizedCollections</span></span>
<span data-ttu-id="a48ff-168">응답에 대 한 tooprovide 목록 값의 집합을 원하는 경우 toocreate는 `LocalizedCollections`합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-168">If you want tooprovide a set list of values for responses, you need toocreate a `LocalizedCollections`.</span></span>  <span data-ttu-id="a48ff-169">`LocalizedCollections`는 `Name` 및 `Value` 쌍의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-169">A `LocalizedCollections` is an array of `Name` and `Value` pairs.</span></span>  <span data-ttu-id="a48ff-170">hello `Name` 표시 되 고 hello `Value` hello 클레임에 반환 되는 항목은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-170">hello `Name` is what is displayed and hello `Value` is what is returned in hello claim.</span></span>  <span data-ttu-id="a48ff-171">tooadd는 `LocalizedCollections`, 형식에 따라 hello에:</span><span class="sxs-lookup"><span data-stu-id="a48ff-171">tooadd a `LocalizedCollections`, it has hello following format:</span></span>

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
><span data-ttu-id="a48ff-172">Toooverride 문자열, 필요한 경우 확인 되었는지 tooset hello `Override` 너무 값`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-172">If you need toooverride a string, make sure tooset hello `Override` value too`true`.</span></span>  <span data-ttu-id="a48ff-173">Hello 값 변경 되지 않고 hello 항목이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-173">If hello value isn't changed, hello entry is ignored.</span></span> 
>

* <span data-ttu-id="a48ff-174">`ElementId`hello 사용자 특성이 `LocalizedCollections` 에 대 한 응답</span><span class="sxs-lookup"><span data-stu-id="a48ff-174">`ElementId` is hello user attribute that this `LocalizedCollections` is a response to</span></span>
* <span data-ttu-id="a48ff-175">`Name`이 값 표시 된 toohello 사용자 hello</span><span class="sxs-lookup"><span data-stu-id="a48ff-175">`Name` is hello value shown toohello user</span></span>
* <span data-ttu-id="a48ff-176">`Value`이 옵션을 선택 하는 hello 클레임에 반환 되는 항목은</span><span class="sxs-lookup"><span data-stu-id="a48ff-176">`Value` is what is returned in hello claim when this option is selected</span></span>

### <a name="upload-your-changes"></a><span data-ttu-id="a48ff-177">변경 내용 업로드</span><span class="sxs-lookup"><span data-stu-id="a48ff-177">Upload your changes</span></span>
1. <span data-ttu-id="a48ff-178">Hello 변경 tooyour JSON 파일을 완료 한 후 뒤로 tooyour B2C 테 넌 트를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-178">Once you have completed hello changes tooyour JSON file, navigate back tooyour B2C tenant.</span></span>
2. <span data-ttu-id="a48ff-179">**정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-179">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="a48ff-180">Hello 왼쪽 탐색 메뉴에서 선택 **콘텐츠 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-180">From hello left-hand navigation menu, select **Upload content**.</span></span>
4. <span data-ttu-id="a48ff-181">에 대 한 변경 내용을 tooupload 원하는 hello 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-181">Select hello page you want tooupload your changes for.</span></span>
5. <span data-ttu-id="a48ff-182">Tooupload 언어에 대 한 JSON 이전에 제공한를 원하는 경우 toodelete hello 이전 항목을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-182">If you want tooupload a language that you've previously provided a JSON for, you need toodelete hello previous entry.</span></span>  <span data-ttu-id="a48ff-183">Hello를 클릭 하 여 삭제할 수 있습니다 `...` 해당 언어의 오른쪽 hello 되 고 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-183">You can delete it by clicking hello `...` on hello right of that language and select **Delete**.</span></span>
6. <span data-ttu-id="a48ff-184">클릭 **추가** hello 상단 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-184">Click **Add** on hello upper left.</span></span>
7. <span data-ttu-id="a48ff-185">JSON 파일의 hello 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-185">Select hello language of your JSON file.</span></span>
8. <span data-ttu-id="a48ff-186">Hello 오른쪽에 hello 폴더 단추를 클릭 하 고 JSON 파일을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-186">Click hello folder button on hello right and browse for your JSON file.</span></span>
9. <span data-ttu-id="a48ff-187">Hello 클릭 **업로드** hello hello 블레이드 맨 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-187">Click hello **Upload** button on hello bottom of hello blade.</span></span>
10. <span data-ttu-id="a48ff-188">Tooyour 돌아가서 **정책 편집** 블레이드에 대 한 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-188">Go back tooyour **Edit policy** blade and click **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="a48ff-189">추가 정보</span><span class="sxs-lookup"><span data-stu-id="a48ff-189">Additional information</span></span>
### <a name="recommendations-for-language-customization"></a><span data-ttu-id="a48ff-190">'언어 사용자 지정'에 대한 권장 사항</span><span class="sxs-lookup"><span data-stu-id="a48ff-190">Recommendations for 'Language customization'</span></span>
<span data-ttu-id="a48ff-191">만에 넣는 문자열에 대 한 항목 tooyour 언어 리소스 하면 명시적으로 원하는 tooreplace 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-191">We recommend only putting in entries tooyour Language resources for strings you explicitly want tooreplace.</span></span>  <span data-ttu-id="a48ff-192">에서는 모든 JSON 번역에서 컴파일되는 크기 제한 toohello 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-192">We enforce a size limit toohello file that is compiled out of all your JSON translations.</span></span>  <span data-ttu-id="a48ff-193">파일이 너무 큰 경우, 사용자 작업의 hello 성능 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-193">If your files get too large, it impacts hello performance of your user journey.</span></span>
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a><span data-ttu-id="a48ff-194">'언어 사용자 지정'을 사용하면 페이지 UI 사용자 지정 레이블이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-194">Page UI customization labels are removed once 'Language customization' is enabled</span></span>
<span data-ttu-id="a48ff-195">'언어 사용자 지정'을 사용하도록 설정하면 사용자 지정 사용자 특성을 제외하고, 페이지 UI 사용자 지정을 사용한 레이블에 대한 이전 편집이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-195">When you enable 'Language customization', your previous edits for labels using Page UI customization are removed except for custom user attributes.</span></span>  <span data-ttu-id="a48ff-196">이 변경은 tooavoid 충돌을 방지 문자열을 편집할 수 있는 작업 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-196">This change is done tooavoid conflicts in where you can edit your strings.</span></span>  <span data-ttu-id="a48ff-197">'언어 사용자 지정'의 언어 리소스를 업로드 하 여 레이블 및 기타 문자열 toochange를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-197">You can continue toochange your labels and other strings by uploading language resources in 'Language customization'.</span></span>
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a><span data-ttu-id="a48ff-198">Microsoft는 사용에 대 한 커밋된 tooprovide hello 최신 번역</span><span class="sxs-lookup"><span data-stu-id="a48ff-198">Microsoft is committed tooprovide hello most up-to-date translations for your use</span></span>
<span data-ttu-id="a48ff-199">지속적으로 번역을 개선하고 사용자에 맞게 유지할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-199">We will continuously improve translations and keep them in compliance for you.</span></span>  <span data-ttu-id="a48ff-200">버그 및 글로벌 용어에서 변경 내용을 식별 하 고 사용자 여정에서 원활 하 게 작동 하는 hello 업데이트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-200">We will identify bugs and changes in global terminology and make hello updates that will work seamlessly in your user journey.</span></span>
### <a name="support-for-right-to-left-languages"></a><span data-ttu-id="a48ff-201">오른쪽에서 왼쪽 언어 지원</span><span class="sxs-lookup"><span data-stu-id="a48ff-201">Support for right-to-left languages</span></span>
<span data-ttu-id="a48ff-202">오른쪽에서 왼쪽 언어에 대한 지원은 없습니다. 이 기능이 필요하면 [Azure 피드백](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag)에서 이 기능에 대해 투표하세요.</span><span class="sxs-lookup"><span data-stu-id="a48ff-202">There is no support for right-to-left languages, if you require this feature please vote for this feature on [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).</span></span>
### <a name="social-identity-provider-translations"></a><span data-ttu-id="a48ff-203">소셜 ID 공급자 변환</span><span class="sxs-lookup"><span data-stu-id="a48ff-203">Social Identity provider translations</span></span>
<span data-ttu-id="a48ff-204">Hello ui_locales OIDC 매개 변수 toosocial 로그인 제공 하지만 Facebook 및 Google 등 일부 소셜 id 공급자에는 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-204">We provide hello ui_locales OIDC parameter toosocial logins but they are not honored by some social identity providers, including Facebook and Google.</span></span> 
### <a name="browser-behavior"></a><span data-ttu-id="a48ff-205">브라우저 동작</span><span class="sxs-lookup"><span data-stu-id="a48ff-205">Browser behavior</span></span>
<span data-ttu-id="a48ff-206">Chrome 및 Firefox 둘 다의 언어 설정에 대 한 요청 및 지원 되는 언어 인 경우 hello 기본 하기 전에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-206">Chrome and Firefox both request for their set language and if it is a supported language, it is displayed before hello default.</span></span>  <span data-ttu-id="a48ff-207">가장자리는 현재 언어를 요청 하지 않고와 직선 toohello 기본 언어를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-207">Edge currently does not request a language and goes straight toohello default language.</span></span>
### <a name="known-issues"></a><span data-ttu-id="a48ff-208">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="a48ff-208">Known issues</span></span>
* <span data-ttu-id="a48ff-209">프로필 편집 정책에서 MFA 페이지 hello에 대 한 언어 리소스를 업로드 하는 중 현재 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-209">Uploading language resources for hello MFA page in a Profile Edit policy is currently unavailable.</span></span>
* <span data-ttu-id="a48ff-210">`LocalizedCollections`hello 응답 형식에 필요한 경우 값에 대해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-210">`LocalizedCollections` aren't generated for values when it is required by hello response type</span></span>
### <a name="what-if-i-want-a-language-that-isnt-supported"></a><span data-ttu-id="a48ff-211">지원되지 않는 언어가 필요하다면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="a48ff-211">What if I want a language that isn't supported?</span></span>
<span data-ttu-id="a48ff-212">예정 tooprovide tooupload '사용자 지정 언어'에 대 한 JSON 리소스 사용 하면이 기능을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-212">We are planning tooprovide an extension of this feature that allows you tooupload a JSON resource towards 'custom languages'.</span></span>  <span data-ttu-id="a48ff-213">hello 기능 있습니다 toospecify hello 이름 및 언어는 모든 언어에 대 한 코드 및 제공 *모든* 해당 언어에 대 한 번역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a48ff-213">hello feature allows you toospecify hello name and language code for any language and provide *all* hello translations for that language.</span></span>  <span data-ttu-id="a48ff-214">이 기능이 필요한 경우 [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)으로 시나리오를 보내 주세요.</span><span class="sxs-lookup"><span data-stu-id="a48ff-214">If you need this feature, send us your scenario at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>  

### <a name="what-languages-are-supported"></a><span data-ttu-id="a48ff-215">어떤 언어가 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="a48ff-215">What languages are supported?</span></span>

| <span data-ttu-id="a48ff-216">language</span><span class="sxs-lookup"><span data-stu-id="a48ff-216">Language</span></span>              | <span data-ttu-id="a48ff-217">언어 코드</span><span class="sxs-lookup"><span data-stu-id="a48ff-217">Language code</span></span> |
|-----------------------|---------------|
| <span data-ttu-id="a48ff-218">벵골어</span><span class="sxs-lookup"><span data-stu-id="a48ff-218">Bangla</span></span>                | <span data-ttu-id="a48ff-219">bn</span><span class="sxs-lookup"><span data-stu-id="a48ff-219">bn</span></span>            |
| <span data-ttu-id="a48ff-220">체코어</span><span class="sxs-lookup"><span data-stu-id="a48ff-220">Czech</span></span>                 | <span data-ttu-id="a48ff-221">cs</span><span class="sxs-lookup"><span data-stu-id="a48ff-221">cs</span></span>            |
| <span data-ttu-id="a48ff-222">덴마크어</span><span class="sxs-lookup"><span data-stu-id="a48ff-222">Danish</span></span>                | <span data-ttu-id="a48ff-223">da</span><span class="sxs-lookup"><span data-stu-id="a48ff-223">da</span></span>            |
| <span data-ttu-id="a48ff-224">독일어</span><span class="sxs-lookup"><span data-stu-id="a48ff-224">German</span></span>                | <span data-ttu-id="a48ff-225">de</span><span class="sxs-lookup"><span data-stu-id="a48ff-225">de</span></span>            |
| <span data-ttu-id="a48ff-226">그리스어</span><span class="sxs-lookup"><span data-stu-id="a48ff-226">Greek</span></span>                 | <span data-ttu-id="a48ff-227">el</span><span class="sxs-lookup"><span data-stu-id="a48ff-227">el</span></span>            |
| <span data-ttu-id="a48ff-228">영어</span><span class="sxs-lookup"><span data-stu-id="a48ff-228">English</span></span>               | <span data-ttu-id="a48ff-229">en</span><span class="sxs-lookup"><span data-stu-id="a48ff-229">en</span></span>            |
| <span data-ttu-id="a48ff-230">스페인어</span><span class="sxs-lookup"><span data-stu-id="a48ff-230">Spanish</span></span>               | <span data-ttu-id="a48ff-231">es</span><span class="sxs-lookup"><span data-stu-id="a48ff-231">es</span></span>            |
| <span data-ttu-id="a48ff-232">핀란드어</span><span class="sxs-lookup"><span data-stu-id="a48ff-232">Finnish</span></span>               | <span data-ttu-id="a48ff-233">fi</span><span class="sxs-lookup"><span data-stu-id="a48ff-233">fi</span></span>            |
| <span data-ttu-id="a48ff-234">프랑스어</span><span class="sxs-lookup"><span data-stu-id="a48ff-234">French</span></span>                | <span data-ttu-id="a48ff-235">fr</span><span class="sxs-lookup"><span data-stu-id="a48ff-235">fr</span></span>            |
| <span data-ttu-id="a48ff-236">구자라트어</span><span class="sxs-lookup"><span data-stu-id="a48ff-236">Gujarati</span></span>              | <span data-ttu-id="a48ff-237">gu</span><span class="sxs-lookup"><span data-stu-id="a48ff-237">gu</span></span>            |
| <span data-ttu-id="a48ff-238">힌디어</span><span class="sxs-lookup"><span data-stu-id="a48ff-238">Hindi</span></span>                 | <span data-ttu-id="a48ff-239">hi</span><span class="sxs-lookup"><span data-stu-id="a48ff-239">hi</span></span>            |
| <span data-ttu-id="a48ff-240">크로아티아어</span><span class="sxs-lookup"><span data-stu-id="a48ff-240">Croatian</span></span>              | <span data-ttu-id="a48ff-241">hr</span><span class="sxs-lookup"><span data-stu-id="a48ff-241">hr</span></span>            |
| <span data-ttu-id="a48ff-242">헝가리어</span><span class="sxs-lookup"><span data-stu-id="a48ff-242">Hungarian</span></span>             | <span data-ttu-id="a48ff-243">hu</span><span class="sxs-lookup"><span data-stu-id="a48ff-243">hu</span></span>            |
| <span data-ttu-id="a48ff-244">이탈리아어</span><span class="sxs-lookup"><span data-stu-id="a48ff-244">Italian</span></span>               | <span data-ttu-id="a48ff-245">it</span><span class="sxs-lookup"><span data-stu-id="a48ff-245">it</span></span>            |
| <span data-ttu-id="a48ff-246">일본어</span><span class="sxs-lookup"><span data-stu-id="a48ff-246">Japanese</span></span>              | <span data-ttu-id="a48ff-247">ja</span><span class="sxs-lookup"><span data-stu-id="a48ff-247">ja</span></span>            |
| <span data-ttu-id="a48ff-248">카나다어</span><span class="sxs-lookup"><span data-stu-id="a48ff-248">Kannada</span></span>               | <span data-ttu-id="a48ff-249">kn</span><span class="sxs-lookup"><span data-stu-id="a48ff-249">kn</span></span>            |
| <span data-ttu-id="a48ff-250">한국어</span><span class="sxs-lookup"><span data-stu-id="a48ff-250">Korean</span></span>                | <span data-ttu-id="a48ff-251">ko</span><span class="sxs-lookup"><span data-stu-id="a48ff-251">ko</span></span>            |
| <span data-ttu-id="a48ff-252">말라얄람어</span><span class="sxs-lookup"><span data-stu-id="a48ff-252">Malayalam</span></span>             | <span data-ttu-id="a48ff-253">ml</span><span class="sxs-lookup"><span data-stu-id="a48ff-253">ml</span></span>            |
| <span data-ttu-id="a48ff-254">마라티어</span><span class="sxs-lookup"><span data-stu-id="a48ff-254">Marathi</span></span>               | <span data-ttu-id="a48ff-255">mr</span><span class="sxs-lookup"><span data-stu-id="a48ff-255">mr</span></span>            |
| <span data-ttu-id="a48ff-256">말레이어</span><span class="sxs-lookup"><span data-stu-id="a48ff-256">Malay</span></span>                 | <span data-ttu-id="a48ff-257">ms</span><span class="sxs-lookup"><span data-stu-id="a48ff-257">ms</span></span>            |
| <span data-ttu-id="a48ff-258">노르웨이어 복말</span><span class="sxs-lookup"><span data-stu-id="a48ff-258">Norwegian Bokmal</span></span>      | <span data-ttu-id="a48ff-259">nb</span><span class="sxs-lookup"><span data-stu-id="a48ff-259">nb</span></span>            |
| <span data-ttu-id="a48ff-260">네덜란드어</span><span class="sxs-lookup"><span data-stu-id="a48ff-260">Dutch</span></span>                 | <span data-ttu-id="a48ff-261">nl</span><span class="sxs-lookup"><span data-stu-id="a48ff-261">nl</span></span>            |
| <span data-ttu-id="a48ff-262">펀잡어</span><span class="sxs-lookup"><span data-stu-id="a48ff-262">Punjabi</span></span>               | <span data-ttu-id="a48ff-263">pa</span><span class="sxs-lookup"><span data-stu-id="a48ff-263">pa</span></span>            |
| <span data-ttu-id="a48ff-264">폴란드어</span><span class="sxs-lookup"><span data-stu-id="a48ff-264">Polish</span></span>                | <span data-ttu-id="a48ff-265">pl</span><span class="sxs-lookup"><span data-stu-id="a48ff-265">pl</span></span>            |
| <span data-ttu-id="a48ff-266">포르투갈어 - 브라질</span><span class="sxs-lookup"><span data-stu-id="a48ff-266">Portuguese - Brazil</span></span>   | <span data-ttu-id="a48ff-267">pt-br</span><span class="sxs-lookup"><span data-stu-id="a48ff-267">pt-br</span></span>         |
| <span data-ttu-id="a48ff-268">포르투갈어 - 포르투갈</span><span class="sxs-lookup"><span data-stu-id="a48ff-268">Portuguese - Portugal</span></span> | <span data-ttu-id="a48ff-269">pt-pt</span><span class="sxs-lookup"><span data-stu-id="a48ff-269">pt-pt</span></span>         |
| <span data-ttu-id="a48ff-270">루마니아어</span><span class="sxs-lookup"><span data-stu-id="a48ff-270">Romanian</span></span>              | <span data-ttu-id="a48ff-271">ro</span><span class="sxs-lookup"><span data-stu-id="a48ff-271">ro</span></span>            |
| <span data-ttu-id="a48ff-272">러시아어</span><span class="sxs-lookup"><span data-stu-id="a48ff-272">Russian</span></span>               | <span data-ttu-id="a48ff-273">ru</span><span class="sxs-lookup"><span data-stu-id="a48ff-273">ru</span></span>            |
| <span data-ttu-id="a48ff-274">슬로바키아어</span><span class="sxs-lookup"><span data-stu-id="a48ff-274">Slovak</span></span>                | <span data-ttu-id="a48ff-275">sk</span><span class="sxs-lookup"><span data-stu-id="a48ff-275">sk</span></span>            |
| <span data-ttu-id="a48ff-276">스웨덴어</span><span class="sxs-lookup"><span data-stu-id="a48ff-276">Swedish</span></span>               | <span data-ttu-id="a48ff-277">sv</span><span class="sxs-lookup"><span data-stu-id="a48ff-277">sv</span></span>            |
| <span data-ttu-id="a48ff-278">타밀어</span><span class="sxs-lookup"><span data-stu-id="a48ff-278">Tamil</span></span>                 | <span data-ttu-id="a48ff-279">ta</span><span class="sxs-lookup"><span data-stu-id="a48ff-279">ta</span></span>            |
| <span data-ttu-id="a48ff-280">텔루구어</span><span class="sxs-lookup"><span data-stu-id="a48ff-280">Telugu</span></span>                | <span data-ttu-id="a48ff-281">te</span><span class="sxs-lookup"><span data-stu-id="a48ff-281">te</span></span>            |
| <span data-ttu-id="a48ff-282">태국어</span><span class="sxs-lookup"><span data-stu-id="a48ff-282">Thai</span></span>                  | <span data-ttu-id="a48ff-283">th</span><span class="sxs-lookup"><span data-stu-id="a48ff-283">th</span></span>            |
| <span data-ttu-id="a48ff-284">터키어</span><span class="sxs-lookup"><span data-stu-id="a48ff-284">Turkish</span></span>               | <span data-ttu-id="a48ff-285">tr</span><span class="sxs-lookup"><span data-stu-id="a48ff-285">tr</span></span>            |
| <span data-ttu-id="a48ff-286">중국어 - 간체</span><span class="sxs-lookup"><span data-stu-id="a48ff-286">Chinese - Simplified</span></span>  | <span data-ttu-id="a48ff-287">zh-hans</span><span class="sxs-lookup"><span data-stu-id="a48ff-287">zh-hans</span></span>       |
| <span data-ttu-id="a48ff-288">중국어 - 번체</span><span class="sxs-lookup"><span data-stu-id="a48ff-288">Chinese - Traditional</span></span> | <span data-ttu-id="a48ff-289">zh-hant</span><span class="sxs-lookup"><span data-stu-id="a48ff-289">zh-hant</span></span>       |
