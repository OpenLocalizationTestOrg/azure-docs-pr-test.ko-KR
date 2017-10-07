---
title: "aaaCreate BizTalk 서비스의 백업을 복원 | Microsoft Docs"
description: "BizTalk 서비스에는 백업 및 복원이 포함되어 있습니다. 자세한 내용은 방법 toocreate 백업을 복원 하 고 백업 대상 결정 합니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>BizTalk 서비스: 백업 및 복원

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk 서비스에는 백업 및 복원 기능이 포함되어 있습니다. 이 항목에서는 toobackup 및 복원 BizTalk 서비스를 사용 하 여 Azure 클래식 포털을 hello 하는 방법을 설명 합니다.

Hello를 사용 하 여 BizTalk 서비스를 백업할 수도 있습니다 [BizTalk 서비스 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584)합니다. 

> [!NOTE]
> 하이브리드 연결 hello 버전에 관계 없이, 백업 하지 않습니다. 하이브리드 연결을 다시 만들어야 합니다.


## <a name="before-you-begin"></a>시작하기 전에
* 일부 버전에서는 백업 및 복원을 사용하지 못할 수도 있습니다. [BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md)를 참조하세요.
* Hello Azure 클래식 포털을 사용 하는 요청 시 백업을 만들려면 하거나 예약 된 백업을 만들 수 있습니다. 
* 콘텐츠 백업 BizTalk 서비스가 동일한 서버 인스턴스나 tooa 복원된 toohello 수 새 BizTalk 서비스입니다. toorestore hello 이름이 같은 기존 BizTalk 서비스는 hello를 삭제 해야 하는 hello를 사용 하 여 BizTalk 서비스 하 고 hello 이름을 사용할 수 있어야 합니다. BizTalk 서비스를 삭제 한 후 동일한 hello에 대 한 원하는 보다 더 긴 시간이 걸릴 수 있습니다 사용할 수 있는 이름 toobe 합니다. Hello 기다릴 수 없는 경우 동일한 이름을 toobe를 사용할 수 있는 지정한 다음 tooa 복원 새 BizTalk 서비스입니다.
* BizTalk Services 복원된 toohello 수 언어 버전과 동일한 버전 또는 더 높은 버전입니다. BizTalk 서비스 tooa 복원 hello 백업을 수행한 경우에서 낮은 버전에서는 지원 되지 않습니다.
  
    예를 들어 Basic Edition 수 hello를 사용 하 여 백업을 복원할 toohello Premium Edition. Premium 버전 수 없습니다 hello를 사용 하 여 백업을 복원할 toohello Standard Edition.
* hello 컨트롤 번호의 toomaintain 연속성 hello EDI 제어 번호는 백업 됩니다. Hello 마지막 백업 이후 메시지를 처리 하는 경우이 백업 콘텐츠를 복원 중복 컨트롤 번호를 발생할 수 있습니다.
* 일괄 처리의 활성 메시지에 있는 경우 hello 일괄 처리 **전에** 백업을 실행 합니다. 필요에 따라 백업을 만들거나 예약된 백업을 만들 때 배치의 메시지는 저장되지 않습니다. 
  
    **일괄 처리의 활성 메시지가 있는 상태에서 백업하면 이러한 메시지는 백업되지 않으므로 손실됩니다.**
* 선택 사항: hello BizTalk 서비스 포털에서에서 모든 관리 작업이 중지.

## <a name="create-a-backup"></a>백업 만들기
언제든 백업을 만들어 완벽하게 제어할 수 있습니다. 이 섹션에서는 Azure 클래식 hello를 사용 하 여 hello 단계 toocreate 백업을 포함 하 여 포털:

[주문형 백업](#backupnow)

[백업 예약](#backupschedule)

#### <a name="backupnow"></a>주문형 백업
1. Hello Azure 클래식 포털에서에서 선택 **BizTalk 서비스**을 다음 선택 hello toobackup BizTalk 서비스 하 고 있습니다.
2. Hello에 **대시보드** 탭에서 **백업** hello hello 페이지 맨 아래에 있습니다.
3. 백업 이름을 입력합니다. 예를 들어 *myBizTalkService*BU*날짜*를 입력합니다.
4. Blob 저장소 계정 및 선택 hello 확인 표시 toostart hello 백업을 선택 합니다.

Hello 백업이 완료 되 면 hello 저장소 계정에는 컨테이너를 입력 하는 hello 백업 이름으로 만들어집니다. 이 컨테이너에는 BizTalk 서비스 백업 구성이 포함됩니다.

#### <a name="backupschedule"></a>백업 예약
1. Hello Azure 클래식 포털에서에서 선택 **BizTalk 서비스**, 선택 hello tooschedule hello 백업 하 고 hello를 선택 하면 BizTalk 서비스 이름을 **구성** 탭 합니다.
2. 집합 hello **백업 상태** 너무**자동**합니다. 
3. 선택 hello **저장소 계정** toostore 백업 hello, hello 입력 **주파수** 백업과 기간 tookeep hello 백업을 toocreate hello (**보존 일**):
   
    ![][AutomaticBU]
   
    **참고 사항**     
   
   * **보존 일**, hello 보존 기간 hello 백업 빈도 보다 커야 합니다.
   * 선택 **항상 하나 이상의 백업 유지**hello 보존 기간이 경과 되는 경우에 합니다.
4. **저장**을 선택합니다.

예약 된 백업 작업이 실행 될 때 입력 한 hello 저장소 계정에서 컨테이너 (toostore 백업 데이터)를 만듭니다. hello hello 컨테이너의 이름이 *BizTalk 서비스 이름-날짜-시간*합니다. 

표시 되는 hello BizTalk 서비스 대시보드는 **실패** 상태:

![마지막으로 예약된 백업 상태][BackupStatus] 

hello 링크 hello toohelp 문제를 해결 하는 관리 서비스 작업 로그를 엽니다. [BizTalk 서비스: 작업 로그를 사용하여 문제 해결](http://go.microsoft.com/fwlink/p/?LinkId=391211)을 참조하세요.

## <a name="restore"></a>복원
Hello 또는 hello Azure 클래식 포털에서에서 백업을 복원할 수 있습니다 [BizTalk 서비스 REST API 복원](http://go.microsoft.com/fwlink/p/?LinkID=325582)합니다. 이 섹션에는 hello 단계 toorestore hello 클래식 포털을 사용 하 여 나열 합니다.

#### <a name="before-restoring-a-backup"></a>복원하기 전에
* BizTalk 서비스를 복원하는 동안 새로운 추적, 보관 및 모니터링 저장소를 입력할 수 있습니다.
* 동일한 EDI 런타임 데이터를 복원 하는 번호입니다. hello EDI 런타임 백업 hello 제어 번호를 저장합니다. 복원 하는 hello 제어 번호는 hello hello 백업 시간에서 시퀀스의입니다. Hello 마지막 백업 이후 메시지를 처리 하는 경우이 백업 콘텐츠를 복원 중복 컨트롤 번호를 발생할 수 있습니다.

#### <a name="restore-a-backup"></a>백업 복원
1. Hello Azure 클래식 포털에서에서 선택 **새로** > **응용 프로그램 서비스** > **BizTalk 서비스** > **복원** :
   
    ![백업 복원][Restore]
2. **백업 URL**, hello 폴더 아이콘을 선택 하 고 저장소 hello 구성 백업 BizTalk 서비스는 hello Azure 저장소 계정을 확장 합니다. Hello 컨테이너를 확장 하 고 hello 오른쪽 창에서.txt 파일을 백업에 해당 하는 hello를 선택 합니다. 
   <br/><br/>
   **열기**를 선택합니다.
3. Hello에 **복원 BizTalk 서비스** 페이지에서 입력 한 **BizTalk 서비스 이름** hello 확인 **도메인 URL**, **Edition**, 및 **지역** hello 복원 BizTalk 서비스에 대 한 합니다. **새 SQL 데이터베이스 인스턴스를 만들어** hello 추적 데이터베이스에 대 한:
   
    ![][RestoreBizTalkService]
   
    Hello 다음 화살표를 선택 합니다.
4. Hello SQL 데이터베이스의 hello 이름이 유효한 지 확인 하 고 해당 서버에 대 한 hello SQL 데이터베이스를 만들 위치를 hello 물리적 서버 및 사용자 이름/암호를 입력 합니다.

    Tooconfigure hello SQL 데이터베이스 버전, 크기 및 기타 속성을 하려는 경우 선택 **고급 데이터베이스 설정 구성**합니다. 

    Hello 다음 화살표를 선택 합니다.

1. 새 저장소 계정을 만들거나 hello BizTalk 서비스에 대 한 기존 저장소 계정을 입력 합니다.
2. Hello, toostart hello 복원 확인 표시를 선택 합니다.

Hello 복원을 성공적으로 완료 되 면 새 BizTalk 서비스는 hello BizTalk 서비스 페이지 hello Azure 클래식 포털에서에서 일시 중단된 된 상태에 나열 됩니다.

### <a name="postrestore"></a>백업을 복원한 후
hello BizTalk 서비스는 항상 복원는 **Suspended** 상태입니다. 이 상태에서는 hello 새 환경 기능을 포함 하는 전에 구성 변경 내용을 작업을 수행할 수 있습니다.

* Hello Azure BizTalk 서비스 SDK를 사용 하 여 BizTalk 서비스 응용 프로그램을 만든 경우 해당 응용 프로그램 toowork hello 복원 환경에 tootooupdate hello ACS (액세스 제어) 자격 증명을 할 수 있습니다.
* BizTalk 서비스 tooreplicate 기존 BizTalk 서비스 환경에 복원합니다. FTP 소스 폴더를 사용 하는 계약 hello 원래 BizTalk 서비스 포털에 구성 된 경우이 상황에서 새로 복원 hello 환경 toouse 다른 소스 FTP 폴더의에서 tooupdate hello 계약을 할 수 있습니다. 그렇지 않으면 있을 수 있습니다 toopull 시도 하는 두 개의 서로 다른 계약 hello 동일한 메시지입니다.
* 여러 BizTalk 서비스 환경 toohave 복원한 경우 hello Visual Studio 응용 프로그램, PowerShell cmdlet, REST Api 또는 거래 업체 관리 OM Api에서 올바른 환경 hello 대상 하는지 확인 합니다.
* 새로 복원한 hello BizTalk 서비스 환경에는 것이 좋습니다 tooconfigure 자동화 된 백업 이며

BizTalk 서비스와 선택 hello Azure 클래식 포털 선택 hello에에서 대 한 BizTalk 서비스 toostart hello 복원 **Resume** hello 작업 표시줄에서 합니다. 

## <a name="what-gets-backed-up"></a>백업 대상
백업을 만들 때 hello 다음과 같은 항목이 백업 됩니다.

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>백업되는 항목</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Azure BizTalk Services 포털</strong></td>
</tr> 
<tr>
<td>구성 및 런타임</td> 
<td>
<ul>
<li>파트너 및 프로필 세부 정보</li>
<li>파트너 계약</li>
<li>배포된 사용자 지정 어셈블리</li>
<li>배포된 브리지</li>
<li>인증서</li>
<li>배포된 변환</li>
<li>파이프라인</li>
<li>Hello BizTalk 서비스 포털에서에서 만들고 저장 하는 서식 파일</li>
<li>X12 ST01 및 GS01 매핑</li>
<li>제어 번호(EDI)</li>
<li>AS2 메시지 MIC 값</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Azure BizTalk 서비스</strong></td>
</tr> 
<tr>
<td>SSL 인증서</td> 
<td>
<ul>
<li>SSL 인증서 데이터</li>
<li>SSL 인증서 암호</li>
</ul>
</td>
</tr> 
<tr>
<td>BizTalk 서비스 설정</td> 
<td>
<ul>
<li>배율 단위 수</li>
<li>버전</li>
<li>제품 버전</li>
<li>지역/데이터 센터</li>
<li>ACS(액세스 제어 서비스) 네임스페이스 및 키</li>
<li>추적 데이터베이스 연결 문자열</li>
<li>보관 저장소 계정 연결 문자열</li>
<li>모니터링 저장소 계정 연결 문자열</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>추가 항목</strong></td>
</tr> 
<tr>
<td>추적 데이터베이스</td> 
<td>Hello BizTalk 서비스를 만들면 hello Azure SQL 데이터베이스 서버 및 hello 추적 데이터베이스 이름을 포함 하 여 hello 추적 데이터베이스 세부 정보 입력 됩니다. hello 추적 데이터베이스를 자동으로 백업 하지 됩니다.
<br/><br/>
<strong>중요</strong><br/>
Hello 추적 데이터베이스 삭제 되 고 복구 데이터베이스 요구를 hello, 이전 백업 존재 해야 합니다. 백업이 없는 경우 hello 추적 데이터베이스 및 해당 데이터는 복구할 수 없습니다. 이 경우 새 추적 데이터베이스를 만들 hello로 동일한 데이터베이스 이름입니다. 지역에서 복제가 권장됩니다.</td>
</tr> 
</table>

## <a name="next"></a>다음
toocreate Azure BizTalk 서비스에서 Azure 클래식 포털, go를 너무 hello[BizTalk 서비스: 프로 비전 사용 하 여 Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=302280)합니다. 응용 프로그램을 이동 너무 만들 toostart[Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=235197)합니다.

## <a name="see-also"></a>참고 항목
* [BizTalk 서비스 백업](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [백업에서 BizTalk 서비스 복원](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk 서비스: 프로비저닝 상태 차트](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk 서비스: 제한](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk 서비스: 발급자 이름 및 발급자 키](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

