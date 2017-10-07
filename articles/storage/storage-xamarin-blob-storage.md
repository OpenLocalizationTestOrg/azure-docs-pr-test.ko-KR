---
title: "Xamarin에서 Blob 저장소 aaaHow toouse | Microsoft Docs"
description: "hello Xamarin에 대 한 Azure 저장소 클라이언트 라이브러리는 개발자가 toocreate iOS, Android 및 Windows 스토어 앱의 네이티브 사용자 인터페이스를 가진 수 있습니다. 이 자습서에서는 어떻게 toouse Xamarin toocreate Azure Blob 저장소를 사용 하는 응용 프로그램입니다."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>어떻게 toouse Xamarin에서 Blob 저장소
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>개요
Xamarin 사용 하면 개발자가 toouse 공유 C# toocreate iOS, Android 및 Windows 스토어 앱의 네이티브 사용자 인터페이스를 가진 codebase 합니다. 이 자습서에서는 어떻게 toouse Xamarin 응용 프로그램과 함께 Azure Blob 저장소입니다. Hello 코드 알아보기 전에 Azure 저장소에 대 한 자세한 toolearn 싶으시면 참조 [Azure 저장소 소개 tooMicrosoft](storage-introduction.md)합니다.

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>새 Xamarin 응용 프로그램 만들기
이 자습서에서는 Android, iOS 및 Windows를 대상으로 하는 앱을 만듭니다. 이 앱은 단순히 컨테이너를 만들고 이 컨테이너에 blob을 업로드합니다. 사용할 예정 Visual Studio 창, 있지만 hello macOS에서 Xamarin Studio를 사용 하 여 앱을 만드는 경우 동일한 정보를 적용할 수 있습니다.

이러한 단계 toocreate 응용 프로그램을 수행 합니다.

1. 아직 하지 않은 경우 [Visual Studio용 Xamarin](https://www.xamarin.com/download)을 다운로드하여 설치합니다.
2. Visual Studio를 열고 [비어 있는 앱(네이티브 이식 가능)]을 만듭니다(**파일 > 새로 만들기 > 프로젝트 > 플랫폼 간 > 비어 있는 앱(네이티브 공유)**).
3. Hello 솔루션 탐색기 창에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **솔루션에 대 한 NuGet 패키지 관리**합니다. 검색할 **WindowsAzure.Storage** hello 최신 안정화 버전 tooall 프로젝트 솔루션에 설치 합니다.
4. 프로젝트를 빌드한 후 실행합니다.

Tooclick 카운터를 증가 시키는 단추를 허용 하는 응용 프로그램을 만들었습니다.

## <a name="create-container-and-upload-blob"></a>컨테이너 만들기 및 blob 업로드
아래에서 다음 프로그램 `(Portable)` 프로젝트를 일부 코드를 너무 추가`MyClass.cs`합니다. 이 코드는 컨테이너를 만들고 이 컨테이너에 Blob을 업로드합니다. `MyClass.cs`hello 다음과 같이 표시 됩니다.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

있는지 tooreplace "your_account_name_here" 및 "your_account_key_here" 실제 계정 이름과 계정 키를 확인 합니다. 

모든 프로젝트에 대 한 참조 tooyour 휴대용 프로젝트-하나에 모든 공유 코드를 작성할 수 있습니다는 하 여 iOS, Android 및 Windows Phone 놓고 모든 프로젝트에서 사용 합니다. 이제 다음 줄의 코드 tooeach 프로젝트 toostart 사용해 hello를 추가할 수 있습니다.`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
이제 Android 또는 Windows Phone 에뮬레이터에서 이 응용 프로그램을 실행할 수 있습니다. iOS 에뮬레이터에서 이 응용 프로그램을 실행할 수도 있지만 Mac이 있어야 합니다. 에 대 한 특정 지침은 어떻게 toodo이 문서를 참조 하십시오 hello에 대 한 [Visual Studio tooa Mac에 연결](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

앱을 실행 한 후 hello 컨테이너 만듭니다 `mycontainer` 저장소 계정에 있습니다. Hello blob 있어야 `myblob`, hello 텍스트가 `Hello, world!`합니다. Hello를 사용 하 여이 확인할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서 배운 toocreate Xamarin에서 플랫폼 간 응용 프로그램을 사용 하는 방법을 Azure 저장소, Blob 저장소의 한 가지 시나리오 특히 중점 합니다. 그러나 Blob Storage 뿐만 아니라 Table, File 및 Queue Storage로도 많은 작업을 수행할 수 있습니다. 다음 문서 toolearn 자세한 hello를 참조 하세요.

* [.NET을 사용하여 Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md)
* [.NET을 사용하여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md)
* [.NET을 사용하여 Azure 큐 저장소 시작](storage-dotnet-how-to-use-queues.md)
* [Windows에서 Azure 파일 저장소 시작](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

