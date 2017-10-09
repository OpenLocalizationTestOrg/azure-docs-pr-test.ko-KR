---
title: "MyDriving Azure IoT 예제: 빠른 시작 | Microsoft Docs"
description: "이 방법의 포괄적인 데모 응용 프로그램 시작 tooarchitect 스트림 분석, 기계 학습 및 이벤트 허브를 포함 하 여 Microsoft Azure를 사용 하 여 프로그램 IoT 시스템."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="1f607-103">MyDriving IoT 시스템: 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="1f607-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="1f607-104">MyDriving는 hello 디자인 및 구현 일반적인을 보여 주는 시스템 [사물 인터넷](iot-suite-overview.md) (IoT) 솔루션 장치에서 원격 분석을 수집 하는 hello 클라우드에서 해당 데이터를 처리 및 기계 학습 적용 됩니다. tooprovide 선택 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="1f607-105">hello 데모 य ल फ와 자동차의 제어 시스템에서 정보를 수집 하는 어댑터에서 데이터를 사용 하 여 자동차 줄어들며에 대 한 데이터를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="1f607-106">이 데이터 tooprovide 피드백 비교 tooother 사용자에서 구동 스타일에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="1f607-107">hello 실제 MyDriving의 목적은 사용자 고유의 IoT 솔루션을 만드는 시작 tooget입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="1f607-108">하지만 그 이전에 액세스할 수 있습니다 hello MyDriving 응용 프로그램 자체가-테스트 사용자 팀의 구성원으로 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="1f607-109">이렇게 하면 hello 앱 및 소비자를 근거 hello 시스템 경험 hello 아키텍처에 살펴보고 전에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="1f607-110">또한, tooHockeyApp, 앱 tootest 사용자의 hello 알파, 베타 분포를 관리 하는 쿨 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="1f607-111">Hello 모바일 환경을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1f607-111">Use hello mobile experience</span></span>
<span data-ttu-id="1f607-112">Android, iOS 또는 Windows 10 장치를 사용 하는 경우 hello MyDriving 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="1f607-113">Android 및 Windows 10 Mobile 설치</span><span class="sxs-lookup"><span data-stu-id="1f607-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="1f607-114">장치에서:</span><span class="sxs-lookup"><span data-stu-id="1f607-114">On your device:</span></span>

1. <span data-ttu-id="1f607-115">앱 개발을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="1f607-116">Android: **설정** > **보안**에서 **알 수 없는 원본**의 앱을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="1f607-117">Windows 10: **설정** > **업데이트** > **개발자용**에서 **개발자 모드**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="1f607-118">[HockeyApp](https://rink.hockeyapp.net)에 등록 또는 로그인하여 베타 테스트 팀에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="1f607-119">HockeyApp 앱 tootest 사용자의 초기 릴리스를 쉽게 toodistribute 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="1f607-120">Windows 10을 사용 하는 경우 hello Edge 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="1f607-121">빌드 2016 참석자 인 경우 इ न क hello 동일 hello Microsoft 단추 중 하나를 사용 하 여 hello 회의 대 한 등록 Microsoft 계정 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="1f607-122">HockeyApp에 이미 등록되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-122">You’re already signed up with HockeyApp.</span></span>
   
   ![HockeyApp 로그인 화면](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="1f607-124">다운로드 하 고 여기에서 hello 앱을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="1f607-125">Android</span><span class="sxs-lookup"><span data-stu-id="1f607-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="1f607-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="1f607-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="1f607-127">두 가지 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-127">There are two items.</span></span> <span data-ttu-id="1f607-128">Hello 인증서를 설치 **신뢰할 수 있는 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="1f607-129">Hello 앱을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-129">Then install hello app.</span></span>

<span data-ttu-id="1f607-130">*Windows 10 Mobile에 hello 앱을 시작 하는 문제?*</span><span class="sxs-lookup"><span data-stu-id="1f607-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="1f607-131">휴대폰이 업데이트되었거나 너무 오래되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="1f607-132">Hello 최신 업데이트를 완료 했습니다 하거나 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="1f607-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="1f607-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="1f607-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="1f607-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="1f607-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="1f607-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="1f607-136">iOS 설치</span><span class="sxs-lookup"><span data-stu-id="1f607-136">iOS installation</span></span>
<span data-ttu-id="1f607-137">빌드 2016 다닌 경우 HockeyApp에서 테스트 팀의 구성원으로 hello 앱을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="1f607-138">IOS 장치에서 로그인 너무[HockeyApp](https://rink.hockeyapp.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="1f607-139">Hello 회의에 등록 하는 동일한 Microsoft 계정 전자 메일을 hello hello Microsoft 로그인 단추 및 기호를 사용 하 여 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="1f607-140">(Hello 전자 메일 및 암호 필드를 사용 하지 마십시오.)</span><span class="sxs-lookup"><span data-stu-id="1f607-140">(Don’t use hello email and password fields.)</span></span>
   
   ![HockeyApp 로그인 화면](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="1f607-142">Hello HockeyApp 대시보드에 MyDriving를 선택 하 고 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="1f607-143">Hello 베타 릴리스를 HockeyApp에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="1f607-144">a.</span><span class="sxs-lookup"><span data-stu-id="1f607-144">a.</span></span> <span data-ttu-id="1f607-145">너무 이동**설정** > **일반** > **프로필 및 장치 관리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f607-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="1f607-146">b.</span><span class="sxs-lookup"><span data-stu-id="1f607-146">b.</span></span> <span data-ttu-id="1f607-147">Hello 신뢰 **비트 경기장 GmbH** 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="1f607-148">빌드 2016 참석 하지 않은 경우 있습니다를 빌드하고 배포 hello 앱 사용자가 직접:</span><span class="sxs-lookup"><span data-stu-id="1f607-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="1f607-149">Hello 코드 다운로드 [GitHub에서]합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="1f607-150">[Xamarin을 사용하여]빌드 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="1f607-151">Hello에 자세한 내용을 보려면 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="1f607-152">OBD 어댑터 가져오기(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="1f607-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="1f607-153">이 실제 사물 인터넷 시스템 수행 하는 hello 부분입니다!</span><span class="sxs-lookup"><span data-stu-id="1f607-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="1f607-154">없으면 hello 앱을 사용할 수 있지만 hello 실제 항목으로 더 재미 있게 되며 비용이 많이 드는 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="1f607-155">온보드 진단 (OBD)는 자동차를 사용 하 여 tootune 차고 hello 및 홀수 소음 및 경고 램프 진단 하는 자동차의 hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="1f607-156">자동차의 훌륭한 아주 오래 전부 아니면 hello 객실 hello 대시보드에서 플랩이 일반적으로 뒤의 어딘가에 소켓을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="1f607-157">Hello 오른쪽 연결선으로 hello 엔진의 성능 메트릭을 가져올 수 있으며 특정 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="1f607-158">OBD 커넥터 hello 일반적인 위치에서 저렴 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="1f607-159">휴대폰에서 Bluetooth 또는 Wi-fi tooan 앱을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="1f607-160">이 예에서 여기 tooconnect 자동차 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="1f607-161">hello OBD의에서 직접 연결 hello tooyour 전화 않으며 릴레이로 작동 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="1f607-162">자동차의 원격 분석 직선 toohello MyDriving IoT 허브, 여기서는 처리 toolog도로 전송 하 고 구동 스타일을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="1f607-163">tooconnect OBD 장치:</span><span class="sxs-lookup"><span data-stu-id="1f607-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="1f607-164">자동차에 OBD 소켓이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="1f607-165">OBD 어댑터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="1f607-166">Android 또는 Windows 휴대폰을 사용하는 경우 Bluetooth 가능 OBD II 어댑터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="1f607-167">[BAFX Products 34t5 Bluetooth OBDII Scan Tool]을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="1f607-168">iOS 휴대폰을 사용하는 경우 Wi-Fi 가능 OBD 어댑터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="1f607-169">[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="1f607-170">와 함께 제공 되 OBD 어댑터 tooconnect 것 tooyour 전화 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="1f607-171">Hello 다음을 염두에 두십시오.</span><span class="sxs-lookup"><span data-stu-id="1f607-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="1f607-172">Bluetooth 어댑터 hello 전화 hello에와 쌍이 되어야 합니다 **설정을** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1f607-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="1f607-173">Wi-fi 어댑터 hello 범위 192.168.xxx.xxx는 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="1f607-174">자동차가 여러 대 있는 경우 각각 별도의 어댑터를 가져올 수 있습니다(최대 3개).</span><span class="sxs-lookup"><span data-stu-id="1f607-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="1f607-175">OBD 어댑터를 설정 하지 않은 경우 hello 앱 종료 및 toosimulate는 OBD 원하면 묻습니다 위치와 속도 hello 전화 GPS 수신기 toohello 다시 데이터로 여전히 송신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="1f607-176">Hello에 섹션 2.1, "IoT 장치"에 고유한 OBD 장치를 만들기 위한 옵션 및 hello 앱 hello OBD 어댑터의 데이터를 사용 하는 방법에 대 한 자세한 내용을 확인할 수 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="1f607-177">Hello 응용 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1f607-177">Use hello app</span></span>
<span data-ttu-id="1f607-178">Hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-178">Start hello app.</span></span> <span data-ttu-id="1f607-179">초기 퀵 스타트 toowalk는 작동 방법 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="1f607-180">사용자의 주행을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-180">Track your trips</span></span>
<span data-ttu-id="1f607-181">Hello 레코드 단추 (hello hello 화면 맨 아래에 빨간색 원이 큰) toostart 여행을 누르고 다시 tooend입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![여정 추적에 대 한 hello 레코드 단추 그림](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="1f607-183">여행을 시작할 때마다 없는 OBD 장치인 경우 묻는 toouse hello 시뮬레이터 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="1f607-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="1f607-184">이동의 hello 끝 tap hello 중지 단추 수행 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![주행 요약의 예](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="1f607-186">주행을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-186">Review your trips</span></span>
![지난 주행의 예](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="1f607-188">프로필을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-188">Review your profile</span></span>
![운전 스타일 프로필의 예](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="1f607-190">테스트 사용자 의견을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-190">Send us your test feedback</span></span>
<span data-ttu-id="1f607-191">사용자 고유의 IoT 시스템 MyDriving toohelp 신속 작성 했기 때문에 얼마나 잘 작동 하는 방법에 대 한 사용자의 toohear 확실히 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="1f607-192">다음의 경우 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="1f607-192">Let us know if:</span></span>

* <span data-ttu-id="1f607-193">문제 또는 도전 과제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="1f607-194">만들 때와 더 적합 한 tooyour 시나리오 있는 확장 지점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="1f607-195">특정 요구를 보다 효율적인 방식으로 tooaccomplish 찾을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="1f607-196">MyDriving 또는 이 설명서를 개선하기 위한 다른 제안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="1f607-197">자체 hello MyDriving 앱 내에서 기본 제공 hello HockeyApp 피드백 메커니즘을 사용할 수 있습니다: iOS 및 Android 지정 휴대폰은 흔들기 하거나 hello를 사용 하 여 **피드백** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="1f607-198">그러면 스크린샷에 자동으로 연결되어 말하는 내용을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="1f607-199">및 모든 든 충돌 인 HockeyApp 수집 hello 크래시 로그 tootell us에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="1f607-200">Hello 통해 피드백을 제공할 수 있습니다 [HockeyApp 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="1f607-201">또한 [GitHub의 문제점]을 제출하거나 아래에 의견을 남길 수도 있습니다(en-US 버전).</span><span class="sxs-lookup"><span data-stu-id="1f607-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="1f607-202">의견에 귀 toohearing에서 있습니다!</span><span class="sxs-lookup"><span data-stu-id="1f607-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f607-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f607-203">Next steps</span></span>
* <span data-ttu-id="1f607-204">Hello 탐색 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs) म 한 설계 및 구축 방법 toounderstand hello 전체 MyDriving 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="1f607-205">[사용자 고유의 시스템을 만들고 배포](iot-solution-build-system.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="1f607-206">hello [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs) 수도 있는 할 hello 대부분의 사용자 지정 영역을 통해 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f607-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[GitHub에서]: https://github.com/Azure-Samples/MyDriving
[Xamarin을 사용하여]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp 포털]: https://rink.hockeyapp.org
[GitHub의 문제점]: https://github.com/Azure-Samples/MyDriving/issues
