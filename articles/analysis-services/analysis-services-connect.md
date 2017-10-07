---
title: Analysis Services aaaConnect tooAzure | Microsoft Docs
description: "Tooconnect tooand Azure에서 Analysis Services 서버에서 데이터를 가져오기 하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Tooan Azure Analysis Services 서버에 연결

이 문서에서는 데이터 모델링 및 SQL Server Management Studio (SSMS) 또는 SQL Server Data Tools (SSDT)와 같은 관리 응용 프로그램을 사용 하 여 tooa 서버 연결을 설명 합니다. 또는 Microsoft Excel, Power BI Desktop 또는 사용자 지정 응용 프로그램과 같은 클라이언트 보고 응용 프로그램을 사용합니다. HTTPS를 사용 하는 연결 tooAzure Analysis Services.

## <a name="client-libraries"></a>클라이언트 라이브러리
[Hello 최신 클라이언트 라이브러리를 얻을](analysis-services-data-providers.md)

형식에 관계 없이 모든 연결 tooa 서버에 업데이트 된 AMO, ADOMD.NET 및 OLEDB 클라이언트 라이브러리 tooconnect tooand 인터페이스는 Analysis Services 서버와 필요 합니다. SSMS, SSDT, Excel 2016 및 Power BI에 대 한 hello 최신 클라이언트 라이브러리 설치 되거나 월별 릴리스에로 업데이트 합니다. 그러나 일부 경우에는 응용 프로그램 hello 최신 버전으로 가질 수 있습니다. 예를 들어 정책 지연 시간을 업데이트 한 경우, 또는 Office 365 업데이트 hello 지연 된 채널에 있습니다.

## <a name="server-name"></a>서버 이름

Azure에서 Analysis Services 서버를 만들면 여기서 hello 서버는 만든 toobe 고유 이름과 hello 지역을 지정 합니다. Hello 서버 이름에 대 한 연결을 지정할 때 hello 서버 이름 지정 체계를:

```
<protocol>://<region>/<servername>
```
 프로토콜은 문자열 **asazure**, 영역은 hello hello 서버 생성 된 위치 Uri입니다 (예를 들어 westus.asazure.windows.net) servername hello 지역 내에서 고유 서버 hello 이름입니다.

### <a name="get-hello-server-name"></a>Hello 서버 이름 가져오기
**Azure 포털** > 서버 > **개요** > **서버 이름**, hello 전체 서버 이름 복사. 조직의 다른 사용자가 연결 하는 경우 toothis 서버 너무,이 서버 이름은 사람과 공유할 수 있습니다. 서버 이름을 지정할 때 hello 전체 경로 사용 합니다.

![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>연결 문자열

TooAzure 연결할 때 사용 하 여 Analysis Services 테이블 형식 개체 모델에서 다음 연결 문자열 형식을 사용 하 여 hello hello:

###### <a name="integrated-azure-active-directory-authentication"></a>통합 Azure Active Directory 인증
통합된 인증에 사용할 수 있는 경우 Azure Active Directory 자격 증명 캐시 hello를 선택 합니다. 파일이 없으면 hello Azure 로그인 창을 표시 합니다.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>사용자 이름 및 암호를 포함한 Azure Active Directory 인증

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Windows 인증(통합 보안)
Hello 현재 프로세스를 실행 하는 hello Windows 계정을 사용 합니다.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>.odc 파일을 사용하여 연결
이전 버전의 Excel 사용자는 Office 데이터 연결 (.odc) 파일을 사용 하 여 tooan Azure Analysis Services 서버를 연결할 수 있습니다. toolearn 더 참조 [Office 데이터 연결 (.odc) 파일을 만들](analysis-services-odc.md)합니다.


## <a name="next-steps"></a>다음 단계
[Excel로 연결](analysis-services-connect-excel.md)    
[Power BI로 연결](analysis-services-connect-pbi.md)   
[서버 관리](analysis-services-manage.md)   

