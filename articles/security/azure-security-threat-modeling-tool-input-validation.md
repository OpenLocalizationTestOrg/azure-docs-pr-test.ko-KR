---
title: "유효성 검사-Microsoft 위협 모델링 도구-Azure aaaInput | Microsoft Docs"
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
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>보안 프레임: 입력 유효성 검사 | 완화 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **웹 응용 프로그램** | <ul><li>[신뢰할 수 없는 스타일시트를 사용하는 모든 변환에 대해 XSLT 스크립팅을 사용하지 않도록 설정](#disable-xslt)</li><li>[사용자가 제어할 수 있는 콘텐츠를 포함할 수 있는 각 페이지가 자동 MIME 스니핑에서 옵트아웃하는지 확인](#out-sniffing)</li><li>[XML 엔터티 확인 확정 또는 사용 중지](#xml-resolution)</li><li>[http.sys를 활용하는 응용 프로그램에서 URL 정형화 확인 수행](#app-verification)</li><li>[사용자의 파일을 허용할 때 적절한 제어가 수행되는지 확인](#controls-users)</li><li>[웹 응용 프로그램에서 데이터 액세스를 위해 형식이 안전한 매개 변수를 사용하는지 확인](#typesafe)</li><li>[별도 모델 필터 목록 tooprevent MVC 대량 할당 취약점을 바인딩 또는 바인딩 클래스를 사용 하 여](#binding-mvc)</li><li>[신뢰할 수 없는 웹 출력 이전 toorendering 인코딩](#rendering)</li><li>[모든 문자열 형식 모델 속성에 대한 입력 유효성 검사 및 필터링 수행](#typemodel)</li><li>[모든 문자를 허용하는 양식 필드(예: 서식 있는 텍스트 편집기)에서 삭제 적용](#richtext)</li><li>[기본 제공 된 인코딩 갖지 않는 DOM 요소 toosinks를 할당 하지 마십시오](#inbuilt-encode)</li><li>[모든 유효성 검사 hello 응용 프로그램 내에서 리디렉션을 닫히거나 안전 하 게 수행](#redirect-safe)</li><li>[컨트롤러 메서드에서 허용하는 모든 문자열 형식 매개 변수에 대한 입력 유효성 검사 구현](#string-method)</li><li>[정규식 toobad 정규식 인해 tooprevent DoS 처리에 대 한 최대 제한 시간 제한 설정](#dos-expression)</li><li>[Razor 보기에서 Html.Raw 사용 방지](#html-razor)</li></ul> | 
| **데이터베이스** | <ul><li>[저장 프로시저에서 동적 쿼리 사용 금지](#stored-proc)</li></ul> |
| **앱 API** | <ul><li>[모델 유효성 검사가 Web API 메서드에서 수행되는지 확인](#validation-api)</li><li>[Web API 메서드에서 허용하는 모든 문자열 형식 매개 변수에 대한 입력 유효성 검사 구현](#string-api)</li><li>[Web API에서 데이터 액세스를 위해 형식이 안전한 매개 변수를 사용하는지 확인](#typesafe-api)</li></ul> | 
| **Azure Document DB** | <ul><li>[DocumentDB에 매개 변수가 있는 SQL 쿼리 사용](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[WCF - 스키마 바인딩을 통한 입력 유효성 검사](#schema-binding)</li><li>[WCF - 매개 변수 검사기를 통한 입력 유효성 검사](#parameters)</li></ul> |

## <a id="disable-xslt"></a>신뢰할 수 없는 스타일시트를 사용하는 모든 변환에 대해 XSLT 스크립팅을 사용하지 않도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [XSLT 보안](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [XsltSettings.EnableScript 속성](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **단계** | XSLT 스타일 시트 hello를 사용 하 여 내부 스크립팅을 지원 `<msxml:script>` 요소입니다. 그러면 XSLT 변환에 사용 된 사용자 지정 함수 toobe 있습니다. hello 스크립트 hello 변환을 수행 하는 hello 프로세스의 hello 컨텍스트 내에서 실행 됩니다. 신뢰할 수 없는 코드의 신뢰할 수 없는 환경 tooprevent 실행에 있는 경우 XSLT 스크립트를 사용 하지 않도록 설정 해야 합니다. *하지만.NET을 사용 하는 경우:* XSLT 스크립트는 기본적으로 해제 하 고 설정 되어 있지 않은 명시적으로 hello를 통해 확인 해야; `XsltSettings.EnableScript` 속성입니다.|

### <a name="example"></a>예제 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>예제
기본적으로 XSLT 스크립트는 비활성화 되어 MSXML 6.0을 사용 하 여를 사용 하는 경우 그러나는 설정 되어 있지 않은 명시적으로 AllowXsltScript hello XML DOM 개체 속성을 통해 확인 해야 합니다. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>예제
MSXML 5 이하를 사용하는 경우 XSLT 스크립팅은 기본적으로 활성화되며, 명시적으로 사용하지 않도록 설정해야 합니다. Hello XML DOM 개체 속성 AllowXsltScript toofalse를 설정 합니다. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>사용자가 제어할 수 있는 콘텐츠를 포함할 수 있는 각 페이지가 자동 MIME 스니핑에서 옵트아웃하는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [IE8 보안 5부 - 포괄적 보호](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)(영문)  |
| **단계** | <p>사용자가 제어할 수 있는 콘텐츠를 포함할 수 있는 각 페이지에 대 한 hello HTTP 헤더를 사용 해야 `X-Content-Type-Options:nosniff`합니다. 이 요구 사항의 toocomply, 어느 집합 hello 필수 헤더 사용자를 제어할 수 있는 콘텐츠가 포함 될 수 있는 해당 페이지에 대 한 페이지 단위로 하거나 hello 응용 프로그램의 모든 페이지에 대 한 전역적으로 설정할 수 있습니다.</p><p>웹 서버에서 전달 하는 파일의 각 형식에 연결 된 [MIME 형식을](http://en.wikipedia.org/wiki/Mime_type) (라고도 *콘텐츠-유형*) hello 콘텐츠 (즉, 이미지, 텍스트, 응용 프로그램 등)의 hello 특성을 설명 하는</p><p>X-콘텐츠-유형-옵션 hello 헤더는 개발자가 사용할 수 있는 HTTP 헤더는 해당 콘텐츠 되지 않아야 MIME 스니핑 toospecify 합니다. 이 헤더는 디자인 된 toomitigate MIME 스니핑 공격입니다. IE8(Internet Explorer 8)에는 이 헤더에 대한 지원이 추가되었습니다.</p><p>IE8 사용자만 X-Content-Type-Options의 이점을 얻을 수 있습니다. 이전 버전의 Internet Explorer hello X-콘텐츠-유형-옵션 헤더를 현재 적용 되지 않습니다.</p><p>Internet Explorer 8 이상 주요 브라우저 MIME 스니핑 tooimplement 옵트아웃 기능만을 hello 됩니다. 이 권장 사항은 이러한 브라우저에 대 한 업데이트 된 tooinclude 구문이 됩니다 유사한 기능을 구현 하는 주요 브라우저 (Safari, Firefox, Chrome) 경우</p>|

### <a name="example"></a>예제
hello 응용 프로그램의 모든 페이지에 대 한 전역적으로 tooenable hello의 필수 헤더를 hello 다음 중 하나를 수행할 수 있습니다. 

* Hello 응용 프로그램에는 인터넷 정보 서비스 (IIS) 7에서 호스팅되는 경우 hello 헤더 hello web.config 파일에 추가 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Hello 통해 hello 헤더 추가 전역 응용 프로그램\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* 사용자 지정 HTTP 모듈을 구현합니다. 

``` 
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
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* Tooindividual 응답을 추가 하 여 특정 페이지에 대해서만 hello 필수 헤더를 설정할 수 있습니다. 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>XML 엔터티 확인 확정 또는 사용 중지

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [XML 엔터티 확장](http://capec.mitre.org/data/definitions/197.html)(영문), [XML DoS(서비스 거부) 공격 및 방어](http://msdn.microsoft.com/magazine/ee335713.aspx)(영문), [MSXML 보안 개요](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [MSXML 코드 보안에 대한 모범 사례](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [NSXMLParserDelegate 프로토콜 참조](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html)(영문), [외부 참조 확인](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **단계**| <p>널리 사용 되지 않습니다 이지만 hello XML 파서 tooexpand 매크로 엔터티 hello 문서 자체 내에서 또는 외부 원본에서 정의 된 값으로 허용 하는 XML의 기능입니다. 예를 들어 통해 hello 문서 때마다 hello 텍스트를 "companyname" hello "Microsoft" 값을 가진 엔터티를 정의할 수 있습니다 "&companyname;"은 자동으로 Microsoft hello 텍스트로 대체 hello 문서에 나타납니다. 또는 hello 문서는 외부 웹 서비스 toofetch hello의 현재 값 Microsoft 재고를 참조 하는 "MSFTStock" 엔터티를 정의할 수 있습니다.</p><p>언제 든 지 다음 "&MSFTStock;" hello 현재 주가으로 자동으로 대체 됩니다 hello 문서에 나타납니다. 그러나이 기능은 악용 toocreate 서비스 거부 (DoS) 조건 수 있습니다. 공격자가 여러 엔터티 toocreate hello 시스템에서 사용 가능한 모든 메모리를 소비 하는 지 수 확장 XML 폭탄 중첩할 수 있습니다. </p><p>또는 그 뒤로 스트림 하는 외부 참조가 무기한 데이터의 만들거나 단순히 hello 스레드를 중단 하는. 결과적으로, 모든 팀 해야 사용 하지 않도록 설정 내부 및/또는 외부 XML 엔터티 해상도 응용 프로그램을 사용 하지 않거나 수동으로 hello 크기의 메모리 및 hello 응용 프로그램에서이 기능을 하는 경우 엔터티 확인을 위해 사용할 수 있는 시간을 제한 하는 경우에 완전 하 게 반드시 필요 합니다. 응용 프로그램에서 엔터티 확인이 필요하지 않은 경우 엔터티 확인을 사용하지 않도록 설정합니다. </p>|

### <a name="example"></a>예제
.NET Framework 코드에 대 한 다음 방법 hello를 사용할 수 있습니다.

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
해당 hello 기본 값을 기록해 둡니다 `ProhibitDtd` 에 `XmlReaderSettings` 하지만 true 이면 `XmlTextReader` 은 false입니다. XmlReaderSettings를 사용 하는 경우 tooset ProhibitDtd tootrue를 명시적으로 필요 하지 않습니다 하지만 것이 좋습니다 안전 위해서는 방어막 수행할 수 있습니다. 또한 hello XmlDocument 클래스는 기본적으로 엔터티 확인을 수 있습니다. 

### <a name="example"></a>예제
XmlDocuments 사용 하 여 hello에 대 한 엔터티 확인 toodisable `XmlDocument.Load(XmlReader)` hello의 오버 로드가 Load 메서드 속성을 설정 hello 적절 한 hello XmlReader 인수 toodisable 확인에 hello 코드 다음에 설명 된 대로: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>예제
엔터티 확인을 사용 하지 않도록 설정, 응용 프로그램에 가져올 수 없으면 hello XmlReaderSettings.MaxCharactersFromEntities 속성 tooa 적당 한 값 tooyour 응용 프로그램의 요구에 따라 설정 합니다. 이 지 수 확장 DoS 공격 가능성의 hello 영향을 제한 합니다. 이 방법의 예제를 제공 하는 코드 다음 hello: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>예제
Tooresolve 인라인 엔터티 필요 하지만 tooresolve 외부 엔터티 불필요 경우 hello XmlReaderSettings.XmlResolver 속성 toonull를 설정 합니다. 예: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Note는 MSXML6의 ProhibitDTD tootrue (DTD 처리를 사용 하지 않으면) 기본적으로 설정 됩니다. Apple OSX/iOS 코드의 경우 두 가지 XML 파서, NSXMLParser 및 libXML2를 사용할 수 있습니다. 

## <a id="app-verification"></a>http.sys를 활용하는 응용 프로그램에서 URL 정형화 확인 수행

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>http.sys를 사용하는 모든 응용 프로그램은 다음 지침을 따라야 합니다.</p><ul><li>Hello URL 길이 toono 개 이상의 16, 384 문자 (ASCII 또는 유니코드)을 제한 합니다. Hello 절대 최대 URL 길이 hello 기본 인터넷 정보 서비스 (IIS) 6 설정에 따라입니다. 웹 사이트에서는 가능한 경우 이 길이보다 더 짧도록 노력해야 합니다.</li><li>이 활용할 hello 정규화 규칙에서.NET FX hello 대로 hello 표준.NET Framework 파일 I/O 클래스 (예: FileStream)를 사용 하 여</li><li>알려진 파일 이름의 허용 목록을 명시적으로 작성합니다.</li><li>UrlScan 거부를 제공하지 않는 것으로 알려진 파일 형식(exe, bat, cmd, com, htw, ida, idq, htr, idc, shtm[l], stm, printer, ini, pol, dat 파일)을 명시적으로 거부합니다.</li><li>Hello 다음 예외를 catch:<ul><li>System.ArgumentException(장치 이름의 경우)</li><li>System.NotSupportedException(데이터 스트림의 경우)</li><li>System.IO.FileNotFoundException(잘못된 이스케이프 문자를 사용한 파일 이름의 경우)</li><li>System.IO.DirectoryNotFoundException(잘못된 이스케이프 문자를 사용한 디렉터리의 경우)</li></ul></li><li>*없는* tooWin32 파일 I/O Api를 호출 합니다. 잘못 된 URL에서 400 오류 toohello 사용자 정상적으로 반환 하 고 hello 실제 오류를 기록.</li></ul>|

## <a id="controls-users"></a>사용자의 파일을 허용할 때 적절한 제어가 수행되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [무제한 파일 업로드](https://www.owasp.org/index.php/Unrestricted_File_Upload)(영문), [파일 서명 테이블](http://www.garykessler.net/library/file_sigs.html)(영문) |
| **단계** | <p>업로드 된 파일은 상당한 위험 tooapplications를 나타냅니다.</p><p>대부분의 공격이 hello 첫 번째 단계에는 일부 코드 toohello 시스템 toobe 공격 tooget 것입니다. 그런 다음 hello 공격 toofind 방식으로 tooget hello 코드가 실행만 필요 합니다. 파일 업로드를 사용 하 여 hello 첫 번째 단계를 수행 하는 hello 공격자는 데 도움이 됩니다. 전체 시스템 인수는 오버 로드 된 파일 시스템 또는 데이터베이스를 전달 공격 tooback 엔드 시스템의 경우 및 단순 손상과 비롯 하 여 무제한 파일 업로드의 hello 결과 달라질 수 있습니다.</p><p>어떤 hello 응용 프로그램을 업로드 하는 hello 파일과 함께 수행 하 고 저장 위치에 특히에 따라 다릅니다. 파일 업로드에 대한 서버 쪽 유효성 검사는 없습니다. 파일 업로드 기능에 대해 다음과 같은 보안 제어를 구현해야 합니다.</p><ul><li>파일 확장명 검사(허용되는 파일 형식의 유효한 집합만)</li><li>최대 파일 크기 제한</li><li>파일에는 업로드 된 toowebroot;를 사용 해야 합니다. hello 위치 비시스템 드라이브의 디렉터리에 있어야 합니다.</li><li>명명 규칙을 따라야도 록 hello 업로드 된 파일 이름 일부 임의성 파일을 덮어씁니다 tooprevent으로 하므로</li><li>Toohello 디스크를 쓰기 전에 바이러스 백신에 대 한 파일을 검색할 수 해야</li><li>Hello 파일 이름 및 다른 메타 데이터 (예: 파일 경로) 악의적인 문자에 대 한 유효성이 검사 됩니다 확인</li><li>파일 형식 서명을 확인 해야 tooprevent masqueraded 파일 업로드 사용자 (예: 확장 tootxt 변경 하 여 exe 파일 업로드)</li></ul>| 

### <a name="example"></a>예제
파일 형식에 대 한 서명 유효성 검사에 대 한 마지막 지점 hello에 대 한 자세한 내용은 아래 toohello 클래스를 참조 하세요. 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>웹 응용 프로그램에서 데이터 액세스를 위해 형식이 안전한 매개 변수를 사용하는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>Hello 매개 변수 컬렉션을 사용 하는 경우 실행 코드가 아니라 리터럴 값으로 SQL에서는 hello 입력이 있습니다. hello 매개 변수 컬렉션에는 입력된 데이터에 사용 되는 tooenforce 형식 및 길이 제약 조건 수 있습니다. Hello 범위 밖의 값에는 예외가 발생합니다. 형식 안정적 SQL 매개 변수 사용 되지 않는 경우 공격자가 필터링 되지 않은 hello 입력에 포함 하는 수 tooexecute 삽입 공격을 수 있습니다.</p><p>Tooavoid 가능한 SQL 삽입 공격 필터링 되지 않은 입력 발생할 수 있는 쿼리를 SQL을 생성 하는 경우 형식 안전 매개 변수를 사용 합니다. 저장 프로시저 및 동적 SQL 문과 함께 형식이 안전한 매개 변수를 사용할 수 있습니다. 매개 변수는 실행 코드가 아닌 리터럴 값 hello 데이터베이스에 의해로 처리 됩니다. 또한 매개 변수의 형식 및 길이에 대해서도 검사합니다.</p>|

### <a name="example"></a>예제 
hello 다음 코드에서는 저장된 프로시저를 호출할 때 toouse SqlParameterCollection hello로 안전 하 게 보호 매개 변수를 입력 하는 방법을 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Hello 코드 예제에서는 앞에에서 hello 입력된 값을 11 자 보다 길 수 없습니다. Hello 데이터 toohello 형식 또는 hello 매개 변수에 의해 정의 된 길이 준수 하지 않는, 경우 hello SqlParameter 클래스 예외를 throw 합니다. 

## <a id="binding-mvc"></a>별도 모델 필터 목록 tooprevent MVC 대량 할당 취약점을 바인딩 또는 바인딩 클래스를 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [메타 데이터 특성](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [공개 키 보안 취약성을 완화](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [완벽 가이드 tooMass ASP.NET MVC에서 할당](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [MVC를 사용해 EF 시작](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **단계** | <ul><li>**과도한 게시 취약성은 언제 찾아야 합니까? -** 사용자 입력에서 모델 클래스를 바인딩하는 모든 위치에서 과도한 게시 취약성이 발생할 수 있습니다. MVC와 같은 프레임워크는 POCO(Plain Old CLR Object)를 포함하여 사용자 지정 .NET 클래스의 사용자 데이터를 나타낼 수 있습니다. MVC를 자동으로 채우려고 hello 요청에서 데이터를 사용 하 여 이러한 모델 클래스 사용자 입력 처리 하기 위한 편리한 표현을 제공 합니다. 이러한 클래스에는 hello 사용자가 설정 하지 않아야 하는 속성, hello 응용 프로그램 하지 hello 응용 프로그램 의도 하는 데이터의 사용자 정의 컨트롤 수 있는 tooover 게시 공격에 취약 한 될 수 있습니다. MVC 모델 바인딩와 같은 Entity Framework와 같은 개체 관계형 매퍼 같은 데이터베이스 액세스 기술을 POCO 개체 toorepresent 데이터베이스 데이터를 사용 하 여 자주도 지원 합니다. 이러한 데이터 모델 클래스 제공 hello MVC 사용자 입력으로 처리 하는 데에서 마찬가지로 데이터베이스 데이터를 처리할 때 동일한 편리 합니다. MVC 및 hello 모두 데이터베이스 POCO 개체와 같은 비슷한 모델을 지원 하기 때문에 두 가지 용도로 클래스 동일 쉽게 tooreuse hello 같습니다. 이 연습 실패 하면 toopreserve 분리 우려 사항, 그리고이 공통 영역은 의도 하지 않은 속성 노출 toomodel 바인딩, 초과 게시 공격을 사용 하도록 설정 합니다.</li><li>**매개 변수 toomy MVC 동작으로 내 필터링 되지 않은 데이터베이스 모델 클래스를 사용 하지 않아야는 이유 -** 때문에 MVC 모델 바인딩은 아무 것도 해당 클래스에 바인딩합니다. 데이터 표시 되지 않습니다 보기에 악의적인 사용자,이 데이터와 HTTP 요청을 보낼 수는 hello 및 MVC는 기꺼이 바인딩할 액션 것으로 표시 database 클래스 hello 모양의 데이터 때문에 경우에 사용자 입력을 허용 해야 합니다.</li><li>**모델 바인딩에 대 한 사용 되는 hello 모양을 대 한 고려해 야 -** 너무 광범위 한 모델을 사용 하 여 ASP.NET MVC 모델 바인딩 응용 프로그램 게시 tooover 공격 노출 합니다. 과도 하 게 게시 하는 중 어떤 hello 개발자가 계정에 대 한 프로그램 항목 또는 hello 보안 권한에 대 한 hello 가격을 재정의 하는 등 의도 한 초과 하 여 공격자가 toochange 응용 프로그램 데이터를 설정 될 수 있습니다. 응용 프로그램 모델 바인딩을 통해 신뢰할 수 없는 입력된 tooallow 어떤 작업별 모델 (또는 특정 허용 되는 속성 필터 목록) 바인딩 tooprovide 명시적 계약을 사용 해야 합니다.</li><li>**코드를 복제하는 별도의 바인딩 모델이 있습니까? -** 아니요, 이는 중요한 부분의 분리 문제입니다. 작업 메서드에서 데이터베이스 모델을 다시 사용 하면 받는지 모든 속성 (또는 하위 속성) hello HTTP 요청에는 사용자가 클래스를 설정할 수 있다는 점에서 합니다. 결과 원하지 않은 MVC toodo 필터 목록이 나 해야 별도 클래스 셰이프 tooshow MVC 사용자 대신 입력에서 어떤 데이터를 가져올 수 있습니다.</li><li>**사용자 입력에 대 한 별도 바인딩을 모델 있으면 용량은 tooduplicate 내 모든 데이터 주석 특성 -** 필요는 없습니다. MetadataTypeAttribute hello 데이터베이스 모델 클래스 toolink toohello 메타 데이터에는 모델 바인딩 클래스에 사용할 수 있습니다. Hello MetadataTypeAttribute 참조 형식 hello 정당한 참고 (가질 수 있습니다 더 하지 하지만 속성이 더 적게) 형식을 참조 하는 hello의 하위 집합 이어야 합니다.</li><li>**사용자 입력 모델과 데이터베이스 모델 간에 데이터를 앞뒤로 이동하는 것은 지루한 작업입니다. 리플렉션을 사용하여 모든 속성을 복사할 수 있습니까? -** 예. hello만 속성 hello 바인딩 모델에 나타나는 toobe 사용자 입력에 안전으로 확인 된 hello 것입니다. 이러한 두 모델 간의 공통 존재 하는 모든 속성에 대해 리플렉션을 toocopy를 사용 하는 것을 금지 하는 보안 않아도가 됩니다.</li><li>**[Bind(Exclude ="â€¦")]는 어떻습니까? 별도의 바인딩 모델을 사용하는 대신 이 특성을 사용할 수 있습니까? -** 이 방법은 권장되지 않습니다. [Bind(Exclude ="â€¦")]를 사용하면 새 속성 모두를 기본적으로 바인딩할 수 있습니다. 새 속성이 추가 되는 경우는 안전 추가 단계 tooremember tookeep 작업 대신 hello 디자인 설정 기본적으로 안전 합니다. Hello 개발자에 따라 속성에 추가 될 때마다이 목록 확인은 위험 합니다.</li><li>**[Bind(Include ="â€¦")]는 편집 작업에 유용합니까? -** 아니요. [Bind(Include ="â€¦")]는 삽입 방식 작업(새 데이터 추가)에만 적합합니다. (기존 데이터를 수정) 스타일 업데이트 작업에 명시적 목록이 허용 되는 속성 tooUpdateModel 또는 TryUpdateModel 전달 하거나 별도 바인딩을 모델 같은 다른 방법을 사용 합니다. 추가 [바인딩합니다 (Include = "â € 해 보아야")] MVC는 개체 인스턴스를 만들고 설정 하나만 hello 표시 속성을 기본값으로 유지 하는 다른 모든 특성 편집 작업을 의미 합니다. Hello 데이터가 유지 되 면 완전히 바꾸게 됩니다 hello 기존 엔터티를 생략된 속성 tootheir 기본값에 대 한 hello 값 다시 설정 합니다. IsAdmin에서 누락 된 경우 등는 [바인딩합니다 (Include = "â € 해 보아야")] 특성 편집 작업에서 모든 사용자 이름이이 동작을 통해 편집 재설정 tooIsAdmin 것 = false (편집 된 모든 사용자는 관리자 상태 손실 없음). Tooprevent toocertain 속성을 업데이트 하려면 중 하나를 사용 hello 위의 다른 방법입니다. 일부 버전의 MVC 도구는 [Bind(Include ="â€¦")]를 포함한 컨트롤러 클래스를 편집 작업에서 생성하며, 해당 목록에서 속성을 제거하면 과도한 게시 공격이 방지됩니다. 그러나 위에서 설명한 대로 해당 접근 의도 한 대로 작동 하지 않습니다 않으며 대신에 생략 hello 속성 tootheir 기본 값의 데이터를 다시 설정 됩니다.</li><li>**만들기 작업의 경우 별도의 바인딩 모델이 아닌 [Bind(Include ="â€¦")]를 사용하는 데 주의해야 합니까? -** 예. 첫째, 이 방법은 편집 시나리오에서 작동하지 않으므로 모든 과도한 게시 취약성을 완화하기 위해서는 별도의 두 가지 방법을 유지해야 합니다. 지 속성을 사용 하는 사용자 입력 및 hello 셰이프에 사용 된 hello 셰이프 간의 문제의 분리를 적용 하는 두 번째, 별도 바인딩을 모델 항목 [바인딩합니다 (포함 "â € 해 보아야" =)] 하지 않습니다. 셋째, 유의 [바인딩합니다 (Include = "â € 해 보아야")] 최상위 속성;만 처리할 수 있습니다 hello 특성에 (예: "Details.Name") 하위 속성의 일부만 허용할 수 없습니다. 와 마지막으로, 가장 중요 하 게 사용 하 여 [바인딩할 (Include = "â € 해 보아야")] 시간 hello 클래스 모델 바인딩의 사용 저장 해야 하는 추가 단계를 추가 합니다. 새 작업 메서드에 toohello 데이터 클래스에 직접 바인딩합니다 tooinclude 잊은 경우는 [바인딩합니다 (포함 "â € 해 보아야" =)] 특성 수 취약 한 tooover 게시 공격 하므로 hello [바인딩할 (포함 "â € 해 보아야" =)] 방법은 기본적으로 상대적으로 덜 안전 합니다. 사용 하는 경우 [바인딩 (Include = "â € 해 보아야")], tooremember toospecify 항상 처리할 데이터 클래스 동작 메서드 매개 변수로 표시 될 때마다 해당 합니다.</li><li>**Hello를 배치 하는 방법에 대 한 어떤 만들기 작업에 대 한 [바인딩합니다 (Include = "â € 해 보아야")] 특성 hello 모델 클래스 자체에? 이 방법을 사용 하지 hello 필요 tooremember 배치 hello 특성에 있는 모든 작업 메서드에 방지 하려면? -** 경우에 따라이 방법은 작동 합니다. 사용 하 여 [바인딩할 (포함 = "â € 해 보아야")] hello 모델 형식 자체에 (아닌이 클래스를 사용 하 여 액션 매개 변수), hello 필요 tooremember tooinclude hello 방지 않습니다 [바인딩할 (포함 "â € 해 보아야" =)] 모든 작업 메서드에 특성을 합니다. Hello 클래스에서 직접 hello 특성을 효과적으로 사용 모델 바인딩 목적에 대 한이 클래스의 별도 노출 영역을 만듭니다. 그러나 이 방법은 모델 클래스마다 모델 바인딩 셰이프 하나만 허용합니다. 하나의 작업 메서드가 해야 tooallow 모델 바인딩 필드 (예를 들어, 관리자 전용 업데이트 하는 동작 사용자 역할)의 다른 작업에는이 필드의 tooprevent 모델 바인딩 필요 하는 경우이 방법은 작동 하지 않습니다. 각 클래스는 모델 바인딩 모양을; 하나만 사용할 수 있습니다. 67gb toorepresent 이러한 별도 모델 바인딩 클래스 중 하나를 사용 하 여 셰이프를 별도 열 데이터 나 별도 동작이 서로 다른 여러 가지 모델 바인딩 셰이프를 필요 [바인딩할 (Include = "â € 해 보아야")] hello 작업 메서드에 특성입니다.</li><li>**바인딩 모델이란 무엇입니까? 모델 보기와 같은 작업을 hello? -** 는 두 개의 관련된 개념입니다. 바인딩 모델에에서 사용 되는 tooa 모델 클래스를 참조 하는 hello 용어는 매개 변수 목록 (hello 셰이프 MVC 모델 바인딩 toohello 작업 메서드에서 전달). hello 용어 뷰 모델 동작 메서드 tooa 보기에서 전달 된 tooa 모델 클래스를 참조 합니다. 보기 관련 모델을 사용 하는 동작 메서드 tooa 보기에서 데이터를 전달 하기 위한 일반적인 방법입니다. 대개이 셰이프는 모델 바인딩에 대 한 적합도 및 hello 용어 뷰 모델에 사용 되는 toorefer hello 양쪽 모두에서 같은 모델에 사용 되는 일 수 있습니다. toobe 정확 하 게,이 절차 바인딩 대량 할당을 위해 중요 한 toohello 동작을 전달 하는 hello 모양에 중점을 두기 모델에 대 한 구체적으로 설명 합니다.</li></ul>| 

## <a id="rendering"></a>신뢰할 수 없는 웹 출력 이전 toorendering 인코딩

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, Web Forms, MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [어떻게 ASP.NET의 tooprevent 교차 사이트 스크립팅](http://msdn.microsoft.com/library/ms998274.aspx), [교차 사이트 스크립팅](http://cwe.mitre.org/data/definitions/79.html), [XSS (교차 사이트 스크립팅) 방지 치트 시트](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **단계** | 사이트 간 (약어로 XSS) 스크립팅은 온라인 서비스 또는 hello 웹에서 입력을 사용 하는 응용 프로그램 구성에 대 한 공격입니다. XSS 취약점 취약 한 웹 응용 프로그램을 통해 다른 사용자의 컴퓨터에서 공격자 tooexecute 스크립트를 허용할 수 있습니다. 악의적인 스크립트 사용된 toosteal 쿠키를 수 있으며 JavaScript 통해 희생자의 컴퓨터와 무단 변경 됩니다. XSS는 사용자 입력의 유효성을 검사하고 웹 페이지에 렌더링하기 전에 형식과 인코딩이 올바른지 확인함으로써 방지됩니다. 입력 유효성 검사 및 출력 인코딩은 Web Protection Library를 사용하여 수행할 수 있습니다. 관리 코드에 대 한 (C\#, VB.net 등), 하나를 사용 하거나 hello hello 사용자 입력 매니페스트 가져옵니다 hello 컨텍스트에 따라 웹 보호 (앤티 XSS) 라이브러리에서에서 인코딩 방법 보다 적절 합니다.| 

### <a name="example"></a>예제

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>모든 문자열 형식 모델 속성에 대한 입력 유효성 검사 및 필터링 수행

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [유효성 검사 추가](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation), [MVC 응용 프로그램에서 모델 데이터 유효성 검사](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)(영문), [ASP.NET MVC 응용 프로그램을 위한 기본 원칙](http://msdn.microsoft.com/magazine/dd942822.aspx)(영문) |
| **단계** | <p>사용 하기 전에 hello 응용 프로그램 tooensure에 악의적인 사용자 입력에 대 한 hello 응용 프로그램 보호는 모든 hello 입력된 매개 변수의 유효성을 검사 해야 합니다. 화이트 리스트 유효성 검사 전략으로 서버 쪽에서 유효성 검사 정규식을 사용 하 여 hello 입력된 값의 유효성을 검사 합니다. 사용자 입력을 unsanitized / toohello 메서드에 전달 된 매개 변수 코드 주입 취약점 발생할 수 있습니다.</p><p>웹 응용 프로그램의 경우 양식 필드, QueryStrings, 쿠키, HTTP 헤더 및 웹 서비스 매개 변수가 진입점에 포함될 수도 있습니다.</p><p>hello 다음 입력된 유효성 검사 수행 해야 모델 바인딩에 따라:</p><ul><li>허용된 되는 문자 및 최대 허용 길이 수락 하는 것에 대 한 정규식으로 주석이로 주석을 달아야 hello 모델 속성</li><li>ModelState 유효성을 수행 해야 하는 hello 컨트롤러 메서드</li></ul>|

## <a id="richtext"></a>모든 문자를 허용하는 양식 필드(예: 서식 있는 텍스트 편집기)에서 삭제 적용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [안전하지 않은 입력 인코딩](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3)(영어), [HTML 삭제기](https://github.com/mganss/HtmlSanitizer)(영어) |
| **단계** | <p>정적으로 toouse 원하는 모든 태그를 식별 합니다. 일반적인 방법은 서식 toosafe HTML 요소와 같은 toorestrict `<b>` (굵게) 및 `<i>` (기울임꼴)입니다.</p><p>HTML 인코딩할 hello 데이터를 쓰기 전에 것입니다. 이렇게 하면 toobe 시켜 안전 악성 스크립트 실행 코드가 아니라 텍스트로 처리 됩니다.</p><ol><li>ASP.NET 요청 hello를 추가 하 여 유효성 검사 ValidateRequest hello 사용 안 함 = "false" 특성 toohello @ Page 지시문</li><li>Hello 문자열 입력 hello HtmlEncode 메서드로 인코딩</li><li>StringBuilder 및 해당 바꾸기 메서드 tooselectively toopermit 원하는 hello HTML 요소에서 인코딩을 hello를 제거 하는 호출을 사용 하 여</li></ol><p>hello hello에 대 한 페이지 참조 ASP.NET 요청 유효성 검사 설정 하 여 해제 `ValidateRequest="false"`합니다. 이 HTML로 인코딩하고 hello 입력과 hello를 선택적으로 허용 `<b>` 및 `<i>` 또는 HTML 삭제에 대 한.NET 라이브러리 사용 될 수도 있습니다.</p><p>HtmlSanitizer는 HTML 조각 및 tooXSS 공격을 야기할 수 있는 구문에서 문서를 정리 하기 위해.NET 라이브러리입니다. AngleSharp tooparse 사용 하 여, 조작 및 HTML 및 CSS를 렌더링 합니다. NuGet 패키지로 HtmlSanitizer 설치할 수 있으며이 메서드를 통해 관련 CSS 또는 HTML 삭제가, hello 서버 쪽에서 해당 hello 사용자 입력을 전달할 수 있습니다. 보안 제어로서의 삭제는 마지막 옵션으로만 고려해야 합니다.</p><p>입력 유효성 검사 및 출력 인코딩은 보다 효과적인 보안 제어로 간주됩니다.</p> |

## <a id="inbuilt-encode"></a>기본 제공 된 인코딩 갖지 않는 DOM 요소 toosinks를 할당 하지 마십시오

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 다양한 JavaScript 함수는 기본적으로 인코딩을 수행하지 않습니다. 이러한 함수를 통해 신뢰할 수 없는 입력된 tooDOM 요소에 할당할 때 교차 사이트 (XSS) 스크립트 실행 될 수 있습니다.| 

### <a name="example"></a>예제
다음은 안전하지 않은 예제입니다. 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
`innerHtml`을 사용하지 않는 대신 `innerText`를 사용합니다. 마찬가지로 `$("#elm").html()` 대신 `$("#elm").text()`를 사용합니다. 

## <a id="redirect-safe"></a>모든 유효성 검사 hello 응용 프로그램 내에서 리디렉션을 닫히거나 안전 하 게 수행

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [OAuth 2.0 Authorization Framework-hello Open 리디렉터](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **단계** | <p>리디렉션 tooa 사용자가 제공한 위치를 요구 하는 응용 프로그램 디자인 hello 가능한 리디렉션 tooa 미리 정의 된 "안전한"의 대상 목록 사이트 또는 도메인을 제한 해야 합니다. Hello 응용 프로그램에서 모든 리디렉션이 종료/안전 해야 합니다.</p><p>toodo이:</p><ul><li>모든 리디렉션을 식별합니다.</li><li>리디렉션마다 적절한 완화를 구현합니다. 적절한 완화에는 리디렉션 허용 목록 또는 사용자 확인이 포함됩니다. 오픈 리디렉션 취약성이 있는 웹 사이트 또는 서비스에서 Facebook/OAuth/OpenID ID 공급자를 사용하는 경우 공격자가 사용자의 로그온 토큰을 도용하여 해당 사용자를 가장할 수 있습니다. 이 내재 된 위험 RFC 6749 "hello OAuth 2.0 권한 부여 프레임 워크"에 설명 되어 있는 OAuth를 사용 하는 경우, 마찬가지로 10.15 "열고 리디렉션합니다" 섹션, 스피어 피싱 공격 열려 리디렉션을 사용 하 여 사용자의 자격 증명을 손상 될 수 있습니다.</li></ul>|

## <a id="string-method"></a>컨트롤러 메서드에서 허용하는 모든 문자열 형식 매개 변수에 대한 입력 유효성 검사 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [MVC 응용 프로그램에서 모델 데이터 유효성 검사](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)(영문), [ASP.NET MVC 응용 프로그램을 위한 기본 원칙](http://msdn.microsoft.com/magazine/dd942822.aspx)(영문) |
| **단계** | 인수로 모델이 아니라 기본 데이터 형식만 허용하는 메서드의 경우 정규식을 사용하여 입력 유효성 검사를 수행해야 합니다. 여기서는 Regex.IsMatch를 유효한 정규식 패턴과 함께 사용해야 합니다. Hello 입력와 일치 하지 않으면 지정 된 정규식 hello, 컨트롤 추가, 계속 진행 하지 않아야 및 유효성 검사 실패와 관련 된 적절 한 경고를 표시 합니다.| 

## <a id="dos-expression"></a>정규식 toobad 정규식 인해 tooprevent DoS 처리에 대 한 최대 제한 시간 제한 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, Web Forms, MVC5, MVC6  |
| **특성**              | 해당 없음  |
| **참조**              | [DefaultRegexMatchTimeout 속성](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **단계** | tooensure 서비스 거부 공격에 대 한 hello 전역 기본 제한 시간을 설정 잘못 시키는 많은 역 추적 정규식을 생성 합니다. Hello 처리 시간이 hello 상한값 정의 된 것 보다 더 오래 걸리면에 시간 제한 예외를 throw 합니다. 구성 되는 것을 hello timeout 한정 된 것입니다.| 

### <a name="example"></a>예제
예를 들어 hello 다음과 같은 구성이 throw 합니다는 RegexMatchTimeoutException hello 처리 5 초 넘게 걸리는 경우: 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>Razor 보기에서 Html.Raw 사용 방지

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| 단계 | ASP.Net WebPages(Razor)는 자동 HTML 인코딩을 수행합니다. 포함된 코드 너깃(@ 블록)으로 인쇄된 모든 문자열은 자동으로 HTML로 인코딩됩니다. 그러나 `HtmlHelper.Raw` 메서드가 호출되면 HTML로 인코딩되지 않은 태그를 반환합니다. 경우 `Html.Raw()` hello 자동 인코딩 보호 Razor 제공 하는 과정이 생략, 도우미 메서드를 사용 합니다.|

### <a name="example"></a>예제
다음은 안전하지 않은 예제입니다. 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
사용 하지 마십시오 `Html.Raw()` toodisplay 태그 경우를 제외 합니다. 이 메서드는 암시적으로 출력 인코딩을 수행하지 않습니다. 다른 ASP.NET 도우미(예: `@Html.DisplayFor()`)를 사용합니다. 

## <a id="stored-proc"></a>저장 프로시저에서 동적 쿼리 사용 금지

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>Hello 데이터베이스에 입력된 유효성 검사 toorun 임의의 명령이의 취약점을 악용 하는 SQL 삽입 공격입니다. 발생할 수 있습니다 응용 프로그램이 입력된 tooconstruct 동적을 사용 하는 경우 SQL 문을 tooaccess hello 데이터베이스입니다. 또한 코드에서 원시 사용자 입력을 포함한 문자열이 전달되는 저장 프로시저를 사용하는 경우에도 발생할 수 있습니다. SQL 삽입 공격 hello를 사용 하 여 hello 데이터베이스의 hello 공격자가 임의의 명령을 실행할 수 있습니다. (저장된 프로시저의 hello SQL 문을 포함)는 모든 SQL 문에 매개 변수가 있어야 합니다. 매개 변수가 있는 SQL 문을 강력한 형식 때문에 문제 없이 (예: 작은따옴표) tooSQL을 특별 한 의미를 가진 문자를 허용 합니다. |

### <a name="example"></a>예제
다음은 안전하지 않은 동적 저장 프로시저의 예제입니다. 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>예제
다음은 동일한 저장된 프로시저가 안전 하 게 구현 하는 hello: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>모델 유효성 검사가 Web API 메서드에서 수행되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET Web API의 모델 유효성 검사](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)(영문) |
| **단계** | 클라이언트가 데이터 tooa web API 보내면는 필수 toovalidate hello 데이터 처리를 수행 하기 전에입니다. 입력으로 모델을 허용 하는 ASP.NET 웹 Api에 대 한 hello 모델의 hello 속성에 대 한 모델 tooset 유효성 검사 규칙에 데이터 주석을 사용 합니다.|

### <a name="example"></a>예제
hello 코드 다음 동일한 hello 하는 방법을 보여 줍니다. 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>예제
Hello API 컨트롤러 동작 메서드에 hello hello 모델의 유효성에는 아래와 같이 명시적으로 확인 toobe 있습니다. 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Web API 메서드에서 허용하는 모든 문자열 형식 매개 변수에 대한 입력 유효성 검사 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, MVC 5, MVC 6 |
| **특성**              | 해당 없음  |
| **참조**              | [MVC 응용 프로그램에서 모델 데이터 유효성 검사](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)(영문), [ASP.NET MVC 응용 프로그램을 위한 기본 원칙](http://msdn.microsoft.com/magazine/dd942822.aspx)(영문) |
| **단계** | 인수로 모델이 아니라 기본 데이터 형식만 허용하는 메서드의 경우 정규식을 사용하여 입력 유효성 검사를 수행해야 합니다. 여기서는 Regex.IsMatch를 유효한 정규식 패턴과 함께 사용해야 합니다. Hello 입력와 일치 하지 않으면 지정 된 정규식 hello, 컨트롤 추가, 계속 진행 하지 않아야 및 유효성 검사 실패와 관련 된 적절 한 경고를 표시 합니다.|

## <a id="typesafe-api"></a>Web API에서 데이터 액세스를 위해 형식이 안전한 매개 변수를 사용하는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>Hello 매개 변수 컬렉션을 사용 하는 경우 실행 코드가 아니라 리터럴 값으로 SQL에서는 hello 입력이 있습니다. hello 매개 변수 컬렉션에는 입력된 데이터에 사용 되는 tooenforce 형식 및 길이 제약 조건 수 있습니다. Hello 범위 밖의 값에는 예외가 발생합니다. 형식 안정적 SQL 매개 변수 사용 되지 않는 경우 공격자가 필터링 되지 않은 hello 입력에 포함 하는 수 tooexecute 삽입 공격을 수 있습니다.</p><p>Tooavoid 가능한 SQL 삽입 공격 필터링 되지 않은 입력 발생할 수 있는 쿼리를 SQL을 생성 하는 경우 형식 안전 매개 변수를 사용 합니다. 저장 프로시저 및 동적 SQL 문과 함께 형식이 안전한 매개 변수를 사용할 수 있습니다. 매개 변수는 실행 코드가 아닌 리터럴 값 hello 데이터베이스에 의해로 처리 됩니다. 또한 매개 변수의 형식 및 길이에 대해서도 검사합니다.</p>|

### <a name="example"></a>예제
hello 다음 코드에서는 저장된 프로시저를 호출할 때 toouse SqlParameterCollection hello로 안전 하 게 보호 매개 변수를 입력 하는 방법을 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Hello 코드 예제에서는 앞에에서 hello 입력된 값을 11 자 보다 길 수 없습니다. Hello 데이터 toohello 형식 또는 hello 매개 변수에 의해 정의 된 길이 준수 하지 않는, 경우 hello SqlParameter 클래스 예외를 throw 합니다. 

## <a id="sql-docdb"></a>Cosmos DB에 매개 변수가 있는 SQL 쿼리 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Document DB | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [DocumentDB에서 SQL 매개 변수 지정 발표](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/)(영문) |
| **단계** | DocumentDB는 읽기 전용 쿼리만 지원하지만 사용자 입력과 연결하여 쿼리를 구성하면 여전히 SQL 삽입이 가능합니다. Hello 내에서 액세스 하지 않아야 하는 사용자 toogain 액세스 toodata 수 있습니다 악성 SQL 쿼리를 만들어 동일한 컬렉션입니다. 사용자 입력을 기반으로 하여 쿼리를 구성한 경우 매개 변수가 있는 SQL를 사용합니다. |

## <a id="schema-binding"></a>WCF - 스키마 바인딩을 통한 입력 유효성 검사

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **단계** | <p>유효성 검사의 부족 toodifferent 형식 삽입 공격을 안내합니다.</p><p>메시지 유효성 검사를 한 줄을의 WCF 응용 프로그램의 hello 보호에는 심층적인 방어를 나타냅니다. 이 방법에서는 악성 클라이언트의 공격 으로부터 스키마 tooprotect WCF 서비스 작업을 사용 하 여 메시지 유효성 검사 합니다. 악성 서비스에서 공격 으로부터 hello 클라이언트 tooprotect hello 클라이언트에서 받은 모든 메시지의 유효성을 검사 합니다. 메시지 유효성 검사를 사용 하면 가능한 toovalidate 메시지 operations 소비할 메시지 계약 또는 데이터 계약을 수정할 수 없는 경우 매개 변수 유효성 검사를 사용 하 여 합니다. 메시지 유효성 검사 스키마에 있으므로 더 많은 유연성을 제공 하 고 개발 시간 단축 내 toocreate 유효성 검사 논리를 허용 합니다. 스키마는 데이터 표현에 대 한 표준을 만들 hello 조직 내에서 다른 응용 프로그램에서 다시 사용할 수 있습니다. 또한 메시지 유효성 검사가 있습니다 tooprotect 작업을 계약을 나타내는 비즈니스 논리를 포함 하는 더 복잡 한 데이터 형식을 사용할 때.</p><p>tooperform 메시지 유효성 검사를 먼저 만듭니다 hello 작업이 해당 작업에 사용 된 서비스 및 hello 데이터 형식을 표시 하는 스키마. 그런 다음 사용자 지정 클라이언트 메시지 검사자와 사용자 정의 디스패처 메시지 검사자 toovalidate hello 메시지 hello 서비스에서 보낸/받은 구현 하는.NET 클래스를 만듭니다. 그런 다음 hello 클라이언트와 hello 서비스에 사용자 지정 끝점 동작 tooenable 메시지 유효성 검사를 구현 합니다. 마지막으로, tooexpose hello hello 서비스 또는 클라이언트 hello hello 구성 파일에서 사용자 지정 끝점 동작 확장을 허용 하는 hello 클래스에는 사용자 지정 구성 요소를 구현할 "</p>|

## <a id="parameters"></a>WCF - 매개 변수 검사기를 통한 입력 유효성 검사

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **단계** | <p>입력 및 데이터 유효성 검사는 WCF 응용 프로그램의 hello 보호에는 심층적인 방어의 중요 한 줄을 나타냅니다. 악성 클라이언트를 공격 으로부터 WCF 서비스 작업 tooprotect hello 서비스에 노출 된 모든 매개 변수를 확인 해야 합니다. 반대로, 악성 서비스에서 공격 으로부터 hello 클라이언트 tooprotect hello 클라이언트에서 받는 모든 반환 값도 확인 해야</p><p>WCF는 사용자 지정 확장 프로그램을 만들어 toocustomize hello WCF 런타임 동작을 허용 하는 다른 확장성 지점을 제공 합니다. 메시지 검사자와 매개 변수 검사자는 두 개의 확장성 메커니즘 사용 toogain는 클라이언트와 서비스 간에 전달 되는 hello 데이터에 대 한 제어 강화 합니다. 입력된 유효성 검사에 대 한 매개 변수 검사자를 사용 하 고 서비스 내부 및 외부로 흐르는 tooinspect hello 전체 메시지를 필요할 때만 메시지 검사자를 사용 해야 합니다.</p><p>tooperform 입력 유효성 검사,.NET 클래스를 빌드하고 적절 toovalidate 작업에 대 한 매개 변수에서 서비스에 사용자 지정 매개 변수 검사자를 구현 합니다. 그런 다음 클라이언트 hello와 hello 서비스에 사용자 지정 끝점 동작 tooenable 유효성 검사를 구현 합니다. 마지막으로, tooexpose hello hello 서비스 또는 클라이언트 hello hello 구성 파일에서 사용자 지정 끝점 동작 확장을 허용 하는 hello 클래스에는 사용자 지정 구성 요소를 구현 합니다.</p>|
