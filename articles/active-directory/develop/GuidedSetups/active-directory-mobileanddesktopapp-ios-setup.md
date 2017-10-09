---
title: "AD aaaAzure v2 iOS 설치 시작 | Microsoft Docs"
description: "iOS(Swift) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="7e5a7-103">iOS 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="7e5a7-103">Setting up your iOS application</span></span>

<span data-ttu-id="7e5a7-104">이 섹션에서는 방법에 대 한 단계별 지침을 제공 toocreate 새 프로젝트 toodemonstrate 어떻게 toointegrate iOS 응용 프로그램 (Swift)와 *Microsoft를 사용 하 여 로그인* 토큰을 필요로 하는 웹 Api를 쿼리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="7e5a7-105">더 선호 toodownload이이 샘플의 XCode 프로젝트?</span><span class="sxs-lookup"><span data-stu-id="7e5a7-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="7e5a7-106">[프로젝트를 다운로드](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) toohello 건너뛸 [구성 단계](#create-an-application-express) tooconfigure hello 코드 샘플을 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="7e5a7-107">Carthage toodownload를 설치 및 MSAL 작성</span><span class="sxs-lookup"><span data-stu-id="7e5a7-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="7e5a7-108">Carthage 패키지 관리자는 MSAL hello 미리 보기 기간 동안 사용 됩니다.-Microsoft toomake 변경 toohello 라이브러리에 대 한 hello 기능을 유지 하면서 XCode와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="7e5a7-109">다운로드 및 설치 hello 최신 릴리스의 Carthage [여기](https://github.com/Carthage/Carthage/releases "Carthage 다운로드 URL")</span><span class="sxs-lookup"><span data-stu-id="7e5a7-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="7e5a7-110">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="7e5a7-110">Creating your application</span></span>

1.  <span data-ttu-id="7e5a7-111">Xcode를 열고 `Create a new Xcode project`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="7e5a7-112">`iOS` > `Single view Application`을 선택하고 *다음*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="7e5a7-113">제품 이름을 지정하고 *다음*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="7e5a7-114">앱과 클릭 폴더 toocreate 선택 *만들기*</span><span class="sxs-lookup"><span data-stu-id="7e5a7-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="7e5a7-115">Hello MSAL 프레임 워크 빌드</span><span class="sxs-lookup"><span data-stu-id="7e5a7-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="7e5a7-116">Toopull 아래 지침을 hello 하 고 hello Carthage를 사용 하 여 MSAL 라이브러리의 최신 버전을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="7e5a7-117">Hello bash 터미널을 열고 toohello 응용 프로그램의 루트 폴더를 이동</span><span class="sxs-lookup"><span data-stu-id="7e5a7-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="7e5a7-118">Hello 아래에서 복사 및 붙여넣기 hello bash 터미널 toocreate 'Cartfile' 파일:</span><span class="sxs-lookup"><span data-stu-id="7e5a7-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="7e5a7-119">복사한 hello 아래에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-119">Copy and paste hello below.</span></span> <span data-ttu-id="7e5a7-120">이 명령은 Carthage/체크 아웃 폴더에 종속성을 인출 하 고 hello MSAL 라이브러리가 구축 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="7e5a7-121">위의 hello 프로세스에 사용 되는 toodownload 되며 빌드 hello Microsoft 인증 라이브러리 (MSAL).</span><span class="sxs-lookup"><span data-stu-id="7e5a7-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="7e5a7-122">MSAL 가져오는, 캐싱 및 사용자 토큰 tooaccess hello Azure Active Directory v 2에 의해 보호 되는 Api를 새로 고침을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="7e5a7-123">Hello MSAL 프레임 워크 tooyour 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="7e5a7-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="7e5a7-124">Xcode에서 엽니다 hello `General` 탭</span><span class="sxs-lookup"><span data-stu-id="7e5a7-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="7e5a7-125">Toohello 이동 `Linked Frameworks and Libraries` 섹션 및 클릭`+`</span><span class="sxs-lookup"><span data-stu-id="7e5a7-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="7e5a7-126">`Add other…`을(를) 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="7e5a7-127">`Carthage` > `Build` > `iOS` > `MSAL.framework`를 선택하고 *열기*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="7e5a7-128">표시 되어야 `MSAL.framework` toohello 목록이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="7e5a7-129">너무 이동`Build Phases` 탭을 클릭 `+` 아이콘을 선택`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="7e5a7-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="7e5a7-130">다음 내용을 toohello hello 추가 *영역 스크립트*:</span><span class="sxs-lookup"><span data-stu-id="7e5a7-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="7e5a7-131">Hello 너무 다음 추가<code>Input Files</code> 클릭 하 여 <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="7e5a7-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="7e5a7-132">응용 프로그램 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="7e5a7-132">Creating your application’s UI</span></span>
<span data-ttu-id="7e5a7-133">Main.storyboard 파일은 프로젝트 템플릿의 일부로 자동으로 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="7e5a7-134">Toocreate hello 앱 UI 아래 hello 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="7e5a7-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="7e5a7-135">제어 상태에서 클릭 `Main.storyboard` toobring hello 상황에 맞는 메뉴 및을 차례로 클릭 합니다.`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="7e5a7-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="7e5a7-136">Hello 대체 `<scenes>` hello 코드 아래에 있는 노드:</span><span class="sxs-lookup"><span data-stu-id="7e5a7-136">Replace hello `<scenes>` node with hello code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
