---
title: "hello Azure Active Directory 연결 마법사를 사용 하 여 aaaHow toodiagnose 오류"
description: "hello active directory 연결 마법사가 호환 되지 않는 인증 유형 검색"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Hello Azure Active Directory 연결 마법사를 사용 하 여 오류 진단
이전 인증 코드를 검색 하는 동안 hello 마법사에는 호환 되지 않는 인증 형식을 검색 했습니다.   

## <a name="what-is-being-checked"></a>무엇을 확인합니까?
**참고:** toocorrectly 프로젝트에서 이전 인증 코드를 검색할 hello 프로젝트를 빌드해야 합니다.  이 오류가 발생했고 프로젝트에 이전 인증 코드가 없는 경우 다시 작성한 다음 다시 시도합니다.

### <a name="project-types"></a>프로젝트 형식
hello 마법사 hello 형식의 hello 프로젝트로 hello 오른쪽 인증 논리를 삽입할 수 있으므로 개발 하는 프로젝트를 확인 합니다.  파생 되는 컨트롤러가 `ApiController` hello 프로젝트 hello 프로젝트에 WebAPI 프로젝트도 간주 됩니다.  파생 되는 컨트롤러에만 있는 경우 `MVC.Controller` hello 프로젝트 hello 프로젝트에 MVC 프로젝트도 간주 됩니다.  그 외 모든 hello 마법사에서 지원 되지 않습니다.

### <a name="compatible-authentication-code"></a>호환 가능한 인증 코드
또한 hello 마법사 hello 마법사로 이전에 구성 된 또는 hello 마법사와 호환 되는 인증 설정을 확인 합니다.  모든 설정이 있으면 재진입용 경우 것으로 간주 됩니다 및 hello 마법사가 열리고 hello 설정을 표시 합니다.  Hello 설정의 일부 값이 있는 경우에 오류 사례를 간주 됩니다.

MVC 프로젝트에서 hello 마법사 hello 설정을 hello 마법사의 이전 사용 결과로 생성 되는 다음 중 하나에 대 한 확인:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

또한 hello 마법사 hello hello 마법사의 이전 사용 결과로 생성 되는 설정은 웹 API 프로젝트에서 다음 중 하나에 대 한 확인:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>호환되지 않는 인증 코드
마지막으로, hello 마법사는 이전 버전의 Visual Studio로 구성 된 toodetect 버전의 인증 코드를 시도 합니다. 이 오류가 발생한 경우에는 프로젝트에 호환되지 않는 인증 코드가 있음을 의미합니다. hello 마법사 hello를 유형의 인증 이전 버전의 Visual Studio에서 다음을 찾습니다.

* Windows 인증 
* 개별 사용자 계정 
* 조직 계정 

hello에 대 한 MVC 프로젝트에 Windows 인증을 toodetect, hello 마법사에서는 `authentication` 요소에서 사용자 **web.config** 파일입니다.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

hello에 대 한 웹 API 프로젝트에 Windows 인증을 toodetect, hello 마법사에서는 `IISExpressWindowsAuthentication` 프로젝트의 요소 **.csproj** 파일:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

hello 패키지 요소에 대 한 toodetect 개별 사용자 계정 인증 hello 마법사에서는 프로그램 **Packages.config** 파일입니다.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

요소 다음에 오는 hello에 대 한 오래 된 형태의 조직 계정 인증 toodetect hello 마법사에서는 **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

toochange hello 인증 유형을 hello 호환 되지 않는 인증 유형을 제거 하 고 hello 마법사를 다시 실행 합니다.

자세한 내용은 [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)를 참조하세요.

#<a name="next-steps"></a>다음 단계
- [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)