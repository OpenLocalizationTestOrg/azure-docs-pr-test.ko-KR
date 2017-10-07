---
title: "AD aaaAzure v2 iOS 시작-구성 ARP () | Microsoft Docs"
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
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="21647-103">Hello 응용 프로그램의 등록 정보 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="21647-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="21647-104">이 단계에서는 tooadd hello 응용 프로그램 Id tooyour 프로젝트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="21647-104">In this step, you need tooadd hello Application Id tooyour project:</span></span>

1.  <span data-ttu-id="21647-105">`ViewController.swift`, 대체 hello 줄으로 시작 '`let kClientID`' 사용:</span><span class="sxs-lookup"><span data-stu-id="21647-105">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="21647-106">제어 상태에서 클릭 <code>Info.plist</code> toobring hello 상황에 맞는 메뉴 및 클릭: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="21647-106">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="21647-107">Hello에서 <code>dict</code> 루트 노드 hello 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="21647-107">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
