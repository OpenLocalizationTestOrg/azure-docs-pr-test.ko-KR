---
title: "aaaHow tooConfigure TLS 웹 앱에 대 한 상호 인증"
description: "어떻게 tooconfigure 웹 앱 toouse 클라이언트 인증서 인증에 알아봅니다. TLS 합니다."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="98ada-103">어떻게 tooConfigure TLS 웹 앱에 대 한 상호 인증</span><span class="sxs-lookup"><span data-stu-id="98ada-103">How tooConfigure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="98ada-104">개요</span><span class="sxs-lookup"><span data-stu-id="98ada-104">Overview</span></span>
<span data-ttu-id="98ada-105">다양 한 유형의 것에 대 한 인증을 사용 하 여 tooyour Azure 웹 앱 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-105">You can restrict access tooyour Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="98ada-106">한 가지 방법은 toodo tooauthenticate hello 요청은 TLS/SSL을 통한 하는 경우 클라이언트 인증서를 사용 하 여이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-106">One way toodo so is tooauthenticate using a client certificate when hello request is over TLS/SSL.</span></span> <span data-ttu-id="98ada-107">이 메커니즘은 TLS 상호 인증이 나 클라이언트 인증서 인증 호출 되 고이 문서에서는 자세히 설명 방법을 toosetup 웹 앱 toouse 클라이언트 인증서 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how toosetup your web app toouse client certificate authentication.</span></span>

> <span data-ttu-id="98ada-108">**참고:** HTTP를 통해 사이트에 액세스하고 HTTPS를 통해서는 액세스하지 않는 경우 클라이언트 인증서가 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="98ada-109">따라서 응용 프로그램 클라이언트 인증서가 필요 하면 해야 없도록 요청 tooyour 응용 프로그램 over HTTP입니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-109">So if your application requires client certificates you should not allow requests tooyour application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="98ada-110">클라이언트 인증서 인증에 대 한 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="98ada-111">toosetup tooadd 필요한 웹 응용 프로그램 toorequire 클라이언트 인증서 hello clientCertEnabled 사이트 웹 앱에 대 한 설정 및 tootrue 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-111">toosetup your web app toorequire client certificates you need tooadd hello clientCertEnabled site setting for your web app and set it tootrue.</span></span> <span data-ttu-id="98ada-112">이 설정은 포털 hello에 hello 관리 환경을 통해 현재 사용 가능한 되며 hello REST API에 필요 사용 toobe tooaccomplish 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-112">This setting is not currently available through hello management experience in hello Portal, and hello REST API will need toobe used tooaccomplish this.</span></span>

<span data-ttu-id="98ada-113">Hello를 사용할 수 있습니다 [ARMClient 도구](https://github.com/projectkudu/ARMClient) toomake 하기 쉽게 toocraft hello REST API 호출을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-113">You can use hello [ARMClient tool](https://github.com/projectkudu/ARMClient) toomake it easy toocraft hello REST API call.</span></span> <span data-ttu-id="98ada-114">Hello 도구 로그인 한 후 다음 명령을 tooissue hello이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-114">After you log in with hello tool you will need tooissue hello following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="98ada-115">웹 앱에 대 한 정보로 {}의 모든 항목을 대체 하 고 파일을 만드는 콘텐츠를 호출한 경우 enableclientcert.json 다음 JSON hello로:</span><span class="sxs-lookup"><span data-stu-id="98ada-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with hello following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="98ada-116">웹 앱이 "위치" toowherever toochange hello 값 예: 미국 중 북부 또는 미국 등 서쪽 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-116">Make sure toochange hello value of "location" toowherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="98ada-117">Https://resources.azure.com tooflip hello를 사용할 수도 있습니다 `clientCertEnabled` 속성 너무`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-117">You can also use https://resources.azure.com tooflip hello `clientCertEnabled` property too`true`.</span></span>

> <span data-ttu-id="98ada-118">**참고:** ARMClient Powershell에서를 실행 하면 할 경우 tooescape hello @ 기호는 역따옴표 hello JSON 파일에 대 한 '.</span><span class="sxs-lookup"><span data-stu-id="98ada-118">**Note:** If you run ARMClient from Powershell, you will need tooescape hello @ symbol for hello JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a><span data-ttu-id="98ada-119">Hello 클라이언트 인증서에서 웹 응용 프로그램에 액세스</span><span class="sxs-lookup"><span data-stu-id="98ada-119">Accessing hello Client Certificate From Your Web App</span></span>
<span data-ttu-id="98ada-120">ASP.NET을 사용 하 여 응용 프로그램 toouse 클라이언트 인증서 인증을 구성 하는 경우 hello 인증서까지 사용할 수 있습니다 hello **HttpRequest.ClientCertificate** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-120">If you are using ASP.NET and configure your app toouse client certificate authentication, hello certificate will be available through hello **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="98ada-121">다른 응용 프로그램 스택에 대 한 클라이언트 인증서 hello hello "X ARR ClientCert" 요청 헤더의 base64 인코딩 값을 통해 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-121">For other application stacks, hello client cert will be available in your app through a base64 encoded value in hello "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="98ada-122">응용 프로그램은 이 값으로부터 인증서를 생성하고, 응용 프로그램에서 인증 및 권한 부여 목적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="98ada-123">인증서 유효성 검사에 대한 특별 고려 사항</span><span class="sxs-lookup"><span data-stu-id="98ada-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="98ada-124">toohello 응용 프로그램에 전송 되는 클라이언트 인증서를 hello 통과 하지 않으므로 모든 유효성 검사 hello Azure 웹 앱 플랫폼에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-124">hello client certificate that is sent toohello application does not go through any validation by hello Azure Web Apps platform.</span></span> <span data-ttu-id="98ada-125">이 인증서의 유효성 검사 하는 것은 hello 웹 앱의 hello 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-125">Validating this certificate is hello responsibility of hello web app.</span></span> <span data-ttu-id="98ada-126">인증을 위해 인증서 속성의 유효성을 검사하는 샘플 ASP.NET 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98ada-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
