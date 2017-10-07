---
title: "Power BI를 사용 하 여 Azure 보안 센터 데이터 로부터 이해를 aaaGet | Microsoft Docs"
description: "Azure 보안 센터 Power BI 콘텐츠 팩 hello 권장 사항을 쉽게 toofind 보안 경고를 사용 하면, 리소스 공격 및 추세를 보여 줍니다, 그리고 보고를 위해 생성 된 데이터 집합에 따라."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Power BI로 Azure 보안 센터 데이터에서 통찰력 얻기
hello [Power BI 대시보드에](http://aka.ms/azure-security-center-power-bi) Azure 보안 센터를 통해 toovisualize 있습니다, 분석 및 권장 사항 및 모바일 장치를 포함 하 여 어디에서 보안 경고를 필터링 합니다. Power BI 대시보드 tooreveal 추세 hello를 사용 하 여 패턴-리소스 또는 원본 IP 주소에서 보안 경고 보기 및 리소스 또는 연령별 채로 보안 위험을 공격 하는 합니다.

또한 [Azure 감사 로그](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) 및 [Azure SQL 데이터베이스 감사](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)의 데이터를 사용하는 등의 원하는 방식으로 다른 데이터와 보안 센터 권장 사항과 보안 경고를 함께 사용할 수 있습니다. Power BI 대시보드를 제공 하는 둘 다 하 고 쉽게 보고 클라우드 리소스의 hello 보안 상태에 대해이 데이터 tooExcel 내보낼 수도 있습니다.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Azure 보안 센터 대시보드 tooaccess Power BI를 사용 하 여
Hello Azure 보안 센터 대시보드 tooaccess Power BI 보고서를 사용할 수 있습니다. Hello 단계 tooperform이이 작업을 수행 합니다.

1. Hello에 **Azure 보안 센터** 대시보드를 클릭 하 여 **Power BI** 단추입니다.

    ![Power BI를 사용 하 여 tooAzure 보안 센터를 연결 합니다.](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. hello **Power BI** hello 다음 화면에에서 표시 된 대로 hello 오른쪽에 블레이드를 엽니다.

    ![Power BI를 사용 하 여 tooAzure 보안 센터를 연결 합니다.](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Hello에 대 한 hello Power BI 대시보드 처음을 만들 수 있습니다 hello 다음 옵션 중 하나에 hello **Power BI의 탐색** 블레이드:

   * **보안 insights 대시보드**: toocreate 보안 상태, 스레드 및 검색을 포함 하는 대시보드를 원하는 경우이 옵션을 선택 합니다. 이 옵션은 구독의 보호 상태 및 감지된 경고를 분석하는 일을 담당하는 DevOps 역할에 보다 일반적입니다.
   * **정책 관리 대시보드**: tooexplore 관리 및 적용 정책을 하려는 경우이 옵션을 선택 합니다.  이 옵션은 관리에 중점을 둔 Central IT에 보다 일반적입니다. 조직 내에서 보안 정책 준수 여부에이 대시보드 toogain 표시 유형 및 통찰력을 사용할 수 있습니다.
   * Power BI 대시보드를 이미 있는 경우 클릭 **Go tooyour 현재 Power BI 대시보드**합니다.
4. 이 예에서는 **보안 insights 대시보드** 옵션을 클릭합니다. 처음으로 hello 이것이 tooinstall hello 콘텐츠 팩을 메시지가 표시 되는 보안 센터에 대 한 Power BI 대시보드를 생성 됩니다. 클릭 **가져오기** hello 단추 **Power BI 용 콘텐츠 팩** hello 화면에 다음 그림과 같이 창:

    ![Azure 보안 센터 보안 Insights 대시보드](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. hello **tooAzure 보안 센터 보안 통찰력 연결** 창이 나타납니다. 있는지 hello 확인 **인증** 메서드는 **oAuth2** 아래와 같이 클릭 **로그인** 단추입니다.

    ![인증](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. 묻습니다 tooauthenticate 다시 Azure 자격 증명을 사용 합니다. 인증 후 대시보드가 생성됩니다. Hello 대시보드 만들어지면 hello 화면에 다음 그림과 같이 hello 유사한 구조를 사용 하 여 보고서 참조:

    ![Power BI 대시보드](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Hello 보고서의 새로 고침에는 매일 예약 된 tootake 위치입니다. 이 새로 고침에 장애가 발생 하는 경우 읽기 [hello Azure 보안 센터 Power BI로 잠재적인 새로 고침 문제](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), 방법에 대 한 자세한 내용은 tootroubleshoot 합니다.
>
>

여기서 보안 알림 및 권장 사항, hello 번호는 물론 hello 수가 Vm, Azure SQL 데이터베이스 및 Azure 보안 센터에서 모니터링 되는 네트워크 리소스를 확인할 수 있습니다.

링크 tooAzure 보안 센터 toohello를 Azure 포털을 리디렉션합니다. hello 차트 만들 보안 권장 사항 및 경고를 포함 하는 방법에 대 한 쉬운 toovisualize 정보.

* 리소스 보안 상태
* 보류 중인 권장 사항
* VM 권장 사항
* 시간에 따른 경고
* 공격 받은 리소스
* 공격 받은 IP

각 차트 뒤에 자세한 내용이 있습니다. 타일 toosee 자세한 정보를 선택 합니다. 예를 들어 hello **리소스 보안 상태** 타일에 표시 추가 세부 정보에 대 한 권장 사항 보류 중인 리소스에 의해 hello 다음 화면에에서 표시 된 대로:

![권장 사항](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

이 그래프의 줄을 클릭 하는 경우 hello 다른 것 아웃 toogray도 및 집중도 하면 선택한 hello에 대해서만입니다. tooreturn toohello 대시보드 클릭 **Azure 보안 센터** hello에서 **대시보드** hello 왼쪽된 창에서이 페이지의 옵션입니다.

> [!NOTE]
> Toocustomize 원하는 경우 보고서를 추가 필드를 추가 하거나 기존 시각적 개체를 변경 하 여 hello 보고서를 편집할 수 있습니다. 자세한 내용은 [Power BI의 편집용 보기에서 보고서와 상호 작용](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) 을 참고합니다.
>
>

hello **시간과 리소스가 공격을 통한 경고** 및 **공격자가 Ip** 각 중에서 클릭할 때 타일 hello 유사한 출력을 갖습니다. 이러한 세 개의 변수 모두에 대 한 정보를 집계 하 고 호출 하는 hello 보고서 때문에 이런 **공격을 받고 리소스** hello 다음 화면에에서 표시 된 대로:

![공격받는 리소스](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

이 시점에서이 보고서의 복사본을 저장, 인쇄 하거나 수도 hello에 사용할 수 있는 hello 옵션을 사용 하 여 hello 웹에 게시할 **파일** 메뉴.

![파일 메뉴](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Power BI로 Azure 보안 센터 데이터 탐색
Toohello 연결 [Power BI 콘텐츠 팩 서비스](https://msit.powerbi.com/groups/me/getdata/services) Power BI에서 단계를 수행 하는 hello 실행:

1. Hello에 **Power BI 용 콘텐츠 팩** 창 아래와 같이 두 가지 옵션이 표시 됩니다.

    ![Power BI용 콘텐츠 팩](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > 이 문서의 첫 번째 부분 hello를 이미 실행 된 경우 Azure 보안 센터 정책 관리는 옵션 하나만 표시 됩니다.
   >
   >
2. 이 예의 hello 용도로 클릭 **가져오기** hello에 **Azure 보안 센터 정책 관리** 바둑판식으로 배열입니다.
3. Hello에 **tooAzure 보안 센터 정책 관리 연결** 창, 확인 되었는지 tooselect **oAuth2** 아래 **인증 방법을** 아래와 같이 아래로 삭제 하 고 클릭 **로그인** 단추입니다.

    ![정책 관리 창](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. 리디렉션된 tooan 인증 페이지 tooconnect tooAzure 보안 센터를 사용 하는 hello 자격 증명을 입력 해야 하면 됩니다. Hello 인증 프로세스가 완료 되 면 Power BI는 가져오기를 시작 데이터 toobuild 보고서. 이 시간 동안 hello hello 브라우저의 오른쪽 아래에 메시지의 뒤에 나타날 수 있습니다.

    ![Power BI를 사용 하 여 tooAzure 보안 센터를 연결 합니다.](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > hello 대시보드가 생성 될 때 hello에 대 한 처음으로 여러 구독이 있는 경우 시나리오에 주로 평소 보다 시간이 오래 걸릴 수 있습니다.
   >
   >
5. Azure 보안 센터 Power BI 대시보드에 hello로 로드 됩니다 hello 프로세스가 완료 되 면 **정책 관리** 아래와 유사한 toohello 보고:

    ![정책 관리 대시보드](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 toouse Power BI Azure 보안 센터에서. Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) -학습 방법을 tooplan Azure 보안 센터를 채택 합니다.
* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 보안 센터의 tooconfigure 보안 설정
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) — Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
