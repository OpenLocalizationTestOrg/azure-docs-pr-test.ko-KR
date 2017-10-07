---
title: "UI(사용자 인터페이스) 사용자 지정 - Azure AD B2C | Microsoft Docs"
description: "Azure Active Directory B2C hello 사용자 인터페이스 (UI) 사용자 지정 기능에 항목"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a>Azure Active Directory B2C: hello Azure AD B2C UI (사용자 인터페이스) 사용자 지정

사용자 환경은 고객 관련 응용 프로그램에서 가장 중요합니다.  고객의 브랜드 hello 모양과 느낌으로 사용자 환경을 만들어 기본 증가 합니다. Azure AD B2C(Azure Active Directory B2C)를 사용하면 픽셀을 완벽하게 제어하여 등록, 로그인, 프로필 편집 및 암호 재설정 페이지를 사용자 지정할 수 있습니다.

> [!NOTE]
> 유일한 정책 로그인 toohello, 함께 제공 된 암호 재설정 페이지 및 확인 전자 메일에는이 문서에서 설명 하는 hello 페이지 UI 사용자 지정 기능이 적용 되지 않습니다.  Hello를 사용 하는 이러한 기능 [회사 브랜딩 기능](../active-directory/active-directory-add-company-branding.md) 대신 합니다.
>

이 문서에서는 hello 다음 항목을 다룹니다.

* hello 페이지 UI 사용자 지정 기능입니다.
* Hello 페이지 UI 사용자 지정 기능에 사용할 HTML 콘텐츠 tooAzure Blob 저장소에 업로드 하기 위한 도구입니다.
* hello UI 요소 (CSS 스타일 시트)를 사용 하 여 사용자 지정할 수 있는 Azure AD B2C에서 사용 합니다.
* 이 기능을 실행할 때 모범 사례입니다.

## <a name="hello-page-ui-customization-feature"></a>hello 페이지 UI 사용자 지정 기능

고객 등록, 로그인, 암호의 hello 모양과 느낌을 사용자 지정할 수 다시 설정 및 프로필 편집 페이지 (구성 하 여 [정책](active-directory-b2c-reference-policies.md)). 고객이 Azure AD B2C에 의해 제공된 응용 프로그램과 페이지 간에 이동하는 경우 원활한 환경을 유지합니다.

여기서 UI 옵션, 단순 및 최신 Azure AD B2C 사용 하 여 접근 tooUI 사용자 지정 하는 다른 서비스와 달리

작동 방식은 다음과 같습니다. Azure AD B2C는 소비자의 브라우저에서 코드를 실행하고 [CORS(원본 간 리소스 공유)](http://www.w3.org/TR/cors/)라는 최신의 방법을 사용합니다.  런타임에, 정책에서 지정한 URL에서 콘텐츠가 로드됩니다. 다른 페이지에 다른 URL을 지정할 수 있습니다. Azure AD B2C에서 삽입 되는 HTML 부분으로 URL에서 로드 한 콘텐츠가 병합 후 hello 페이지는 표시 된 tooyour 고객입니다. 다음은 toodo 가장 필요한 것입니다.

1. 올바른 형식의 HTML5 비어 있는 콘텐츠 만들 `<div id="api"></div>` 요소 hello에 어딘가에 있는 `<body>`합니다. Azure AD B2C 콘텐츠 hello 삽입 되는 위치를 표시 하는 요소입니다.
1. (허용된 CORS로)HTTPS 끝점의 콘텐츠를 호스트합니다. CORS를 구성할 때 GET 및 OPTIONS 요청 메서드를 둘 다 사용하도록 설정해야 합니다.
1. Azure AD B2C를 삽입 하는 CSS toostyle hello UI 요소를 사용 합니다.

### <a name="a-basic-example-of-customized-html"></a>사용자 지정된 HTML의 기본 예제

다음 예제는 hello hello 가장 기본적인 HTML 콘텐츠에 사용할 수 있는 tootest이이 기능입니다. 사용 하 여 hello [도우미 도구](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload 및 Azure Blob 저장소에이 콘텐츠를 구성 합니다. 그런 다음 각 페이지에서 양식 필드 및 hello basic, 비 양식 화 단추는 표시 되 고 있으며 제대로 작동을 확인할 수 있습니다.

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a>Hello UI 사용자 지정 기능을 미리 테스트

샘플 HTML 및 CSS 콘텐츠를 사용 하 여 hello UI 사용자 지정 기능을 미리 tootry를 선택 하십시오.  Azure Blob Storage에 샘플 콘텐츠를 업로드하고 구성하는 [도우미 도구](active-directory-b2c-reference-ui-customization-helper-tool.md)를 제공하고 있습니다.

> [!NOTE]
> 웹 서버, CDN, AWS S3, 파일 공유 시스템 등 어느 곳에나 UI 콘텐츠를 호스트할 수 있습니다. Hello 콘텐츠를 사용 하도록 설정 하는 CORS를 공개적으로 사용할 수 있는 HTTPS 끝점에서 호스트 된으로 좋은 toogo 됩니다. Azure Blob 저장소를 설명 목적으로만 사용합니다.
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a>Azure AD B2C로 포함 하는 hello UI 조각

hello 다음 섹션에 나열 되어 Azure AD B2C hello에 병합 하는 HTML5 hello 부분이 `<div id="api"></div>` 콘텐츠에 있는 요소입니다. **HTML 5 콘텐츠에 이러한 조각을 삽입하지 마십시오.** hello Azure AD B2C 서비스 실행 시에 삽입합니다. 사용자 고유의 CSS 스타일 시트를 디자인할 때 이러한 조각을 참조하세요.

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a>"Id 공급자 선택 페이지" hello에 조각 삽입

이 페이지에는 사용자 hello 공급자 등록 또는 로그인 중에서 선택할 수는 id의 목록을 포함 합니다. 이러한 단추에는 Facebook, Google+ 또는 로컬 계정(메일 주소 또는 사용자 이름 기반)과 같은 소셜 ID 공급자가 포함됩니다.

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a>Hello "로컬 계정 등록 페이지"에 삽입 된 조각

이 페이지에는 전자 메일 주소 또는 사용자 이름을 기준으로 하는 로컬 계정 등록 양식이 있습니다. hello 양식 텍스트 입력된 상자, 암호 입력 상자, 라디오 단추, 단일 선택 드롭다운 목록 상자, 다중 선택 확인란 등 서로 다른 입력된 컨트롤을 포함할 수 있습니다.

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a>"" 사회 account 등록 페이지"hello에 조각 삽입

이 페이지는 Facebook 또는 Google+와 같은 소셜 ID 공급자에서 기존 계정을 사용하여 등록하는 경우 나타날 수 있습니다.  등록 양식을 사용 하 여 hello 최종 사용자 로부터 추가 정보를 수집 해야 하는 경우 사용 됩니다. 이 페이지는 비슷한 toohello 로컬 계정 등록 페이지 (hello 이전 섹션에 표시) hello 암호 입력 필드의 hello 예외를 사용 합니다.

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a>"통합 등록 또는 로그인 페이지" hello에 조각 삽입

이 페이지는 Facebook 또는 Google+ 또는 로컬 계정과 같은 소셜 ID 공급자를 사용할 수 있는 고객의 등록 및 로그인을 모두 다룹니다.

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a>"Multi-factor authentication 페이지" hello에 삽입 된 조각

이 페이지에서 등록 또는 로그인하는 동안 사용자가 텍스트 또는 음성을 사용하여 전화 번호를 확인할 수 있습니다.

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a>"" 오류 페이지"hello에 조각 삽입

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a>HTML 콘텐츠 지역화

['언어 사용자 지정'](active-directory-b2c-reference-language-customization.md)을 설정하여 HTML 콘텐츠를 지역화할 수 있습니다.  Azure AD B2C tooforward hello Open ID 연결 매개 변수를 사용 하면이 기능을 사용 하면 `ui-locales`, tooyour 끝점입니다.  위해 콘텐츠 서버 언어 관련 된이 매개 변수 tooprovide 사용자 지정 된 HTML 페이지를 사용할 수 있습니다.

## <a name="things-tooremember-when-building-your-own-content"></a>작업 tooremember 내용을 직접 빌드할 때

Toouse hello 페이지 UI 사용자 지정 기능을 계획 하는 경우에 hello 최선의 구현 방법을 검토 합니다.

* Hello Azure AD B2C 기본 콘텐츠 복사 및 toomodify를 시도 하지 않는 것입니다. 것은 최상의 toobuild HTML5 콘텐츠를 참조로 처음 및 toouse 기본 콘텐츠입니다.
* 보안상의 이유로 것을 허용 하지 않습니다 tooinclude 콘텐츠에 모든 JavaScript 합니다. 대부분의 필요한 hello 유틸리티로 제공 해야 합니다. 그렇지 않은 경우 사용 하 여 [사용자 음성](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest 새로운 기능입니다.
* 지원되는 브라우저 버전:
  * Internet Explorer 11, 10, Edge
  * Internet Explorer 9, 8에 대한 지원 제한
  * Google Chrome 42.0 이상
  * Mozilla Firefox 38.0 이상
