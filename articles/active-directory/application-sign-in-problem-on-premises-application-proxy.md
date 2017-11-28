---
title: "Azure AD 응용 프로그램 프록시를 사용하여 온-프레미스 응용 프로그램에 로그인하는 데 문제가 있음 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시를 사용하여 Azure AD와 통합된 온-프레미스 응용 프로그램에 로그인할 수 없을 때 직면하는 일반적인 문제 해결"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 5687f789355cc9769d26b53e98486bb213c66419
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-on-premises-application-using-the-azure-ad-application-proxy"></a><span data-ttu-id="dcf05-103">Azure AD 응용 프로그램 프록시를 사용하여 온-프레미스 응용 프로그램에 로그인하는 데 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-103">Problems signing in to an on-premises application using the Azure AD application proxy</span></span>

<span data-ttu-id="dcf05-104">온-프레미스 응용 프로그램에 로그인하는 데 문제가 있을 경우 아래 단계를 시도하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf05-104">If you are having problems signing in an on-premises application, you can try following the steps below to resolving your problem.</span></span>

## <a name="i-can-load-my-application-but-something-on-the-page-looks-broken"></a><span data-ttu-id="dcf05-105">내 응용 프로그램을 로드할 수 있지만 페이지의 일부가 손상됨</span><span class="sxs-lookup"><span data-stu-id="dcf05-105">I can load my application, but something on the page looks broken</span></span>

<span data-ttu-id="dcf05-106">다음 문서는 이 범주에서 가장 일반적인 몇 가지 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf05-106">The following documents can help you to resolve some of the most common issues in this category.</span></span>

  * [<span data-ttu-id="dcf05-107">내 응용 프로그램으로 이동할 수 있지만 응용 프로그램 페이지가 올바르게 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="dcf05-107">I can get to my application, but the application page isn't displaying correctly</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-appearance-broken-problem/)
  * [<span data-ttu-id="dcf05-108">내 응용 프로그램으로 이동할 수 있지만 응용 프로그램을 로드하는 데 시간이 너무 오래 걸림</span><span class="sxs-lookup"><span data-stu-id="dcf05-108">I can get to my application, but the application takes too long to load</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-load-speed-problem/)
  * [<span data-ttu-id="dcf05-109">내 응용 프로그램으로 이동할 수 있지만 응용 프로그램 페이지의 링크가 작동하지 않음</span><span class="sxs-lookup"><span data-stu-id="dcf05-109">I can get to my application, but the links on the application page do not work</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-links-broken-problem/)

## <a name="im-having-a-connectivity-problem-my-application"></a><span data-ttu-id="dcf05-110">내 응용 프로그램에 연결 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-110">I'm having a connectivity problem my application</span></span>
  <span data-ttu-id="dcf05-111">다음 문서는 이 범주에서 가장 일반적인 몇 가지 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf05-111">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="dcf05-112">내 응용 프로그램에 대해 어떤 포트를 열지 모름</span><span class="sxs-lookup"><span data-stu-id="dcf05-112">I don't know what ports to open for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-ports-how-to/)
  * [<span data-ttu-id="dcf05-113">내 응용 프로그램에 대한 커넥터 그룹에 작동 중인 커넥터가 없으므로 문제가 발생함</span><span class="sxs-lookup"><span data-stu-id="dcf05-113">I encountered a problem because there was no working connector in a connector group for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-no-working-connector/)

## <a name="im-having-a-problem-configuring-the-azure-ad-application-proxy-in-the-admin-portal"></a><span data-ttu-id="dcf05-114">관리 포털에서 Azure AD 응용 프로그램 프록시를 구성하는 데 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-114">I'm having a problem configuring the Azure AD Application Proxy in the admin portal</span></span>
  <span data-ttu-id="dcf05-115">다음 문서는 이 범주에서 가장 일반적인 몇 가지 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf05-115">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="dcf05-116">응용 프로그램 프록시 응용 프로그램을 구성하는 데 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-116">I am having difficulty configuring an application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-how-to/)
  * [<span data-ttu-id="dcf05-117">내 응용 프로그램 프록시 응용 프로그램에 대해 Single Sign-On을 구성하는 방법을 모름</span><span class="sxs-lookup"><span data-stu-id="dcf05-117">I don't know how to configure single sign-on to my application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-sso-how-to/)
  * [<span data-ttu-id="dcf05-118">관리 포털에 내 응용 프로그램을 만들 때 문제가 발생함</span><span class="sxs-lookup"><span data-stu-id="dcf05-118">I encountered a problem when creating my application in admin portal</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-problem/)

## <a name="im-having-a-problem-setting-up-back-end-authentication-to-my-application"></a><span data-ttu-id="dcf05-119">내 응용 프로그램에 백 엔드 인증을 설정하는 데 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-119">I'm having a problem setting up back-end authentication to my application</span></span>
  <span data-ttu-id="dcf05-120">다음 문서는 이 범주에서 가장 일반적인 몇 가지 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf05-120">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="dcf05-121">Kerberos 제한 위임을 구성하는 방법을 모름</span><span class="sxs-lookup"><span data-stu-id="dcf05-121">I don't know how to configure Kerberos Constrained Delegation</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-kerberos-constrained-delegation-how-to/)
  * [<span data-ttu-id="dcf05-122">PingAccess로 내 응용 프로그램을 구성하는 방법을 모름</span><span class="sxs-lookup"><span data-stu-id="dcf05-122">I don't know how to configure my application with PingAccess</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-ping-access-how-to/)

## <a name="im-having-a-problem-when-signing-in-to-my-application"></a><span data-ttu-id="dcf05-123">내 응용 프로그램에 로그인할 때 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-123">I'm having a problem when signing in to my application</span></span>
  <span data-ttu-id="dcf05-124">다음 문서는 이 범주에서 가장 일반적인 몇 가지 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf05-124">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="dcf05-125">"Can't Access this Corporate Application"(회사 응용 프로그램에 액세스할 수 없음) 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="dcf05-125">I get a "Can't Access this Corporate Application" error</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-sign-in-bad-gateway-timeout-error/)

## <a name="im-having-a-problem-with-the-application-proxy-agent-connector"></a><span data-ttu-id="dcf05-126">응용 프로그램 프록시 에이전트 커넥터에 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-126">I'm having a problem with the Application Proxy Agent Connector</span></span>
  <span data-ttu-id="dcf05-127">다음 문서는 이 범주에서 가장 일반적인 몇 가지 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf05-127">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="dcf05-128">응용 프로그램 프록시 에이전트 커넥터를 설치하는 데 문제가 있음</span><span class="sxs-lookup"><span data-stu-id="dcf05-128">I am having issues installing the Application Proxy Agent Connector </span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connector-installation-problem/)

## <a name="next-steps"></a><span data-ttu-id="dcf05-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dcf05-129">Next steps</span></span>
[<span data-ttu-id="dcf05-130">온-프레미스 응용 프로그램에 보안된 원격 액세스를 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="dcf05-130">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
