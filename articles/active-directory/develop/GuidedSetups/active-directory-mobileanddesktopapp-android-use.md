---
title: "AD aaaAzure v2 Android 시작-사용 | Microsoft Docs"
description: "Android 앱이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 4480d89eb7638fe7d588c8cebd2b1e3c9d4c6e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Hello Microsoft 인증 라이브러리 (MSAL) tooget 토큰을 사용 하 여 hello Microsoft Graph API에 대 한

1.  (`app` > `java` > `{domain}.{appname}`에서) `MainActivity`를 엽니다.
2.  Hello 다음 가져오기를 추가 합니다.

```java
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import com.android.volley.*;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONObject;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import com.microsoft.identity.client.*;
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Hello 대체 `MainActivity` 아래 클래스:
</li>
</ol>

```java
public class MainActivity extends AppCompatActivity {

    final static String CLIENT_ID = "[Enter hello application Id here]";
    final static String SCOPES [] = {"https://graph.microsoft.com/User.Read"};
    final static String MSGRAPH_URL = "https://graph.microsoft.com/v1.0/me";

    /* UI & Debugging Variables */
    private static final String TAG = MainActivity.class.getSimpleName();
    Button callGraphButton;
    Button signOutButton;

    /* Azure AD Variables */
    private PublicClientApplication sampleApp;
    private AuthenticationResult authResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        callGraphButton = (Button) findViewById(R.id.callGraph);
        signOutButton = (Button) findViewById(R.id.clearCache);

        callGraphButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onCallGraphClicked();
            }
        });

        signOutButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onSignOutClicked();
            }
        });

  /* Configure your sample app and save state for this activity */
        sampleApp = null;
        if (sampleApp == null) {
            sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    CLIENT_ID);
        }

  /* Attempt tooget a user and acquireTokenSilent
   * If this fails we do an interactive request
   */
        List<User> users = null;

        try {
            users = sampleApp.getUsers();

            if (users != null && users.size() == 1) {
          /* We have 1 user */

                sampleApp.acquireTokenSilentAsync(SCOPES, users.get(0), getAuthSilentCallback());
            } else {
          /* We have no user */

          /* Let's do an interactive request */
                sampleApp.acquireToken(this, SCOPES, getAuthInteractiveCallback());
            }
        } catch (MsalClientException e) {
            Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

        } catch (IndexOutOfBoundsException e) {
            Log.d(TAG, "User at this position does not exist: " + e.toString());
        }

    }

//
// App callbacks for MSAL
// ======================
// getActivity() - returns activity so we can acquireToken within a callback
// getAuthSilentCallback() - callback defined toohandle acquireTokenSilent() case
// getAuthInteractiveCallback() - callback defined toohandle acquireToken() case
//

    public Activity getActivity() {
        return this;
    }

    /* Callback method for acquireTokenSilent calls 
     * Looks if tokens are in hello cache (refreshes if necessary and if we don't forceRefresh)
     * else errors that we need toodo an interactive request.
     */
    private AuthenticationCallback getAuthSilentCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call Graph now */
                Log.d(TAG, "Successfully authenticated");

            /* Store hello authResult */
                authResult = authenticationResult;

            /* call graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                } else if (exception instanceof MsalUiRequiredException) {
                /* Tokens expired or no session, retry with interactive */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }


    /* Callback used for interactive request.  If succeeds we use hello access
         * token toocall hello Microsoft Graph. Does not check cache
         */
    private AuthenticationCallback getAuthInteractiveCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call graph now */
                Log.d(TAG, "Successfully authenticated");
                Log.d(TAG, "ID Token: " + authenticationResult.getIdToken());

            /* Store hello auth result */
                authResult = authenticationResult;

            /* call Graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }

    /* Set hello UI for successful token acquisition data */
    private void updateSuccessUI() {
        callGraphButton.setVisibility(View.INVISIBLE);
        signOutButton.setVisibility(View.VISIBLE);
        findViewById(R.id.welcome).setVisibility(View.VISIBLE);
        ((TextView) findViewById(R.id.welcome)).setText("Welcome, " +
                authResult.getUser().getName());
        findViewById(R.id.graphData).setVisibility(View.VISIBLE);
    }

    /* Use MSAL tooacquireToken for hello end-user
     * Callback will call Graph api w/ access token & update UI
     */
    private void onCallGraphClicked() {
        sampleApp.acquireToken(getActivity(), SCOPES, getAuthInteractiveCallback());
    }

    /* Handles hello redirect from hello System Browser */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        sampleApp.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

}
```
<!--start-collapse-->
### <a name="more-information"></a>추가 정보
#### <a name="getting-a-user-token-interactive"></a>대화형 사용자 토큰 가져오기
호출 hello `AcquireTokenAsync` 확인 창에서 메서드 결과에 대 한 사용자 toosign hello 합니다. 응용 프로그램 일반적으로 필요에 대화형으로 hello 사용자 toosign tooaccess 필요한 처음으로 보호 된 리소스 되거나 자동 작업 tooacquire 토큰 실패 (예: hello 사용자의 암호 만료 됨).

#### <a name="getting-a-user-token-silently"></a>자동으로 사용자 토큰 가져오기
`AcquireTokenSilentAsync`는 토큰 획득 및 갱신을 자동으로 처리합니다. 후 `AcquireTokenAsync` 처음으로 hello에 대 한 실행 `AcquireTokenSilentAsync` hello 일반적으로 사용 되는 방법 tooobtain 토큰 tooaccess 호출 toorequest로 보호 되는 대 한 후속 호출-리소스 또는 토큰을 갱신은 자동으로 수행 됩니다.
결국 `AcquireTokenSilentAsync` 못합니다-예: hello 사용자가 로그 아웃 또는 다른 장치에서 암호 변경 되었습니다. MSAL 탐지 대화형 작업을 요구 하 여 hello 문제 해결을 발생 시킬는 `MsalUiRequiredException`합니다. 응용 프로그램에서는 이러한 예외를 다음 두 가지 방법으로 처리할 수 있습니다.

1.  에 대 한 호출 `AcquireTokenAsync` 즉시 줄어들고 결과적 toosign에 hello 사용자 확인 합니다. 이 패턴은 일반적으로 온라인 응용 프로그램에서 사용 되는 오프 라인 콘텐츠 hello 응용 프로그램의 hello 사용자에 대해 사용할 수 있습니다. hello이 단계별된 설치 프로그램에 의해 생성 된 샘플 사용 하 여이 패턴: 나타나면 작업 hello에 hello 샘플을 실행 하는 처음으로: 사용자 hello 응용 프로그램을 사용 하기 때문에 `PublicClientApp.Users.FirstOrDefault` null 값이 포함 됩니다 및 `MsalUiRequiredException` 예외가 throw 됩니다. 핸들 예외를 호출 하 여 hello 다음 hello 샘플의 코드를 hello `AcquireTokenAsync` toosign에 hello 사용자 확인 발생 합니다.
2.  응용 프로그램으로는 대화형 로그인가 필요 하지 않으므로 hello 선택할 수 있는, 적절 한 시기 toosign hello 또는 hello 응용 프로그램을 다시 시도할 수 있는 시각적으로 확인할 toohello 사용자 만들 수도 `AcquireTokenSilentAsync` 나중에 있습니다. 이 hello 사용자가 중단 되지 않고 hello 응용 프로그램의 수 tooaccess 기능-예를 들어 콘텐츠가 오프 라인 hello 응용 프로그램에서 사용할 수 있는 경우에 일반적으로 사용 됩니다. 때 toosign tooaccess hello 보호 된 리소스에서 원하는 또는 toorefresh hello 정보를 오래 된 항목 또는 응용 프로그램 tooretry를 결정할 수 hello 사용자 결정할 수는 경우 `AcquireTokenSilentAsync` 네트워크 일시적으로 사용할 수 없게 후 복원 된 경우.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>얻은 hello 토큰을 사용 하 여 hello Microsoft Graph API를 호출 합니다.
1.  Hello hello에 메서드를 다음 추가 `MainActivity` 클래스:

```java
/* Use Volley toomake an HTTP request toohello /me endpoint from MS Graph using an access token */
private void callGraphAPI() {
    Log.d(TAG, "Starting volley request toograph");

    /* Make sure we have a token toosend toograph */
    if (authResult.getAccessToken() == null) {return;}

    RequestQueue queue = Volley.newRequestQueue(this);
    JSONObject parameters = new JSONObject();

    try {
        parameters.put("key", "value");
    } catch (Exception e) {
        Log.d(TAG, "Failed tooput parameters: " + e.toString());
    }
    JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
            parameters,new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            /* Successfully called graph, process data and send tooUI */
            Log.d(TAG, "Response: " + response.toString());

            updateGraphUI(response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.d(TAG, "Error: " + error.toString());
        }
    }) {
        @Override
        public Map<String, String> getHeaders() throws AuthFailureError {
            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "Bearer " + authResult.getAccessToken());
            return headers;
        }
    };

    Log.d(TAG, "Adding HTTP GET tooQueue, Request: " + request.toString());

    request.setRetryPolicy(new DefaultRetryPolicy(
            3000,
            DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
            DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
    queue.add(request);
}

/* Sets hello Graph response */
private void updateGraphUI(JSONObject graphResponse) {
    TextView graphText = (TextView) findViewById(R.id.graphData);
    graphText.setText(graphResponse.toString());
}
```
<!--start-collapse-->
### <a name="more-information-about-making-a-rest-call-against-a-protected-api"></a>보호되는 API에 대한 REST 호출에 관한 추가 정보

이 샘플 응용 프로그램에서 `callGraphAPI` 호출 `getAccessToken` HTTP 다음 한 `GET` 토큰 하며 hello 콘텐츠를 반환 하는 리소스에 대 한 요청입니다. 이 메서드는 hello에서 토큰 획득 hello 추가 *HTTP 권한 부여 헤더*합니다. 이 샘플에 대 한 hello 리소스는 Microsoft Graph API hello *me* 끝점으로 – hello 사용자의 프로필 정보를 표시 합니다.
<!--end-collapse-->

## <a name="setup-sign-out"></a>로그아웃 설정

1.  Hello hello에 메서드를 다음 추가 `MainActivity` 클래스:

```java
/* Clears a user's tokens from hello cache.
 * Logically similar too"sign out" but only signs out of this app.
 */
private void onSignOutClicked() {

    /* Attempt tooget a user and remove their cookies from cache */
    List<User> users = null;

    try {
        users = sampleApp.getUsers();

        if (users == null) {
            /* We have no users */

        } else if (users.size() == 1) {
            /* We have 1 user */
            /* Remove from token cache */
            sampleApp.remove(users.get(0));
            updateSignedOutUI();

        }
        else {
            /* We have multiple users */
            for (int i = 0; i < users.size(); i++) {
                sampleApp.remove(users.get(i));
            }
        }

        Toast.makeText(getBaseContext(), "Signed Out!", Toast.LENGTH_SHORT)
                .show();

    } catch (MsalClientException e) {
        Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

    } catch (IndexOutOfBoundsException e) {
        Log.d(TAG, "User at this position does not exist: " + e.toString());
    }
}

/* Set hello UI for signed-out user */
private void updateSignedOutUI() {
    callGraphButton.setVisibility(View.VISIBLE);
    signOutButton.setVisibility(View.INVISIBLE);
    findViewById(R.id.welcome).setVisibility(View.INVISIBLE);
    findViewById(R.id.graphData).setVisibility(View.INVISIBLE);
    ((TextView) findViewById(R.id.graphData)).setText("No Data");
}
```
<!--start-collapse-->
### <a name="more-information"></a>자세한 정보

`onSignOutClicked`제거 위에 hello MSAL 사용자 캐시 –에서 사용자가 명령은 효과적으로 알려줍니다 MSAL tooforget hello에 대 한 현재 사용자는 후속 요청 tooacquire 만들어진 경우 toobe 대화형 토큰 성공만 됩니다.
MSAL 여러 계정을 hello에 로그인 될 수 있는 시나리오를 지원 hello 응용 프로그램에서이 샘플에서는 단일 사용자를 지원 하지만 동일한 시간-예로 전자 메일 응용 프로그램 사용자가 계정을 여러 개 있습니다.
<!--end-collapse-->
