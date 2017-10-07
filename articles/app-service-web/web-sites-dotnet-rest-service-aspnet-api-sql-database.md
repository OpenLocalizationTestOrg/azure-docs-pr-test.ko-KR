---
title: "ASP.NET 및 SQL DB를 사용 하 여 Azure에서 REST API aaaCreate | Microsoft Docs"
description: "자습서를 참조 하는 방법을 배웁니다 toodeploy 응용 프로그램을 사용 하 여 Visual Studio를 사용 하 여 ASP.NET Web API tooan Azure 웹 앱을 hello 하는 방법을."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Azure 앱 서비스에서 ASP.NET Web API 및 SQL 데이터베이스를 사용하여 REST 서비스 만들기
이 자습서에서는 어떻게 toodeploy ASP.NET 웹 응용 프로그램 tooan [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) Visual Studio 2013 또는 Visual Studio 2013 Community Edition hello 웹 게시 마법사를 사용 하 여 합니다. 

Azure 계정이 있으세요을 무료, 열 수 있으며 hello SDK Web Express에 대 한 Visual Studio 2013를 자동으로 설치 Visual Studio 2013, 아직 없는 경우. 따라서 Azure용 개발을 무료로 시작할 수 있습니다.

이 자습서에서는 이전에 Azure를 사용한 경험이 없다고 가정합니다. 이 자습서를 완료를 단순한 웹 앱 및 hello 클라우드에서 실행 해야 합니다.

다음 내용을 배웁니다.

* 어떻게 tooenable 시스템에 설치 하 여 Azure 개발 hello Azure SDK입니다.
* 어떻게 toocreate Visual Studio ASP.NET MVC 5 프로젝트 및 tooan Azure 응용 프로그램을 게시 합니다.
* Toouse hello ASP.NET Web API tooenable Restful API 호출 하는 방법입니다.
* 어떻게 toouse SQL 데이터베이스는 Azure에서 toostore 데이터입니다.
* Toopublish 응용 프로그램 tooAzure 업데이트 하는 방식입니다.

ASP.NET MVC 5를 기반으로 하는 간단한 대화 상대 목록 웹 응용 프로그램을 빌드하게 됩니다 및 사용 하 여 데이터베이스 액세스를 위해 ADO.NET Entity Framework hello 합니다. 다음 그림에서는 hello hello 완료 응용 프로그램:

![웹 사이트의 스크린샷][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Hello 프로젝트 만들기
1. Visual Studio 2013을 시작합니다.
2. Hello에서 **파일** 메뉴 클릭 **새 프로젝트**합니다.
3. Hello에 **새 프로젝트** 대화 상자에서 **Visual C#** 선택 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다. Hello 응용 프로그램 이름을 **ContactManager** 클릭 **확인**합니다.
   
    ![새 프로젝트 대화 상자](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. Hello에 **새 ASP.NET 프로젝트** 대화 상자, 선택 hello **MVC** 서식 파일을 검사 **웹 API** 클릭 하 고 **인증 변경**합니다.
5. Hello에 **인증 변경** 대화 상자를 클릭 **인증 안 함**, 클릭 하 고 **확인**합니다.
   
    ![인증 없음](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    만드는 hello 샘플 응용 프로그램에서 사용자가 toolog 요구 하는 기능 없을 있습니다. 방법에 대 한 내용은 tooimplement 인증 및 권한 부여 기능 참조 hello [다음 단계](#nextsteps) hello 끝이 자습서에는 섹션입니다. 
6. Hello에 **새 ASP.NET 프로젝트** 대화 상자에서 확인 되었는지 hello **호스트 클라우드 hello에** 선택 되 고 클릭 **확인**합니다.

이전에 tooAzure에 등록 하지 않은 경우에 증명된 toosign 됩니다.

1. hello 구성 마법사는 기반으로 고유 이름을 제안 *ContactManager* (hello 이미지 아래 참조). 근처에 있는 지역을 선택합니다. 사용할 수 있습니다 [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello 가장 낮은 대기 시간 데이터 센터입니다. 
2. 기존에 만든 데이터베이스 서버가 없으면 **새 서버 만들기**를 선택하고 데이터베이스 사용자 이름과 암호를 입력합니다.
   
    ![Azure 웹 사이트 구성](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

데이터베이스 서버를 설정한 경우 해당 toocreate 새 데이터베이스를 사용 합니다. 일반적으로 원하는 toocreate hello에 있는 여러 데이터베이스 및 데이터베이스 서버는 소중한 리소스를 테스트 및 개발 아닌 데이터베이스 마다 데이터베이스 서버를 만드는 동일한 서버입니다. 웹 사이트 및 데이터베이스에에서 있어야 hello 동일한 지역입니다.

![Azure 웹 사이트 구성](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Hello 페이지 머리글 및 바닥글을 설정 합니다.
1. **솔루션 탐색기**, hello 확장 *Views\Shared* 폴더를 열고 hello *_Layout.cshtml* 파일입니다.
   
    ![솔루션 탐색기의 _Layout.cshtml][newapp004]
2. Hello hello 내용 바꾸기 *Views\Shared_Layout.cshtml* 코드 다음 hello로 파일:

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

hello 태그 "내 ASP.NET 응용 프로그램"에서 변경 내용 hello 응용 프로그램 이름 위에 너무 "Contact Manager" 및 해당 링크를 제거 hello 너무**홈**, **에 대 한** 및 **연락처**합니다.

### <a name="run-hello-application-locally"></a>Hello 응용 프로그램을 로컬로 실행
1. CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.
   hello 응용 프로그램 홈 페이지 hello 기본 브라우저에 나타납니다.
    ![tooDo 목록 홈 페이지](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

이 하기만 하면 toodo 지금은 toocreate hello 응용 프로그램 tooAzure를 배포 합니다. 나중에 데이터베이스 기능을 추가하겠습니다.

## <a name="deploy-hello-application-tooazure"></a>Hello 응용 프로그램 tooAzure 배포
1. Visual Studio에서의 hello 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택 **게시** hello 상황에 맞는 메뉴에서입니다.
   
    ![프로젝트 상황에 맞는 메뉴의 게시][PublishVSSolution]
   
    hello **웹 게시** 마법사가 열립니다.
2. **게시**를 클릭합니다.

![설정 탭](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio hello 복사 프로세스를 hello 파일 toohello Azure 서버를 시작 합니다. hello **출력** 창 수행 된 배포 작업을 표시 하 고 hello 배포를 성공적으로 완료를 보고 합니다.

1. hello 기본 브라우저 toohello 사이트의 URL을 배포 하는 hello 자동으로 열립니다.
   
   hello 응용 프로그램을 만든 hello 클라우드에서 실행 됩니다.
   
   ![Azure에서 실행 되 고 tooDo 목록 홈 페이지][rxz2]

## <a name="add-a-database-toohello-application"></a>데이터베이스 toohello 응용 프로그램 추가
다음으로 hello MVC 응용 프로그램 tooadd hello 기능 toodisplay 업데이트 및 연락처를 업데이트 하 hello 데이터는 데이터베이스에 저장 합니다. hello 응용 프로그램이 hello Entity Framework toocreate hello 데이터베이스와 tooread를 사용 하 고 hello 데이터베이스에서 데이터를 업데이트 합니다.

### <a name="add-data-model-classes-for-hello-contacts"></a>Hello 연락처에 대 한 데이터 모델 클래스를 추가 합니다.
먼저 코드로 간단한 데이터 모델을 만듭니다.

1. **솔루션 탐색기**hello 모델 폴더를 마우스 오른쪽 단추로 클릭 하 여 **추가**, 차례로 **클래스**합니다.
   
    ![모델 폴더 상황에 맞는 메뉴의 클래스 추가][adddb001]
2. Hello에 **새 항목 추가** 대화 상자, 이름 hello 새 클래스 파일 *Contact.cs*, 클릭 하 고 **추가**합니다.
   
    ![새 항목 추가 대화 상자][adddb002]
3. Hello Contacts.cs 파일의 내용을 hello 코드 다음 hello로 대체 합니다.
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

hello **문의** 각 연락처와 ContactID hello 데이터베이스에 필요한 기본 키를 저장 하는 hello 데이터 클래스를 정의 합니다. Hello에 데이터 모델에 대 한 자세한 정보를 얻을 수 [다음 단계](#nextsteps) hello 끝이 자습서에는 섹션입니다.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Hello 연락처가 있는 응용 프로그램 사용자 toowork 수 있도록 하는 웹 페이지 만들기
hello ASP.NET MVC hello 스 캐 폴딩 기능은 자동으로 생성할 수 수행 하는 코드 생성, 읽기, 업데이트 및 삭제 (CRUD) 작업입니다.

## <a name="add-a-controller-and-a-view-for-hello-data"></a>컨트롤러와 hello 데이터에 대 한 보기를 추가 합니다.
1. **솔루션 탐색기**, 안녕하세요 Controllers 폴더를 확장 합니다.
2. Hello 프로젝트 빌드 **(Ctrl + Shift + B)**합니다. (스 캐 폴딩 메커니즘을 사용 하기 전에 hello 프로젝트를 빌드합니다 해야 합니다.) 
3. 안녕하세요 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, 클릭 하 고 **컨트롤러**합니다.
   
    ![컨트롤러 폴더 상황에 맞는 메뉴의 컨트롤러 추가][addcode001]
4. Hello에 **추가 스 캐 폴드** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 컨트롤러** 클릭 **추가**합니다.
   
   ![컨트롤러 추가](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Hello 컨트롤러 이름을 너무 설정**HomeController**합니다. 모델 클래스로 **Contact** 를 선택합니다. Hello 클릭 **새 데이터 컨텍스트에** hello에 대 한 hello 기본값 "ContactManager.Models.ContactManagerContext" क र च 단추 **새 데이터 컨텍스트 형식**합니다. **추가**를 클릭합니다.

    묻는 대화 상자가: "hello 이름 가진 파일이 HomeController 이미 종료 됩니다. Tooreplace 원하는 것? "입니다. **예**를 클릭합니다. Hello hello 새 프로젝트를 사용 하 여 만든 홈 컨트롤러를 덮어쓰는 것입니다. 사용 합니다 hello 새 홈 컨트롤러에 대 한 연락처 목록.

    Visual Studio에서 **Contact** 개체에 대한 CRUD 데이터베이스 작업의 컨트롤러 메서드와 뷰를 만듭니다.

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>마이그레이션을 사용 하도록 설정, hello 데이터베이스 만들기, 샘플 데이터와 데이터 이니셜라이저를 추가 합니다.
hello 다음 작업은 tooenable hello [Code First 마이그레이션을](http://curah.microsoft.com/55220) 만든 hello 데이터 모델을 기반으로 하는 주문 toocreate hello 데이터베이스의 기능입니다.

1. Hello에 **도구** 메뉴 선택 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.
   
    ![도구 메뉴의 패키지 관리자 콘솔][addcode008]
2. Hello에 **패키지 관리자 콘솔** 창의 hello 다음 명령을 입력 합니다.
   
        enable-migrations 
   
    hello **사용 마이그레이션** 명령은 만듭니다는 *마이그레이션* 폴더 이므로 해당 폴더에 넣습니다는 *Configuration.cs* 파일 tooconfigure 마이그레이션을 편집할 수 있습니다. 
3. Hello에 **패키지 관리자 콘솔** 창의 hello 다음 명령을 입력 합니다.
   
        add-migration Initial
   
    hello **추가 마이그레이션 초기** 라는 클래스를 생성 하는 명령  **&lt;date_stamp&gt;초기** hello 데이터베이스를 만듭니다. 첫 번째 매개 변수를 hello ( *초기* ) 되 고 사용 된 임의의 toocreate hello hello 파일 이름입니다. Hello에서 새 클래스 파일을 볼 수 **솔루션 탐색기**합니다.
   
    Hello에 **초기** 클래스 hello **를** 메서드 hello Contacts 테이블와 hello 만듭니다 **아래로** 메서드 (tooreturn toohello 이전 상태로 하려는 경우 사용) 하 여 삭제 합니다.
4. 열기 hello *Migrations\Configuration.cs* 파일입니다. 
5. Hello 다음 네임 스페이스를 추가 합니다. 
   
         using ContactManager.Models;
6. Hello 대체 *시드* 메서드 코드 다음 hello로:
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    위의이 코드를이 hello 연락처 정보를 사용 하 여 hello 데이터베이스를 초기화 합니다. 시드 hello 데이터베이스에 대 한 자세한 내용은 참조 하십시오. [디버깅 Entity Framework (EF) Db](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)합니다.
7. Hello에 **패키지 관리자 콘솔** hello 명령을 입력 합니다.
   
        update-database
   
    ![패키지 관리자 콘솔 명령][addcode009]
   
    hello **데이터베이스 업데이트** 실행 hello hello 데이터베이스를 만드는 첫 번째 마이그레이션. 기본적으로 SQL Server Express LocalDB 데이터베이스 서 hello 데이터베이스가 생성 됩니다.
8. CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다. 

hello 응용 프로그램 hello 시드 데이터를 표시 하 고 편집, 내용 및 삭제 링크를 제공 합니다.

![MVC 데이터 뷰][rxz3]

## <a name="edit-hello-view"></a>Hello 보기 편집
1. 열기 hello *Views\Home\Index.cshtml* 파일입니다. Hello 다음 단계에서 사용 하는 코드로 생성 된 hello 태그 바꿉니다 됩니다 [jQuery](http://jquery.com/) 및 [Knockout.js](http://knockoutjs.com/)합니다. 이 새 코드 웹 API를 사용 하 여에서 연락처 목록을 hello를 검색 하 고 JSON 및 바인딩 hello 문의 데이터 toohello UI knockout.js를 사용 하 여 합니다. 자세한 내용은 참조 hello [다음 단계](#nextsteps) hello 끝이 자습서에는 섹션입니다. 
2. Hello 파일의 내용을 hello 코드 다음 hello로 대체 합니다.
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. Hello 콘텐츠 폴더를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가**, 클릭 하 고 **새 항목...** .
   
    ![Content 폴더의 상황에 맞는 메뉴에서 스타일시트 추가][addcode005]
4. Hello에 **새 항목 추가** 대화 상자에 입력 **스타일** 에 hello 위쪽 오른쪽 검색 상자를 클릭 한 **스타일 시트**합니다.
    ![새 항목 추가 대화 상자][rxStyle]
5. 이름 hello 파일 *Contacts.css* 클릭 **추가**합니다. Hello 파일의 내용을 hello 코드 다음 hello로 대체 합니다.
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    이 스타일 시트 hello 레이아웃, 색 및 hello 연락처 관리자 앱에서 사용 되는 스타일에 대 한 사용 합니다.
6. 열기 hello *App_Start\BundleConfig.cs* 파일입니다.
7. 다음 코드 tooregister hello hello 추가 [Knockout](http://knockoutjs.com/index.html "KO") 플러그 인 합니다.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Knockout toosimplify 동적 JavaScript 코드를 hello 화면 템플릿을 처리를 사용 하 여이 샘플입니다.
8. Hello 내용을/css 항목 tooregister hello 수정 *contacts.css* 스타일 시트입니다. Hello 다음 줄을 변경 합니다.
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   아래와 같이 변경합니다.
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Hello 패키지 관리자 콘솔에서에서 다음 명령을 tooinstall Knockout hello를 실행 합니다.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Hello 웹 API Restful 인터페이스에 대 한 컨트롤러 추가
1. **솔루션 탐색기**에서 컨트롤러를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **컨트롤러...**를 클릭합니다. 
2. Hello에 **추가 스 캐 폴드** 대화 상자에 입력 **Entity Framework를 사용 하 여 작업을 포함 된 Web API 2 컨트롤러** 클릭 하 고 **추가**합니다.
   
    ![API 컨트롤러 추가](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. Hello에 **컨트롤러 추가** 대화 상자에 컨트롤러 이름으로 "ContactsController"를 입력 합니다. Hello에 대 한 "Contact (ContactManager.Models)"를 선택 **모델 클래스**합니다.  Hello에 대 한 hello 기본값 유지 **데이터 컨텍스트 클래스가**합니다. 
4. **추가**를 클릭합니다.

### <a name="run-hello-application-locally"></a>Hello 응용 프로그램을 로컬로 실행
1. CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.
   
    ![인덱스 페이지][intro001]
2. 연락처를 입력하고 **추가**를 클릭합니다. hello 앱 toohello 홈 페이지를 반환 하 고 입력 한 hello 연락처를 표시 합니다.
   
    ![할 일 모음 항목이 있는 인덱스 페이지][addwebapi004]
3. Hello 브라우저에서 추가 **/api/연락처** toohello URL입니다.
   
    hello 결과 URL http://localhost:1234/api/연락처와 비슷합니다. hello RESTful 웹 API 추가한 저장 hello 연락처를 반환 합니다. Firefox 및 Chrome은 XML 형식의 hello 데이터를 표시 됩니다.
   
    ![할 일 모음 항목이 있는 인덱스 페이지][rxFFchrome]

    IE는 tooopen 라는 메시지가 표시 되거나 hello 연락처 저장 됩니다.

    ![Web API 저장 대화 상자][addwebapi006]


    메모장 이나 브라우저에서 연락처를 반환 하는 hello를 열 수 있습니다.

    이 출력은 모바일 웹 페이지나 모바일 응용 프로그램 같은 다른 응용 프로그램에서 사용될 수 있습니다.

    ![Web API 저장 대화 상자][addwebapi007]

    **보안 경고**:이 시점에서 응용 프로그램은 안전 하지 않은 및 취약 한 tooCSRF 방식의 공격입니다. Hello 자습서의 뒷부분에 나오는 이러한 취약성을 제거 합니다. 자세한 내용은 [CSRF(교차 사이트 요청 위조) 공격 예방][prevent-csrf-attacks]을 참조하세요.
## <a name="add-xsrf-protection"></a>XSRF 보호 추가
교차 사이트 요청 위조 (XSRF 또는 CSRF 라고도 함)은 악성 웹 사이트 클라이언트 브라우저와 해당 브라우저에서 신뢰할 수 있는 웹 사이트 간의 상호 작용 hello 영향을 줄 수는 그에 따라 웹 호스팅 응용 프로그램에 대 한 공격입니다. 이러한 공격은 웹 브라우저에서 자동으로 모든 요청 tooa 웹 사이트와 함께 인증 토큰을 보냅니다 때문에 가능 합니다. hello 정식 예는 예: ASP는 인증 쿠키입니다. NET의 폼 인증 티켓입니다. 하지만 Windows 인증, 기본 인증 등 영구적 인증 메커니즘을 사용하는 웹 사이트가 이러한 공격의 대상이 될 수 있습니다.

XSRF 공격은 피싱 공격과는 구분됩니다. 피싱 공격 hello 교착 상태가 발생에서 상호 작용을 필요로 합니다. 피싱 공격에서는 악의적인 웹 사이트를 hello 대상 웹 사이트를 모방 합니다 및 hello 교착 상태가 발생 toohello 공격자가 중요 한 정보를 제공 하도록 속일 됩니다. XSRF 공격에서 종종 hello 교착 상태가 발생에서 필요한 조작은 하지 않습니다. 대신, hello 공격자가 모든 관련 쿠키 toohello 대상 웹 사이트를 자동으로 보낼 hello 브라우저에 의존 하므로 합니다.

자세한 내용은 참조 hello [웹 응용 프로그램 보안 프로젝트 열기](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\))합니다.

1. **솔루션 탐색기**에서 **ContactManager** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **클래스**를 클릭합니다.
2. 이름 hello 파일 *ValidateHttpAntiForgeryTokenAttribute.cs* hello 코드 다음에 추가 합니다.
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. Hello 다음 추가 *를 사용 하 여* 액세스 toohello 해야 하므로 문을 toohello 계약 컨트롤러 **[ValidateHttpAntiForgeryToken]** 특성입니다.
   
        using ContactManager.Filters;
4. Hello 추가 **[ValidateHttpAntiForgeryToken]** hello의 toohello Post 메서드 특성 **ContactsController** tooprotect XSRF 위협 옵니다. Toohello "PutContact", "PostContact" 추가 합니다 및 **DeleteContact** 작업 메서드.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. 업데이트 hello *스크립트* hello 섹션 *Views\Home\Index.cshtml* tooinclude 코드 tooget hello XSRF 토큰 파일입니다.
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>응용 프로그램 업데이트 tooAzure hello 및 SQL 데이터베이스를 게시 합니다.
toopublish hello 응용 프로그램을 이전에 따른 hello 절차를 반복 합니다.

1. **솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.
   
    ![게시][rxP]
2. Hello 클릭 **설정을** 탭 합니다.
3. 아래 **ContactsManagerContext(ContactsManagerContext)**, hello 클릭 **v** 아이콘 toochange *원격 연결 문자열* hello 연락처에 대 한 toohello 연결 문자열 데이터베이스입니다. **ContactDB**를 클릭합니다.
   
    ![설정](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. 에 대 한 hello 확인란 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다.
5. **다음**을 클릭한 후 **미리 보기**를 클릭합니다. Visual Studio에 추가 하거나 업데이트할 수 있는 hello 파일의 목록이 표시 됩니다.
6. **게시**를 클릭합니다.
   Hello 배포가 완료 된 후 hello 브라우저 hello 응용 프로그램의 toohello 홈 페이지를 엽니다.
   
    ![연락처가 없는 인덱스 페이지][intro001]
   
    배포 된 hello에 hello 연결 문자열을 자동으로 구성 하는 프로세스를 게시 하는 hello Visual Studio *Web.config* toopoint toohello SQL 데이터베이스 파일입니다. 또한 Code First 마이그레이션을 tooautomatically 업그레이드 hello 데이터베이스 toohello 최신 버전 hello 첫 번째 시간 hello 응용 프로그램 배포 후 hello 데이터베이스에 액세스를 구성 합니다.
   
    이 구성으로 인해 코드 첫 번째 데이터베이스를 만들었습니다 hello hello에 hello 코드를 실행 하 여 **초기** 앞에서 만든 클래스입니다. 배포 후이 hello 첫 번째 시간 hello 응용 프로그램 시도 tooaccess hello 데이터베이스에서 수행한 합니다.
7. Hello 응용 프로그램을 로컬로 설치에 데이터베이스 배포 성공 tooverify 실행 되었을 때 수행한 대로 연락처를 입력 합니다.

입력 하면 해당 hello 항목이 저장 되 고 hello 연락처 관리자 페이지에 표시를 보면 hello 데이터베이스에 저장 되어 있는 알 수 있습니다.

![연락처가 있는 인덱스 페이지][addwebapi004]

hello 응용 프로그램은 이제 클라우드에서 실행 중인 hello, toostore SQL 데이터베이스를 사용 하 여 해당 데이터입니다. Azure의 hello 응용 프로그램 테스트를 마친 후 삭제 합니다. hello 응용 프로그램은 공용 및 메커니즘 toolimit 액세스할 수 없는 합니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
Azure 응용 프로그램에서 다른 방식으로 toostore 데이터 toouse Azure 저장소 blob 및 테이블 hello 형태로 비관계형 데이터 저장소를 제공 하는 경우 링크를 따라 hello 웹 API, ASP.NET MVC 및 Window Azure에서 자세한 정보를 제공 합니다.

* [MVC를 사용하여 Entity Framework 시작][EFCodeFirstMVCTutorial]
* [소개 tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [최초 ASP.NET 앱 API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [WAWS 디버그](web-sites-dotnet-troubleshoot-visual-studio.md)

이 자습서와 hello 샘플 응용 프로그램에 의해 작성 되었으므로 [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) Tom Dykstra 및 Barry Dorrans의 도움을 받아 (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

좋아 있습니다 또는 원하는 toosee 자체 hello 자습서 정보 뿐만 아니라 코드를 보여 줍니다 hello 제품에 대 한 향상 된 사용자 의견을 남겨 주세요. 사용자 의견은 개선 사항의 우선 순위를 지정하는 데 도움이 됩니다. 하는 hello 프로세스에 대 한 많은 자동화 구성 하 고 hello 멤버 자격 데이터베이스 배포에 얼마나 많은 관심 있는 인지 찾기에 특히 관심이 많습니다. 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

