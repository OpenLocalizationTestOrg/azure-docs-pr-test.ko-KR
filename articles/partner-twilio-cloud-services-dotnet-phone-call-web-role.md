---
title: "Twilio (.NET)에서 전화 통화를 aaaHow toomake | Microsoft Docs"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 코드 샘플은 .NET으로 작성되었습니다."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="d67da-104">Toomake 휴대폰 호출 방법을 Twilio를 사용 하 여 Azure에서 웹 역할에서</span><span class="sxs-lookup"><span data-stu-id="d67da-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="d67da-105">이 가이드 방법을 toouse Twilio toomake 웹 페이지에서 호출 하는 Azure에서 호스트 되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="d67da-106">hello 결과 응용 프로그램 메시지 hello 사용자 toomake hello 스크린 샷 뒤에 표시 된 대로 번호와 메시지를 제공 하는 hello로 호출을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Twilio 및 ASP.NET을 사용하는 Azure 통화 양식][twilio_dotnet_basic_form]

## <span data-ttu-id="d67da-108"><a name="twilio-prereqs"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="d67da-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="d67da-109">Toodo hello 다음 해야이 항목의 toouse hello 코드:</span><span class="sxs-lookup"><span data-stu-id="d67da-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="d67da-110">Twilio 계정 및 인증을 획득 hello에서 토큰 [Twilio 콘솔][twilio_console]합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="d67da-111">tooget 시작 Twilio, 기호에서 [https://www.twilio.com/try-twilio][try_twilio]합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="d67da-112">[http://www.twilio.com/pricing][twilio_pricing]에서 가격을 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="d67da-113">Hello Twilio에서 제공 하는 API에 대 한 정보를 참조 하십시오. [http://www.twilio.com/voice/api][twilio_api]합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="d67da-114">Hello 추가 *Twilio.NET 라이브러리* tooyour 웹 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="d67da-115">참조 **tooadd hello Twilio 라이브러리 tooyour 웹 역할 프로젝트**이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="d67da-116">[Azure에서 기본적인 웹 역할][azure_webroles_get_started] 만들기에 익숙해져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="d67da-117"><a name="howtocreateform"></a>방법: 전화 걸기 웹 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="d67da-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="d67da-118"><a id="use_nuget"></a>tooadd hello Twilio 라이브러리 tooyour 웹 역할 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="d67da-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="d67da-119">Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="d67da-120">**참조**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-120">Right-click **References**.</span></span>
3. <span data-ttu-id="d67da-121">**NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="d67da-122">**온라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-122">Click **Online**.</span></span>
5. <span data-ttu-id="d67da-123">Hello 검색 온라인 상자에 입력 *twilio*합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="d67da-124">클릭 **설치** hello Twilio 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="d67da-125">코드 다음 hello toocreate 웹 전화 걸기 tooretrieve 사용자 데이터를 형성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="d67da-126">이 예제에서는 **TwilioCloud**라는 ASP.NET 웹 역할이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="d67da-127"><a id="howtocreatecode"></a>방법: hello 코드 toomake hello 호출 만들기</span><span class="sxs-lookup"><span data-stu-id="d67da-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="d67da-128">hello hello 폼을 완료 하는 hello 사용자가을 라고 하는 다음 코드 hello 호출 메시지를 만들고 hello 호출을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="d67da-129">이 예제에서는 hello 코드 hello 양식에 hello 단추의 hello onclick 이벤트 처리기에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="d67da-130">(너무 할당 hello 자리 표시자 값 대신 Twilio 계정 및 인증 토큰을 사용 하 여`accountSID` 및 `authToken` hello 코드 아래에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d67da-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="d67da-131">hello 호출을 수행 하 고 hello Twilio 끝점, API 버전 및 hello 호출 상태 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="d67da-132">실행 하는 샘플에서 스크린 샷 표시 출력 다음 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-132">hello following screenshot shows output from a sample run.</span></span>

![Twilio 및 ASP.NET을 사용하는 Azure 통화 응답][twilio_dotnet_basic_form_output]

<span data-ttu-id="d67da-134">TwiML에 대한 자세한 내용은 [http://www.twilio.com/docs/api/twiml][twiml]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="d67da-135">&lt;Say&gt; 및 기타 Twilio 동사에 대한 정보는 [http://www.twilio.com/docs/api/twiml/say][twilio_say]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="d67da-136"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="d67da-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="d67da-137">이 코드는 tooshow 제공한 하면 기본 기능 Twilio를 사용 하 여 Azure에서 ASP.NET 웹 역할에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="d67da-138">프로덕션 환경에서 tooAzure를 배포 하기 전에 tooadd 자세한 오류 처리 또는 다른 기능을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="d67da-139">예:</span><span class="sxs-lookup"><span data-stu-id="d67da-139">For example:</span></span>

* <span data-ttu-id="d67da-140">Web form을 사용 하는 대신 Azure Blob 저장소 또는 Azure SQL 데이터베이스 인스턴스 toostore 전화 번호를 사용 하 고 텍스트를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="d67da-141">Azure에서 Blob을 사용 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 toouse hello.NET에서 Azure Blob 저장소 서비스][howto_blob_storage_dotnet]합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="d67da-142">SQL 데이터베이스를 사용 하는 방법에 대 한 정보를 참조 하십시오. [toouse Azure SQL 데이터베이스 방법.NET 응용 프로그램에서][howto_sql_azure_dotnet]합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="d67da-143">사용할 수 있습니다 `RoleEnvironment.getConfigurationSettings` 폼에서 하드 코딩 hello 값이 아닌 배포의 구성 설정에서 tooretrieve hello Twilio 계정 ID 및 인증 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="d67da-144">Hello에 대 한 내용은 `RoleEnvironment` 클래스를 참조 하십시오. [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet]합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="d67da-145">hello Twilio 보안 지침을 읽고 [https://www.twilio.com/docs/security][twilio_docs_security]합니다.</span><span class="sxs-lookup"><span data-stu-id="d67da-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="d67da-146">[https://www.twilio.com/docs][twilio_docs]에서 Twilio에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d67da-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="d67da-147"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="d67da-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d67da-148">어떻게 toouse Twilio Azure에서 음성 및 SMS 기능에 대 한</span><span class="sxs-lookup"><span data-stu-id="d67da-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
