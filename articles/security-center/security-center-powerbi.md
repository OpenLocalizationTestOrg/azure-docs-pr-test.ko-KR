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
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a><span data-ttu-id="4be2d-103">Power BI로 Azure 보안 센터 데이터에서 통찰력 얻기</span><span class="sxs-lookup"><span data-stu-id="4be2d-103">Get insights from Azure Security Center data with Power BI</span></span>
<span data-ttu-id="4be2d-104">hello [Power BI 대시보드에](http://aka.ms/azure-security-center-power-bi) Azure 보안 센터를 통해 toovisualize 있습니다, 분석 및 권장 사항 및 모바일 장치를 포함 하 여 어디에서 보안 경고를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-104">hello [Power BI Dashboard](http://aka.ms/azure-security-center-power-bi) for Azure Security Center enables you toovisualize, analyze, and filter recommendations and security alerts from anywhere, including your mobile device.</span></span> <span data-ttu-id="4be2d-105">Power BI 대시보드 tooreveal 추세 hello를 사용 하 여 패턴-리소스 또는 원본 IP 주소에서 보안 경고 보기 및 리소스 또는 연령별 채로 보안 위험을 공격 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-105">Use hello Power BI dashboard tooreveal trends and attack patterns - view security alerts by resource or source IP address and unaddressed security risks by resource or age.</span></span>

<span data-ttu-id="4be2d-106">또한 [Azure 감사 로그](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) 및 [Azure SQL 데이터베이스 감사](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)의 데이터를 사용하는 등의 원하는 방식으로 다른 데이터와 보안 센터 권장 사항과 보안 경고를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-106">You can also mash up Security Center recommendations and security alerts with other data in interesting ways, for example using data from [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) and [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span></span> <span data-ttu-id="4be2d-107">Power BI 대시보드를 제공 하는 둘 다 하 고 쉽게 보고 클라우드 리소스의 hello 보안 상태에 대해이 데이터 tooExcel 내보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-107">Both offer Power BI Dashboards, and you can also export this data tooExcel for easy reporting on hello security state of your cloud resources.</span></span>

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a><span data-ttu-id="4be2d-108">Azure 보안 센터 대시보드 tooaccess Power BI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4be2d-108">Using Azure Security Center dashboard tooaccess Power BI</span></span>
<span data-ttu-id="4be2d-109">Hello Azure 보안 센터 대시보드 tooaccess Power BI 보고서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-109">You can also use hello Azure Security Center dashboard tooaccess Power BI reports.</span></span> <span data-ttu-id="4be2d-110">Hello 단계 tooperform이이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-110">Follow hello steps tooperform this task:</span></span>

1. <span data-ttu-id="4be2d-111">Hello에 **Azure 보안 센터** 대시보드를 클릭 하 여 **Power BI** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-111">In hello **Azure Security Center** dashboard, click **Power BI** button.</span></span>

    ![Power BI를 사용 하 여 tooAzure 보안 센터를 연결 합니다.](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. <span data-ttu-id="4be2d-113">hello **Power BI** hello 다음 화면에에서 표시 된 대로 hello 오른쪽에 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-113">hello **Power BI** blade opens on hello right side as shown in hello following screen:</span></span>

    ![Power BI를 사용 하 여 tooAzure 보안 센터를 연결 합니다.](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. <span data-ttu-id="4be2d-115">Hello에 대 한 hello Power BI 대시보드 처음을 만들 수 있습니다 hello 다음 옵션 중 하나에 hello **Power BI의 탐색** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="4be2d-115">If you are creating hello Power BI dashboard for hello first time, you can choose one of hello following options in hello **Explore in Power BI** blade:</span></span>

   * <span data-ttu-id="4be2d-116">**보안 insights 대시보드**: toocreate 보안 상태, 스레드 및 검색을 포함 하는 대시보드를 원하는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-116">**Security insights dashboard**: choose this option if you want toocreate a dashboard that includes security status, threads, and detections.</span></span> <span data-ttu-id="4be2d-117">이 옵션은 구독의 보호 상태 및 감지된 경고를 분석하는 일을 담당하는 DevOps 역할에 보다 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-117">This option is a more common for DevOps role that is responsible for analyzing their protection status and detected alerts across subscriptions.</span></span>
   * <span data-ttu-id="4be2d-118">**정책 관리 대시보드**: tooexplore 관리 및 적용 정책을 하려는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-118">**Policy management dashboard**: choose this option if you want tooexplore management and enforcement policy.</span></span>  <span data-ttu-id="4be2d-119">이 옵션은 관리에 중점을 둔 Central IT에 보다 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-119">This option is a more common for Central IT who are more focused on governance.</span></span> <span data-ttu-id="4be2d-120">조직 내에서 보안 정책 준수 여부에이 대시보드 toogain 표시 유형 및 통찰력을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-120">They can use this dashboard toogain visibility and insights on security policy adherence across their organization.</span></span>
   * <span data-ttu-id="4be2d-121">Power BI 대시보드를 이미 있는 경우 클릭 **Go tooyour 현재 Power BI 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-121">If you already have a Power BI dashboard, click **Go tooyour current Power BI dashboard**.</span></span>
4. <span data-ttu-id="4be2d-122">이 예에서는 **보안 insights 대시보드** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-122">For this example, click **Security insights dashboard** option.</span></span> <span data-ttu-id="4be2d-123">처음으로 hello 이것이 tooinstall hello 콘텐츠 팩을 메시지가 표시 되는 보안 센터에 대 한 Power BI 대시보드를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-123">If this is hello first time, you are creating a Power BI dashboard for Security Center you are prompted tooinstall hello content pack.</span></span> <span data-ttu-id="4be2d-124">클릭 **가져오기** hello 단추 **Power BI 용 콘텐츠 팩** hello 화면에 다음 그림과 같이 창:</span><span class="sxs-lookup"><span data-stu-id="4be2d-124">Click **Get** button in hello **Content packs for Power BI** window as shown in hello following screen:</span></span>

    ![Azure 보안 센터 보안 Insights 대시보드](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. <span data-ttu-id="4be2d-126">hello **tooAzure 보안 센터 보안 통찰력 연결** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-126">hello **Connect tooAzure Security Center Security Insights** window appear.</span></span> <span data-ttu-id="4be2d-127">있는지 hello 확인 **인증** 메서드는 **oAuth2** 아래와 같이 클릭 **로그인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-127">Make sure hello **Authentication** method is **oAuth2** as shown below and click **Sign in** button.</span></span>

    ![인증](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. <span data-ttu-id="4be2d-129">묻습니다 tooauthenticate 다시 Azure 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-129">You may be asked tooauthenticate again with your Azure credentials.</span></span> <span data-ttu-id="4be2d-130">인증 후 대시보드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-130">After authenticating your dashboard will be created.</span></span> <span data-ttu-id="4be2d-131">Hello 대시보드 만들어지면 hello 화면에 다음 그림과 같이 hello 유사한 구조를 사용 하 여 보고서 참조:</span><span class="sxs-lookup"><span data-stu-id="4be2d-131">Once hello dashboard is created you see a report with hello similar structure as shown in hello following screen:</span></span>

    ![Power BI 대시보드](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> <span data-ttu-id="4be2d-133">Hello 보고서의 새로 고침에는 매일 예약 된 tootake 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-133">A refresh of hello report is scheduled tootake place on a daily basis.</span></span> <span data-ttu-id="4be2d-134">이 새로 고침에 장애가 발생 하는 경우 읽기 [hello Azure 보안 센터 Power BI로 잠재적인 새로 고침 문제](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), 방법에 대 한 자세한 내용은 tootroubleshoot 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-134">In case you experience a failure on this refresh, read [Potential Refresh Issues with hello Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), for more information on how tootroubleshoot.</span></span>
>
>

<span data-ttu-id="4be2d-135">여기서 보안 알림 및 권장 사항, hello 번호는 물론 hello 수가 Vm, Azure SQL 데이터베이스 및 Azure 보안 센터에서 모니터링 되는 네트워크 리소스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-135">Here you can see hello number of security alerts and recommendations, as well as hello number of VMs, Azure SQL databases, and network resources being monitored by Azure Security Center.</span></span>

<span data-ttu-id="4be2d-136">링크 tooAzure 보안 센터 toohello를 Azure 포털을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-136">A link tooAzure Security Center redirects you toohello Azure portal.</span></span> <span data-ttu-id="4be2d-137">hello 차트 만들 보안 권장 사항 및 경고를 포함 하는 방법에 대 한 쉬운 toovisualize 정보.</span><span class="sxs-lookup"><span data-stu-id="4be2d-137">hello charts make it easy toovisualize information about security recommendations and alerts, including:</span></span>

* <span data-ttu-id="4be2d-138">리소스 보안 상태</span><span class="sxs-lookup"><span data-stu-id="4be2d-138">Resource Security State</span></span>
* <span data-ttu-id="4be2d-139">보류 중인 권장 사항</span><span class="sxs-lookup"><span data-stu-id="4be2d-139">Pending Recommendations</span></span>
* <span data-ttu-id="4be2d-140">VM 권장 사항</span><span class="sxs-lookup"><span data-stu-id="4be2d-140">VM Recommendations</span></span>
* <span data-ttu-id="4be2d-141">시간에 따른 경고</span><span class="sxs-lookup"><span data-stu-id="4be2d-141">Alerts over Time</span></span>
* <span data-ttu-id="4be2d-142">공격 받은 리소스</span><span class="sxs-lookup"><span data-stu-id="4be2d-142">Attacked Resources</span></span>
* <span data-ttu-id="4be2d-143">공격 받은 IP</span><span class="sxs-lookup"><span data-stu-id="4be2d-143">Attacked IPs</span></span>

<span data-ttu-id="4be2d-144">각 차트 뒤에 자세한 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-144">Behind each chart, there are additional insights.</span></span> <span data-ttu-id="4be2d-145">타일 toosee 자세한 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-145">Select a tile toosee more information.</span></span> <span data-ttu-id="4be2d-146">예를 들어 hello **리소스 보안 상태** 타일에 표시 추가 세부 정보에 대 한 권장 사항 보류 중인 리소스에 의해 hello 다음 화면에에서 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="4be2d-146">For example, hello **Resource Security State** tile shows you additional details about pending recommendations by resources as shown in hello following screen:</span></span>

![권장 사항](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

<span data-ttu-id="4be2d-148">이 그래프의 줄을 클릭 하는 경우 hello 다른 것 아웃 toogray도 및 집중도 하면 선택한 hello에 대해서만입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-148">If you click on any line of this graph, hello others are going toogray out and you focus only on hello one you selected.</span></span> <span data-ttu-id="4be2d-149">tooreturn toohello 대시보드 클릭 **Azure 보안 센터** hello에서 **대시보드** hello 왼쪽된 창에서이 페이지의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-149">tooreturn toohello dashboard, click **Azure Security Center** under hello **Dashboards** option on hello left pane of this page.</span></span>

> [!NOTE]
> <span data-ttu-id="4be2d-150">Toocustomize 원하는 경우 보고서를 추가 필드를 추가 하거나 기존 시각적 개체를 변경 하 여 hello 보고서를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-150">If you’d like toocustomize your reports by adding additional fields or changing existing visuals, you can edit hello report.</span></span> <span data-ttu-id="4be2d-151">자세한 내용은 [Power BI의 편집용 보기에서 보고서와 상호 작용](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) 을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-151">Read [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) for more information.</span></span>
>
>

<span data-ttu-id="4be2d-152">hello **시간과 리소스가 공격을 통한 경고** 및 **공격자가 Ip** 각 중에서 클릭할 때 타일 hello 유사한 출력을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-152">hello **Alerts over Time, Attacked Resources** and **Attacker IPs** tiles will have hello similar output when you click on each one of it.</span></span> <span data-ttu-id="4be2d-153">이러한 세 개의 변수 모두에 대 한 정보를 집계 하 고 호출 하는 hello 보고서 때문에 이런 **공격을 받고 리소스** hello 다음 화면에에서 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="4be2d-153">This happens because hello report aggregates information regarding all those three variables and calls it **Resources under Attack** as shown in hello following screen:</span></span>

![공격받는 리소스](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

<span data-ttu-id="4be2d-155">이 시점에서이 보고서의 복사본을 저장, 인쇄 하거나 수도 hello에 사용할 수 있는 hello 옵션을 사용 하 여 hello 웹에 게시할 **파일** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="4be2d-155">At this point you can also save a copy of this report, print it or publish it on hello web by using hello options available in hello **File** menu.</span></span>

![파일 메뉴](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a><span data-ttu-id="4be2d-157">Power BI로 Azure 보안 센터 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="4be2d-157">Exploring your Azure Security Center data with Power BI services</span></span>
<span data-ttu-id="4be2d-158">Toohello 연결 [Power BI 콘텐츠 팩 서비스](https://msit.powerbi.com/groups/me/getdata/services) Power BI에서 단계를 수행 하는 hello 실행:</span><span class="sxs-lookup"><span data-stu-id="4be2d-158">Connect toohello [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) in Power BI and execute hello following steps:</span></span>

1. <span data-ttu-id="4be2d-159">Hello에 **Power BI 용 콘텐츠 팩** 창 아래와 같이 두 가지 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-159">In hello **Content Pack for Power BI** window you will see two options as shown below.</span></span>

    ![Power BI용 콘텐츠 팩](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > <span data-ttu-id="4be2d-161">이 문서의 첫 번째 부분 hello를 이미 실행 된 경우 Azure 보안 센터 정책 관리는 옵션 하나만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-161">If already executed hello first part of this article you will see only one option, which is Azure Security Center Policy Management.</span></span>
   >
   >
2. <span data-ttu-id="4be2d-162">이 예의 hello 용도로 클릭 **가져오기** hello에 **Azure 보안 센터 정책 관리** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-162">For hello purpose of this example, click **Get** in hello **Azure Security Center Policy Management** tile.</span></span>
3. <span data-ttu-id="4be2d-163">Hello에 **tooAzure 보안 센터 정책 관리 연결** 창, 확인 되었는지 tooselect **oAuth2** 아래 **인증 방법을** 아래와 같이 아래로 삭제 하 고 클릭 **로그인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-163">In hello **Connect tooAzure Security Center Policy Management** window, make sure tooselect **oAuth2** under **Authentication Method** drop down as shown below and click **Sign in** button.</span></span>

    ![정책 관리 창](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. <span data-ttu-id="4be2d-165">리디렉션된 tooan 인증 페이지 tooconnect tooAzure 보안 센터를 사용 하는 hello 자격 증명을 입력 해야 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-165">You will be redirected tooan authentication page where you should type hello credentials that you are using tooconnect tooAzure Security Center.</span></span> <span data-ttu-id="4be2d-166">Hello 인증 프로세스가 완료 되 면 Power BI는 가져오기를 시작 데이터 toobuild 보고서.</span><span class="sxs-lookup"><span data-stu-id="4be2d-166">After hello authentication process is complete, Power BI will start importing data toobuild your reports.</span></span> <span data-ttu-id="4be2d-167">이 시간 동안 hello hello 브라우저의 오른쪽 아래에 메시지의 뒤에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-167">During this time you may see hello following message on hello right corner of your browser:</span></span>

    ![Power BI를 사용 하 여 tooAzure 보안 센터를 연결 합니다.](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > <span data-ttu-id="4be2d-169">hello 대시보드가 생성 될 때 hello에 대 한 처음으로 여러 구독이 있는 경우 시나리오에 주로 평소 보다 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-169">when hello dashboard is being created for hello first time it can take longer than usual, mainly for scenarios where you have multiple subscriptions.</span></span>
   >
   >
5. <span data-ttu-id="4be2d-170">Azure 보안 센터 Power BI 대시보드에 hello로 로드 됩니다 hello 프로세스가 완료 되 면 **정책 관리** 아래와 유사한 toohello 보고:</span><span class="sxs-lookup"><span data-stu-id="4be2d-170">Once hello process is finished, your Azure Security Center Power BI dashboard will load with hello **Policy Management** report similar toohello one shown below:</span></span>

    ![정책 관리 대시보드](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a><span data-ttu-id="4be2d-172">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4be2d-172">See also</span></span>
<span data-ttu-id="4be2d-173">이 문서에서는 방법에 대해 배웠습니다 toouse Power BI Azure 보안 센터에서.</span><span class="sxs-lookup"><span data-stu-id="4be2d-173">In this document, you learned how toouse Power BI in Azure Security Center.</span></span> <span data-ttu-id="4be2d-174">Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-174">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="4be2d-175">[Azure 보안 센터 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) -학습 방법을 tooplan Azure 보안 센터를 채택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-175">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how tooplan Azure Security Center adoption.</span></span>
* <span data-ttu-id="4be2d-176">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 보안 센터의 tooconfigure 보안 설정</span><span class="sxs-lookup"><span data-stu-id="4be2d-176">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security settings in Azure Security Center</span></span>
* <span data-ttu-id="4be2d-177">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고</span><span class="sxs-lookup"><span data-stu-id="4be2d-177">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts</span></span>
* <span data-ttu-id="4be2d-178">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="4be2d-178">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service</span></span>
* <span data-ttu-id="4be2d-179">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) — Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4be2d-179">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>
