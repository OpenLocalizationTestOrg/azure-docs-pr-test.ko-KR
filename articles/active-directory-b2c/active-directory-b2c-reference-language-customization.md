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
ms.openlocfilehash: 3c7c49ee5fbd98762da0eef6f02e7c2f036453cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a><span data-ttu-id="df5f3-102">Azure Active Directory B2C: 언어 사용자 지정 사용</span><span class="sxs-lookup"><span data-stu-id="df5f3-102">Azure Active Directory B2C: Using language customization</span></span>

>[!NOTE] 
><span data-ttu-id="df5f3-103">이 기능은 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-103">This feature is in public preview.</span></span>  <span data-ttu-id="df5f3-104">이 기능을 사용할 때 테스트 테넌트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-104">It is recommended that you use a test tenant when using this feature.</span></span>  <span data-ttu-id="df5f3-105">미리 보기에서 일반 공급 릴리스로 주요 변경 사항은 계획하지 않지만 기능 개선을 위해 이러한 변경 작업을 수행할 권리를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-105">We don't plan on any breaking changes from the preview to the general availability release, but we reserve the right to make such changes to improve the feature.</span></span>  <span data-ttu-id="df5f3-106">기능을 사용해 볼 기회가 있는 경우 경험에 대한 피드백을 제공하고 더 나은 결과를 얻을 수 있는 방법을 제공해주세요.</span><span class="sxs-lookup"><span data-stu-id="df5f3-106">Once you've had a chance to try feature, please provide feedback on your experiences and how we can make it better.</span></span>  <span data-ttu-id="df5f3-107">Azure Portal을 통해 오른쪽 상단의 웃는 얼굴 도구로 피드백을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-107">You can provide feedback through the Azure portal with the smiley face tool on the top right.</span></span>   <span data-ttu-id="df5f3-108">미리 보기 단계에서 이 기능을 라이브로 전환하여 사용해야 하는 비즈니스 요구 사항이 있는 경우 시나리오를 알려 주시면 적절한 안내와 지원을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-108">If there is a business requirement for you to go live using this feature during the preview phase, let us know your scenarios and we can provide you with the proper guidance and assistance.</span></span>  <span data-ttu-id="df5f3-109">[aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)으로 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-109">You can contact us at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>

<span data-ttu-id="df5f3-110">언어 사용자 지정을 통해 고객 요구에 맞게 사용자 경험을 다른 언어로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-110">Language customization allows you to change your user journey to a different language to suit your customer needs.</span></span>  <span data-ttu-id="df5f3-111">36개 언어에 대한 번역이 제공됩니다([추가 정보](#additional-information) 참조).</span><span class="sxs-lookup"><span data-stu-id="df5f3-111">We provide translations for 36 languages (see [Additional information](#additional-information)).</span></span>  <span data-ttu-id="df5f3-112">단일 언어로만 환경이 제공되더라도 사용자 요구에 맞게 페이지에 있는 텍스트를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-112">Even if your experience is only provided for a single language, you can customize any text on the pages to suit your needs.</span></span>  

## <a name="how-does-language-customization-work"></a><span data-ttu-id="df5f3-113">언어 사용자 지정이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="df5f3-113">How does Language customization work?</span></span>
<span data-ttu-id="df5f3-114">언어 사용자 지정을 통해 사용자 경험이 제공되는 언어를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-114">Language customization allows you to select which languages your user journey is available in.</span></span>  <span data-ttu-id="df5f3-115">해당 기능을 사용하도록 설정하면 사용자 응용 프로그램에서 쿼리 문자열 매개 변수 ui_locales를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-115">Once the feature is enabled, you can provide the query string parameter, ui_locales, from your application.</span></span>  <span data-ttu-id="df5f3-116">Azure AD B2C를 호출하면 페이지가 표시된 로케일로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-116">When you call into Azure AD B2C, we translate your page to the locale that you have indicated.</span></span>  <span data-ttu-id="df5f3-117">구성 유형을 사용하면 사용자 경험의 언어를 완전히 제어할 수 있고 고객의 브라우저 언어 설정이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-117">Using type of configuration gives you complete control over the languages in your user journey and ignores the language settings of the customer's browser.</span></span> <span data-ttu-id="df5f3-118">또는 고객이 볼 수 있는 언어에 대한 제어 수준이 필요하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-118">Alternatively, you may not need that level of control over what languages your customer see.</span></span>  <span data-ttu-id="df5f3-119">ui_locales 매개 변수를 제공하지 않으면 고객의 환경이 브라우저 설정으로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-119">If you don't provide a ui_locales parameter, the customer's experience is dictated by their browser's settings.</span></span>  <span data-ttu-id="df5f3-120">언어를 지원 언어로 추가하여 사용자 경험이 번역된 언어를 계속 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-120">You can still control which languages your user journey is translated to by adding it as a supported language.</span></span>  <span data-ttu-id="df5f3-121">고객의 브라우저가 지원하지 않으려는 언어를 표시하도록 설정된 경우 지원되는 문화에서 기본값으로 선택한 언어가 대신 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-121">If a customer's browser is set to show a language you don't want to support, then the language you selected as a default in supported cultures is shown instead.</span></span>

1. <span data-ttu-id="df5f3-122">**ui-locales 지정된 언어** - 언어 사용자 지정을 사용하도록 설정한 경우 사용자 경험은 여기에 지정된 언어로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-122">**ui-locales specified language** - Once you enable Language customization, your user journey is translated to the language specified here</span></span>
2. <span data-ttu-id="df5f3-123">**브라우저 요청 언어** - ui-locales가 지정되지 않았고 **지원되는 언어에 포함된 경우** 브라우저 요청 언어로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-123">**Browser requested language** - If no ui-locales was specified, it translates to the browser requested language, **if it was included in Supported languages**</span></span>
3. <span data-ttu-id="df5f3-124">**정책 기본 언어** - 브라우저에서 언어를 지정하지 않거나 지원되지 않는 언어를 지정하면 정책 기본 언어로 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-124">**Policy default language** - If the browser doesn't specify a language, or it specifies one that is not supported, it translates to the policy default language</span></span>

>[!NOTE]
><span data-ttu-id="df5f3-125">사용자 지정 사용자 특성을 사용하는 경우 사용자 고유의 번역을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-125">If you are using custom user attributes, you need to provide your own translations.</span></span> <span data-ttu-id="df5f3-126">자세한 내용은 '[문자열 사용자 지정](#customize-your-strings)'을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df5f3-126">See '[Customize your strings](#customize-your-strings)' for details.</span></span>
>

## <a name="support-uilocales-requested-languages"></a><span data-ttu-id="df5f3-127">ui_locales 요청 언어 지원</span><span class="sxs-lookup"><span data-stu-id="df5f3-127">Support ui_locales requested languages</span></span> 
<span data-ttu-id="df5f3-128">정책에서 '언어 사용자 지정'을 사용하도록 설정하면 ui_locales 매개 변수를 추가하여 사용자 경험의 언어를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-128">By enabling 'Language customization' on a policy, you can now control the language of the user journey by adding the ui_locales parameter.</span></span>
1. [<span data-ttu-id="df5f3-129">다음 단계에 따라 Azure Portal의 B2C 기능 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-129">Follow these steps to navigate to the B2C features blade on the Azure portal.</span></span>](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. <span data-ttu-id="df5f3-130">번역에 사용할 정책으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-130">Navigate to a policy that you want to enable for translations.</span></span>
3. <span data-ttu-id="df5f3-131">**언어 사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-131">Click **Language customization**.</span></span>
4. <span data-ttu-id="df5f3-132">경고를 주의깊게 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-132">Read the warning carefully.</span></span>  <span data-ttu-id="df5f3-133">사용하도록 설정된 후에는 '언어 사용자 지정'을 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-133">Once enabled, you cannot turn off 'Language customization'.</span></span>
5. <span data-ttu-id="df5f3-134">기능을 설정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-134">Turn on the feature and click **OK**.</span></span>
6. <span data-ttu-id="df5f3-135">**정책 편집** 블레이드의 왼쪽 맨 위 모퉁이에서 정책을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-135">Save your policy on the upper left corner of your **Edit policy** blade.</span></span>

## <a name="select-which-languages-your-user-journey-supports"></a><span data-ttu-id="df5f3-136">사용자 경험에서 지원하는 언어 선택</span><span class="sxs-lookup"><span data-stu-id="df5f3-136">Select which languages your user journey supports</span></span> 
<span data-ttu-id="df5f3-137">ui_locales 매개 변수가 제공되지 않을 때 번역할 사용자 경험에 대해 허용되는 언어 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-137">Create a list of allowed languages for your user journey to be translated in when the ui_locales parameter is not provided.</span></span>
1. <span data-ttu-id="df5f3-138">이전 지침에서 정책에 '언어 사용자 지정'이 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-138">Ensure your policy has 'Language customization' enabled from previous instructions.</span></span>
2. <span data-ttu-id="df5f3-139">**정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-139">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="df5f3-140">**지원되는 언어** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-140">You are taken to your **Supported languages** blade.</span></span>  <span data-ttu-id="df5f3-141">여기에서 **언어 추가**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-141">From here, you can select **Add language**.</span></span>
4. <span data-ttu-id="df5f3-142">지원하려는 모든 언어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-142">Select all the languages that you would like to be supported.</span></span>  

>[!NOTE]
><span data-ttu-id="df5f3-143">ui_locales 매개 변수가 제공되지 않으면 페이지가 고객의 브라우저 언어(목록에 있는 경우)로만 번역됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-143">If a ui_locales parameter is not provided, then the page is translated to the customer's browser language only if it is on this list</span></span>
>

5. <span data-ttu-id="df5f3-144">아래쪽에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-144">Click **Ok** at the bottom</span></span>
6. <span data-ttu-id="df5f3-145">**언어 사용자 지정** 블레이드를 닫고 정책을 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-145">Close the **Language customization** blade and **save** your policy.</span></span>

## <a name="customize-your-strings"></a><span data-ttu-id="df5f3-146">문자열 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="df5f3-146">Customize your strings</span></span>
<span data-ttu-id="df5f3-147">'언어 사용자 지정'을 통해 사용자 경험에서 모든 문자열을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-147">'Language customization' allows you to customize any string in your user journey.</span></span>
1. <span data-ttu-id="df5f3-148">이전 지침에서 정책에 '언어 사용자 지정'이 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-148">Ensure your policy has 'Language customization' enabled from the previous instructions.</span></span>
2. <span data-ttu-id="df5f3-149">**정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-149">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="df5f3-150">왼쪽 탐색 메뉴에서 **콘텐츠 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-150">From the left-hand navigation menu, select **Download content**.</span></span>
4. <span data-ttu-id="df5f3-151">편집하려는 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-151">Select the page you want to edit.</span></span>
5. <span data-ttu-id="df5f3-152">드롭다운에서 편집할 언어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-152">In the dropdown, select the language you want to edit for.</span></span>
6. <span data-ttu-id="df5f3-153">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-153">Click **Download**.</span></span> 

<span data-ttu-id="df5f3-154">이러한 단계는 문자열 편집을 시작하는 데 사용할 수 있는 JSON 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-154">These steps give you a JSON file that you can use to start editing your strings.</span></span>

### <a name="changing-any-string-on-the-page"></a><span data-ttu-id="df5f3-155">페이지에서 문자열 변경</span><span class="sxs-lookup"><span data-stu-id="df5f3-155">Changing any string on the page</span></span>
1. <span data-ttu-id="df5f3-156">이전 지침에서 다운로드한 JSON 파일을 JSON 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-156">Open the JSON file downloaded from previous instructions in a JSON editor.</span></span>
2. <span data-ttu-id="df5f3-157">변경할 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-157">Find the element you want to change.</span></span>  <span data-ttu-id="df5f3-158">찾으려는 문자열의 `StringId`를 찾거나 변경할 `Value`를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-158">You can find the `StringId` of the string you are looking for, or look for the `Value` you want to change.</span></span>
3. <span data-ttu-id="df5f3-159">`Value` 특성을 표시하기를 원하는 항목으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-159">Update the `Value` attribute with what you want displayed.</span></span>
4. <span data-ttu-id="df5f3-160">파일을 저장하고 변경 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-160">Save the file and upload your changes.</span></span>

### <a name="changing-extension-attributes"></a><span data-ttu-id="df5f3-161">확장 특성 변경</span><span class="sxs-lookup"><span data-stu-id="df5f3-161">Changing extension attributes</span></span>
<span data-ttu-id="df5f3-162">사용자 지정 사용자 특성의 문자열을 변경하려는 경우 또는 JSON에 문자열을 추가하려는 경우 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-162">If you are looking to change the string for a custom user attribute, or want to add one to the JSON, it is in the following format:</span></span>
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
><span data-ttu-id="df5f3-163">문자열을 재정의해야 하는 경우 `Override` 값을 `true`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-163">If you need to override a string, make sure to set the `Override` value to `true`.</span></span>  <span data-ttu-id="df5f3-164">값이 변경되지 않으면 항목이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-164">If the value isn't changed, the entry is ignored.</span></span> 
>

<span data-ttu-id="df5f3-165">`<ExtensionAttribute>`를 사용자 지정 사용자 특성 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-165">Replace `<ExtensionAttribute>` with the name of your custom user attribute.</span></span>  
<span data-ttu-id="df5f3-166">`<ExtensionAttributeValue>`를 표시할 새 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-166">Replace `<ExtensionAttributeValue>` with the new string to be displayed.</span></span>

### <a name="using-localizedcollections"></a><span data-ttu-id="df5f3-167">LocalizedCollections 사용</span><span class="sxs-lookup"><span data-stu-id="df5f3-167">Using LocalizedCollections</span></span>
<span data-ttu-id="df5f3-168">응답에 대한 값 목록 집합을 지정하려면 `LocalizedCollections`를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-168">If you want to provide a set list of values for responses, you need to create a `LocalizedCollections`.</span></span>  <span data-ttu-id="df5f3-169">`LocalizedCollections`는 `Name` 및 `Value` 쌍의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-169">A `LocalizedCollections` is an array of `Name` and `Value` pairs.</span></span>  <span data-ttu-id="df5f3-170">`Name`은 표시되는 항목이고 `Value`는 클레임에 반환된 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-170">The `Name` is what is displayed and the `Value` is what is returned in the claim.</span></span>  <span data-ttu-id="df5f3-171">`LocalizedCollections`를 추가하기 위해 다음 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-171">To add a `LocalizedCollections`, it has the following format:</span></span>

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
><span data-ttu-id="df5f3-172">문자열을 재정의해야 하는 경우 `Override` 값을 `true`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-172">If you need to override a string, make sure to set the `Override` value to `true`.</span></span>  <span data-ttu-id="df5f3-173">값이 변경되지 않으면 항목이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-173">If the value isn't changed, the entry is ignored.</span></span> 
>

* <span data-ttu-id="df5f3-174">`ElementId`는 이 `LocalizedCollections`가 응답인 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-174">`ElementId` is the user attribute that this `LocalizedCollections` is a response to</span></span>
* <span data-ttu-id="df5f3-175">`Name`은 사용자에게 표시된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-175">`Name` is the value shown to the user</span></span>
* <span data-ttu-id="df5f3-176">`Value`는 이 옵션이 선택될 때 클레임에 반환된 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-176">`Value` is what is returned in the claim when this option is selected</span></span>

### <a name="upload-your-changes"></a><span data-ttu-id="df5f3-177">변경 내용 업로드</span><span class="sxs-lookup"><span data-stu-id="df5f3-177">Upload your changes</span></span>
1. <span data-ttu-id="df5f3-178">JSON 파일에 대한 변경을 완료했으면 B2C 테넌트로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-178">Once you have completed the changes to your JSON file, navigate back to your B2C tenant.</span></span>
2. <span data-ttu-id="df5f3-179">**정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-179">From your **Edit policy** blade, select **Language customization**.</span></span>
3. <span data-ttu-id="df5f3-180">왼쪽 탐색 메뉴에서 **콘텐츠 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-180">From the left-hand navigation menu, select **Upload content**.</span></span>
4. <span data-ttu-id="df5f3-181">변경 내용을 업로드하려는 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-181">Select the page you want to upload your changes for.</span></span>
5. <span data-ttu-id="df5f3-182">이전에 JSON을 제공한 언어를 업로드하려면 이전 항목을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-182">If you want to upload a language that you've previously provided a JSON for, you need to delete the previous entry.</span></span>  <span data-ttu-id="df5f3-183">해당 언어 오른쪽에서 `...`를 클릭하고 **삭제**를 선택하여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-183">You can delete it by clicking the `...` on the right of that language and select **Delete**.</span></span>
6. <span data-ttu-id="df5f3-184">왼쪽 위에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-184">Click **Add** on the upper left.</span></span>
7. <span data-ttu-id="df5f3-185">JSON 파일의 언어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-185">Select the language of your JSON file.</span></span>
8. <span data-ttu-id="df5f3-186">오른쪽에서 폴더 단추를 클릭하고 JSON 파일을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-186">Click the folder button on the right and browse for your JSON file.</span></span>
9. <span data-ttu-id="df5f3-187">블레이드 맨 아래에 있는 **업로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-187">Click the **Upload** button on the bottom of the blade.</span></span>
10. <span data-ttu-id="df5f3-188">**정책 편집** 블레이드로 다시 이동하여 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-188">Go back to your **Edit policy** blade and click **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="df5f3-189">추가 정보</span><span class="sxs-lookup"><span data-stu-id="df5f3-189">Additional information</span></span>
### <a name="recommendations-for-language-customization"></a><span data-ttu-id="df5f3-190">'언어 사용자 지정'에 대한 권장 사항</span><span class="sxs-lookup"><span data-stu-id="df5f3-190">Recommendations for 'Language customization'</span></span>
<span data-ttu-id="df5f3-191">명시적으로 바꾸려는 문자열에 대한 언어 리소스에 항목을 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-191">We recommend only putting in entries to your Language resources for strings you explicitly want to replace.</span></span>  <span data-ttu-id="df5f3-192">모든 JSON 변환에서 컴파일된 파일에 크기 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-192">We enforce a size limit to the file that is compiled out of all your JSON translations.</span></span>  <span data-ttu-id="df5f3-193">파일이 너무 큰 경우 사용자 경험의 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-193">If your files get too large, it impacts the performance of your user journey.</span></span>
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a><span data-ttu-id="df5f3-194">'언어 사용자 지정'을 사용하면 페이지 UI 사용자 지정 레이블이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-194">Page UI customization labels are removed once 'Language customization' is enabled</span></span>
<span data-ttu-id="df5f3-195">'언어 사용자 지정'을 사용하도록 설정하면 사용자 지정 사용자 특성을 제외하고, 페이지 UI 사용자 지정을 사용한 레이블에 대한 이전 편집이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-195">When you enable 'Language customization', your previous edits for labels using Page UI customization are removed except for custom user attributes.</span></span>  <span data-ttu-id="df5f3-196">이 변경은 문자열을 편집할 수 있는 곳에서 충돌을 피하기 위해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-196">This change is done to avoid conflicts in where you can edit your strings.</span></span>  <span data-ttu-id="df5f3-197">'언어 사용자 지정'에서 언어 리소스를 업로드하여 레이블 및 기타 문자열을 계속해서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-197">You can continue to change your labels and other strings by uploading language resources in 'Language customization'.</span></span>
### <a name="microsoft-is-committed-to-provide-the-most-up-to-date-translations-for-your-use"></a><span data-ttu-id="df5f3-198">Microsoft는 사용자가 사용할 수 있는 가장 최신의 번역을 제공하기 위해 최선을 다하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-198">Microsoft is committed to provide the most up-to-date translations for your use</span></span>
<span data-ttu-id="df5f3-199">지속적으로 번역을 개선하고 사용자에 맞게 유지할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-199">We will continuously improve translations and keep them in compliance for you.</span></span>  <span data-ttu-id="df5f3-200">버그 및 글로벌 용어의 변화를 파악하고 사용자 경험에서 원활하게 작동하도록 업데이트할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-200">We will identify bugs and changes in global terminology and make the updates that will work seamlessly in your user journey.</span></span>
### <a name="support-for-right-to-left-languages"></a><span data-ttu-id="df5f3-201">오른쪽에서 왼쪽 언어 지원</span><span class="sxs-lookup"><span data-stu-id="df5f3-201">Support for right-to-left languages</span></span>
<span data-ttu-id="df5f3-202">오른쪽에서 왼쪽 언어에 대한 지원은 없습니다. 이 기능이 필요하면 [Azure 피드백](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag)에서 이 기능에 대해 투표하세요.</span><span class="sxs-lookup"><span data-stu-id="df5f3-202">There is no support for right-to-left languages, if you require this feature please vote for this feature on [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).</span></span>
### <a name="social-identity-provider-translations"></a><span data-ttu-id="df5f3-203">소셜 ID 공급자 변환</span><span class="sxs-lookup"><span data-stu-id="df5f3-203">Social Identity provider translations</span></span>
<span data-ttu-id="df5f3-204">소셜 로그인에 ui_locales OIDC 매개 변수를 제공하지만 Facebook 및 Google을 포함한 일부 소셜 ID 공급자에는 이 매개 변수가 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-204">We provide the ui_locales OIDC parameter to social logins but they are not honored by some social identity providers, including Facebook and Google.</span></span> 
### <a name="browser-behavior"></a><span data-ttu-id="df5f3-205">브라우저 동작</span><span class="sxs-lookup"><span data-stu-id="df5f3-205">Browser behavior</span></span>
<span data-ttu-id="df5f3-206">Chrome 및 Firefox는 모두 설정된 언어를 요청하며 지원되는 언어인 경우 기본값보다 먼저 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-206">Chrome and Firefox both request for their set language and if it is a supported language, it is displayed before the default.</span></span>  <span data-ttu-id="df5f3-207">에지에서는 현재 언어를 요청하지 않으며 기본 언어로 바로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-207">Edge currently does not request a language and goes straight to the default language.</span></span>
### <a name="known-issues"></a><span data-ttu-id="df5f3-208">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="df5f3-208">Known issues</span></span>
* <span data-ttu-id="df5f3-209">프로필 편집 정책에서 MFA 페이지에 대한 언어 리소스 업로드는 현재 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-209">Uploading language resources for the MFA page in a Profile Edit policy is currently unavailable.</span></span>
* <span data-ttu-id="df5f3-210">응답 유형에 필요한 경우 값에 대한 `LocalizedCollections`는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-210">`LocalizedCollections` aren't generated for values when it is required by the response type</span></span>
### <a name="what-if-i-want-a-language-that-isnt-supported"></a><span data-ttu-id="df5f3-211">지원되지 않는 언어가 필요하다면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="df5f3-211">What if I want a language that isn't supported?</span></span>
<span data-ttu-id="df5f3-212">JSON 리소스를 '사용자 지정 언어'로 업로드할 수 있도록 이 기능의 확장을 제공할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-212">We are planning to provide an extension of this feature that allows you to upload a JSON resource towards 'custom languages'.</span></span>  <span data-ttu-id="df5f3-213">이 기능을 사용하면 언어에 대한 이름과 언어 코드를 지정하고 해당 언어에 대한 *모든* 번역을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df5f3-213">The feature allows you to specify the name and language code for any language and provide *all* the translations for that language.</span></span>  <span data-ttu-id="df5f3-214">이 기능이 필요한 경우 [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)으로 시나리오를 보내 주세요.</span><span class="sxs-lookup"><span data-stu-id="df5f3-214">If you need this feature, send us your scenario at [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).</span></span>  

### <a name="what-languages-are-supported"></a><span data-ttu-id="df5f3-215">어떤 언어가 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="df5f3-215">What languages are supported?</span></span>

| <span data-ttu-id="df5f3-216">language</span><span class="sxs-lookup"><span data-stu-id="df5f3-216">Language</span></span>              | <span data-ttu-id="df5f3-217">언어 코드</span><span class="sxs-lookup"><span data-stu-id="df5f3-217">Language code</span></span> |
|-----------------------|---------------|
| <span data-ttu-id="df5f3-218">벵골어</span><span class="sxs-lookup"><span data-stu-id="df5f3-218">Bangla</span></span>                | <span data-ttu-id="df5f3-219">bn</span><span class="sxs-lookup"><span data-stu-id="df5f3-219">bn</span></span>            |
| <span data-ttu-id="df5f3-220">체코어</span><span class="sxs-lookup"><span data-stu-id="df5f3-220">Czech</span></span>                 | <span data-ttu-id="df5f3-221">cs</span><span class="sxs-lookup"><span data-stu-id="df5f3-221">cs</span></span>            |
| <span data-ttu-id="df5f3-222">덴마크어</span><span class="sxs-lookup"><span data-stu-id="df5f3-222">Danish</span></span>                | <span data-ttu-id="df5f3-223">da</span><span class="sxs-lookup"><span data-stu-id="df5f3-223">da</span></span>            |
| <span data-ttu-id="df5f3-224">독일어</span><span class="sxs-lookup"><span data-stu-id="df5f3-224">German</span></span>                | <span data-ttu-id="df5f3-225">de</span><span class="sxs-lookup"><span data-stu-id="df5f3-225">de</span></span>            |
| <span data-ttu-id="df5f3-226">그리스어</span><span class="sxs-lookup"><span data-stu-id="df5f3-226">Greek</span></span>                 | <span data-ttu-id="df5f3-227">el</span><span class="sxs-lookup"><span data-stu-id="df5f3-227">el</span></span>            |
| <span data-ttu-id="df5f3-228">영어</span><span class="sxs-lookup"><span data-stu-id="df5f3-228">English</span></span>               | <span data-ttu-id="df5f3-229">en</span><span class="sxs-lookup"><span data-stu-id="df5f3-229">en</span></span>            |
| <span data-ttu-id="df5f3-230">스페인어</span><span class="sxs-lookup"><span data-stu-id="df5f3-230">Spanish</span></span>               | <span data-ttu-id="df5f3-231">es</span><span class="sxs-lookup"><span data-stu-id="df5f3-231">es</span></span>            |
| <span data-ttu-id="df5f3-232">핀란드어</span><span class="sxs-lookup"><span data-stu-id="df5f3-232">Finnish</span></span>               | <span data-ttu-id="df5f3-233">fi</span><span class="sxs-lookup"><span data-stu-id="df5f3-233">fi</span></span>            |
| <span data-ttu-id="df5f3-234">프랑스어</span><span class="sxs-lookup"><span data-stu-id="df5f3-234">French</span></span>                | <span data-ttu-id="df5f3-235">fr</span><span class="sxs-lookup"><span data-stu-id="df5f3-235">fr</span></span>            |
| <span data-ttu-id="df5f3-236">구자라트어</span><span class="sxs-lookup"><span data-stu-id="df5f3-236">Gujarati</span></span>              | <span data-ttu-id="df5f3-237">gu</span><span class="sxs-lookup"><span data-stu-id="df5f3-237">gu</span></span>            |
| <span data-ttu-id="df5f3-238">힌디어</span><span class="sxs-lookup"><span data-stu-id="df5f3-238">Hindi</span></span>                 | <span data-ttu-id="df5f3-239">hi</span><span class="sxs-lookup"><span data-stu-id="df5f3-239">hi</span></span>            |
| <span data-ttu-id="df5f3-240">크로아티아어</span><span class="sxs-lookup"><span data-stu-id="df5f3-240">Croatian</span></span>              | <span data-ttu-id="df5f3-241">hr</span><span class="sxs-lookup"><span data-stu-id="df5f3-241">hr</span></span>            |
| <span data-ttu-id="df5f3-242">헝가리어</span><span class="sxs-lookup"><span data-stu-id="df5f3-242">Hungarian</span></span>             | <span data-ttu-id="df5f3-243">hu</span><span class="sxs-lookup"><span data-stu-id="df5f3-243">hu</span></span>            |
| <span data-ttu-id="df5f3-244">이탈리아어</span><span class="sxs-lookup"><span data-stu-id="df5f3-244">Italian</span></span>               | <span data-ttu-id="df5f3-245">it</span><span class="sxs-lookup"><span data-stu-id="df5f3-245">it</span></span>            |
| <span data-ttu-id="df5f3-246">일본어</span><span class="sxs-lookup"><span data-stu-id="df5f3-246">Japanese</span></span>              | <span data-ttu-id="df5f3-247">ja</span><span class="sxs-lookup"><span data-stu-id="df5f3-247">ja</span></span>            |
| <span data-ttu-id="df5f3-248">카나다어</span><span class="sxs-lookup"><span data-stu-id="df5f3-248">Kannada</span></span>               | <span data-ttu-id="df5f3-249">kn</span><span class="sxs-lookup"><span data-stu-id="df5f3-249">kn</span></span>            |
| <span data-ttu-id="df5f3-250">한국어</span><span class="sxs-lookup"><span data-stu-id="df5f3-250">Korean</span></span>                | <span data-ttu-id="df5f3-251">ko</span><span class="sxs-lookup"><span data-stu-id="df5f3-251">ko</span></span>            |
| <span data-ttu-id="df5f3-252">말라얄람어</span><span class="sxs-lookup"><span data-stu-id="df5f3-252">Malayalam</span></span>             | <span data-ttu-id="df5f3-253">ml</span><span class="sxs-lookup"><span data-stu-id="df5f3-253">ml</span></span>            |
| <span data-ttu-id="df5f3-254">마라티어</span><span class="sxs-lookup"><span data-stu-id="df5f3-254">Marathi</span></span>               | <span data-ttu-id="df5f3-255">mr</span><span class="sxs-lookup"><span data-stu-id="df5f3-255">mr</span></span>            |
| <span data-ttu-id="df5f3-256">말레이어</span><span class="sxs-lookup"><span data-stu-id="df5f3-256">Malay</span></span>                 | <span data-ttu-id="df5f3-257">ms</span><span class="sxs-lookup"><span data-stu-id="df5f3-257">ms</span></span>            |
| <span data-ttu-id="df5f3-258">노르웨이어 복말</span><span class="sxs-lookup"><span data-stu-id="df5f3-258">Norwegian Bokmal</span></span>      | <span data-ttu-id="df5f3-259">nb</span><span class="sxs-lookup"><span data-stu-id="df5f3-259">nb</span></span>            |
| <span data-ttu-id="df5f3-260">네덜란드어</span><span class="sxs-lookup"><span data-stu-id="df5f3-260">Dutch</span></span>                 | <span data-ttu-id="df5f3-261">nl</span><span class="sxs-lookup"><span data-stu-id="df5f3-261">nl</span></span>            |
| <span data-ttu-id="df5f3-262">펀잡어</span><span class="sxs-lookup"><span data-stu-id="df5f3-262">Punjabi</span></span>               | <span data-ttu-id="df5f3-263">pa</span><span class="sxs-lookup"><span data-stu-id="df5f3-263">pa</span></span>            |
| <span data-ttu-id="df5f3-264">폴란드어</span><span class="sxs-lookup"><span data-stu-id="df5f3-264">Polish</span></span>                | <span data-ttu-id="df5f3-265">pl</span><span class="sxs-lookup"><span data-stu-id="df5f3-265">pl</span></span>            |
| <span data-ttu-id="df5f3-266">포르투갈어 - 브라질</span><span class="sxs-lookup"><span data-stu-id="df5f3-266">Portuguese - Brazil</span></span>   | <span data-ttu-id="df5f3-267">pt-br</span><span class="sxs-lookup"><span data-stu-id="df5f3-267">pt-br</span></span>         |
| <span data-ttu-id="df5f3-268">포르투갈어 - 포르투갈</span><span class="sxs-lookup"><span data-stu-id="df5f3-268">Portuguese - Portugal</span></span> | <span data-ttu-id="df5f3-269">pt-pt</span><span class="sxs-lookup"><span data-stu-id="df5f3-269">pt-pt</span></span>         |
| <span data-ttu-id="df5f3-270">루마니아어</span><span class="sxs-lookup"><span data-stu-id="df5f3-270">Romanian</span></span>              | <span data-ttu-id="df5f3-271">ro</span><span class="sxs-lookup"><span data-stu-id="df5f3-271">ro</span></span>            |
| <span data-ttu-id="df5f3-272">러시아어</span><span class="sxs-lookup"><span data-stu-id="df5f3-272">Russian</span></span>               | <span data-ttu-id="df5f3-273">ru</span><span class="sxs-lookup"><span data-stu-id="df5f3-273">ru</span></span>            |
| <span data-ttu-id="df5f3-274">슬로바키아어</span><span class="sxs-lookup"><span data-stu-id="df5f3-274">Slovak</span></span>                | <span data-ttu-id="df5f3-275">sk</span><span class="sxs-lookup"><span data-stu-id="df5f3-275">sk</span></span>            |
| <span data-ttu-id="df5f3-276">스웨덴어</span><span class="sxs-lookup"><span data-stu-id="df5f3-276">Swedish</span></span>               | <span data-ttu-id="df5f3-277">sv</span><span class="sxs-lookup"><span data-stu-id="df5f3-277">sv</span></span>            |
| <span data-ttu-id="df5f3-278">타밀어</span><span class="sxs-lookup"><span data-stu-id="df5f3-278">Tamil</span></span>                 | <span data-ttu-id="df5f3-279">ta</span><span class="sxs-lookup"><span data-stu-id="df5f3-279">ta</span></span>            |
| <span data-ttu-id="df5f3-280">텔루구어</span><span class="sxs-lookup"><span data-stu-id="df5f3-280">Telugu</span></span>                | <span data-ttu-id="df5f3-281">te</span><span class="sxs-lookup"><span data-stu-id="df5f3-281">te</span></span>            |
| <span data-ttu-id="df5f3-282">태국어</span><span class="sxs-lookup"><span data-stu-id="df5f3-282">Thai</span></span>                  | <span data-ttu-id="df5f3-283">th</span><span class="sxs-lookup"><span data-stu-id="df5f3-283">th</span></span>            |
| <span data-ttu-id="df5f3-284">터키어</span><span class="sxs-lookup"><span data-stu-id="df5f3-284">Turkish</span></span>               | <span data-ttu-id="df5f3-285">tr</span><span class="sxs-lookup"><span data-stu-id="df5f3-285">tr</span></span>            |
| <span data-ttu-id="df5f3-286">중국어 - 간체</span><span class="sxs-lookup"><span data-stu-id="df5f3-286">Chinese - Simplified</span></span>  | <span data-ttu-id="df5f3-287">zh-hans</span><span class="sxs-lookup"><span data-stu-id="df5f3-287">zh-hans</span></span>       |
| <span data-ttu-id="df5f3-288">중국어 - 번체</span><span class="sxs-lookup"><span data-stu-id="df5f3-288">Chinese - Traditional</span></span> | <span data-ttu-id="df5f3-289">zh-hant</span><span class="sxs-lookup"><span data-stu-id="df5f3-289">zh-hant</span></span>       |
