---
author: mikben
ms.service: azure-communication-services
ms.topic: include
ms.date: 9/1/2020
ms.author: mikben
ms.openlocfilehash: 5d81e37ab547d12e33cfacb9725d9bdb22666142
ms.sourcegitcommit: 86acfdc2020e44d121d498f0b1013c4c3903d3f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/17/2020
ms.locfileid: "97628712"
---
## <a name="prerequisites"></a>前提条件

- アクティブなサブスクリプションが含まれる Azure アカウント。 [無料でアカウントを作成できます](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。 
- デプロイ済みの Communication Services リソース。 [Communication Services リソースを作成します](../../create-communication-resource.md)。
- 通話クライアントを有効にするための `User Access Token`。 [`User Access Token` を取得する方法](../../access-tokens.md)についての詳細
- 省略可能:[アプリケーションへの通話の追加の概要](../getting-started-with-calling.md)に関するクイックスタートを完了します

## <a name="setting-up"></a>設定

### <a name="install-the-package"></a>パッケージをインストールする

<!-- TODO: update with instructions on how to download, install and add package to project -->
プロジェクト レベルの build.gradle を見つけて、`buildscript` および `allprojects` の下のリポジトリの一覧に `mavenCentral()` を追加します
```groovy
buildscript {
    repositories {
    ...
        mavenCentral()
    ...
    }
}
```

```groovy
allprojects {
    repositories {
    ...
        mavenCentral()
    ...
    }
}
```
次に、お使いのモジュール レベルの build.gradle で、次の行を dependencies セクションに追加します

```groovy
dependencies {
    ...
    implementation 'com.azure.android:azure-communication-calling:1.0.0-beta.2'
    ...
}

```

## <a name="object-model"></a>オブジェクト モデル

Azure Communication Services 通話クライアント ライブラリが備える主な機能のいくつかは、以下のクラスとインターフェイスにより処理されます。

| 名前                                  | 説明                                                  |
| ------------------------------------- | ------------------------------------------------------------ |
| CallClient| CallClient は、通話クライアント ライブラリへのメイン エントリ ポイントです。|
| CallAgent | CallAgent は、通話を開始および管理するために使用されます。 |
| CommunicationUserCredential | CommunicationUserCredential は、CallAgent をインスタンス化するためのトークン資格情報として使用されます。|

## <a name="initialize-the-callclient-create-a-callagent-and-access-the-devicemanager"></a>CallClient を初期化し、Callclient を作成して、DeviceManager にアクセスする

`CallAgent` インスタンスを作成するには、`CallClient` インスタンスで `createCallAgent` メソッドを呼び出す必要があります。 これにより、`CallAgent` インスタンス オブジェクトが非同期に返されます。
`createCallAgent` メソッドが引数として受け取る `CommunicationUserCredential` には、[アクセス トークン](../../access-tokens.md)がカプセル化されています。
`DeviceManager` にアクセスするには、最初に callAgent インスタンスを作成してから、`CallClient.getDeviceManager` メソッドを使用して DeviceManager を取得する必要があります。

```java
String userToken = '<user token>';
CallClient callClient = new CallClient();
CommunicationUserCredential tokenCredential = new CommunicationUserCredential(userToken);
android.content.Context appContext = this.getApplicationContext(); // From within an Activity for instance
CallAgent callAgent = await callClient.createCallAgent((appContext, tokenCredential).get();
DeviceManage deviceManager = await callClient.getDeviceManager().get();
```
呼び出し元の表示名を設定するには、この代替メソッドを使用します。

```java
String userToken = '<user token>';
CallClient callClient = new CallClient();
CommunicationUserCredential tokenCredential = new CommunicationUserCredential(userToken);
android.content.Context appContext = this.getApplicationContext(); // From within an Activity for instance
CallAgentOptions callAgentOptions = new CallAgentOptions();
callAgentOptions.setDisplayName("Alice Bob");
CallAgent callAgent = await callClient.createCallAgent((appContext, tokenCredential, callAgentOptions).get();
DeviceManage deviceManager = await callClient.getDeviceManager().get();
```


## <a name="place-an-outgoing-call-and-join-a-group-call"></a>発信通話を行って、グループ通話に参加する

通話を作成して開始するには、`CallAgent.call()` メソッドを呼び出して、通話先の `Identifier` を指定する必要があります。
グループ通話に参加するには、`CallAgent.join()` メソッドを呼び出して、groupId を指定する必要があります。 グループ ID は、GUID または UUID 形式にする必要があります。

通話の作成と開始は同期的に行われます。 通話インスタンスを使用すると、通話のすべてのイベントをサブスクライブできます。

### <a name="place-a-11-call-to-a-user"></a>ユーザーと 1:1 の通話を行う
別の Communication Services ユーザーと通話するには、`callAgent` で `call` メソッドを呼び出し、`communicationUserId` キーを使用してオブジェクトを渡します。
```java
StartCallOptions startCallOptions = new StartCallOptions();
Context appContext = this.getApplicationContext();
CommunicationUser acsUserId = new CommunicationUser(<USER_ID>);
CommunicationUser participants[] = new CommunicationUser[]{ acsUserId };
call oneToOneCall = callAgent.call(appContext, participants, startCallOptions);
```

### <a name="place-a-1n-call-with-users-and-pstn"></a>ユーザーおよび PSTN と 1:n の通話を行う
> [!WARNING]
> 現在、PSTN 通話は使用できません。ユーザーと PSTN 番号への 1:n の通話を行うには、通話先の電話番号を指定する必要があります。
PSTN 通話を許可するように Communication Services リソースを構成する必要があります。
```java
CommunicationUser acsUser1 = new CommunicationUser(<USER_ID>);
PhoneNumber acsUser2 = new PhoneNumber("<PHONE_NUMBER>");
CommunicationIdentifier participants[] = new CommunicationIdentifier[]{ acsUser1, acsUser2 };
StartCallOptions startCallOptions = new StartCallOptions();
Context appContext = this.getApplicationContext();
Call groupCall = callAgent.call(participants, startCallOptions);
```

### <a name="place-a-11-call-with-video-camera"></a>ビデオ カメラを使用して 1:1 の通話を行う
> [!WARNING]
> 現在、サポートされている発信ローカル動画ストリームは 1 つだけです。動画を使用して通話を行うには、`deviceManager` `getCameraList` API を使用して、ローカル カメラを列挙する必要があります。
目的のカメラを選択したら、それを使用して `LocalVideoStream` インスタンスを構築し、それを `call` メソッドへの `localVideoStream` 配列内の項目として、`videoOptions` に渡します。
通話が接続されると、選択したカメラから他の参加者への動画ストリームの送信が自動的に開始されます。

> [!NOTE]
> プライバシーに対する懸念から、動画がローカルでプレビューされていない場合に、通話に共有されることはありません。
詳細については、「[ローカル カメラのプレビュー](#local-camera-preview)」を参照してください。
```java
Context appContext = this.getApplicationContext();
VideoDeviceInfo desiredCamera = callClient.getDeviceManager().get().getCameraList().get(0);
LocalVideoStream currentVideoStream = new LocalVideoStream(desiredCamera, appContext);
VideoOptions videoOptions = new VideoOptions(currentVideoStream);

// Render a local preview of video so the user knows that their video is being shared
Renderer previewRenderer = new Renderer(currentVideoStream, appContext);
View uiView = previewRenderer.createView(new RenderingOptions(ScalingMode.Fit));
// Attach the uiView to a viewable location on the app at this point
layout.addView(uiView);

CommunicationUser[] participants = new CommunicationUser[]{ new CommunicationUser("<acs user id>") };
StartCallOptions startCallOptions = new StartCallOptions();
startCallOptions.setVideoOptions(videoOptions);
Call call = callAgent.call(context, participants, startCallOptions);
```

### <a name="join-a-group-call"></a>グループ通話に参加する
新しいグループ通話を始めるか、進行中のグループ通話に参加するには、"join" メソッドを呼び出して、`groupId` プロパティを含むオブジェクトを渡す必要があります。 値には GUID を指定する必要があります
```java
Context appContext = this.getApplicationContext();
GroupCallContext groupCallContext = new groupCallContext("<GUID>");
JoinCallOptions joinCallOptions = new JoinCallOptions();

call = callAgent.join(context, groupCallContext, joinCallOptions);
```

### <a name="accept-a-call"></a>着信を受け入れる
着信を受け入れるには、呼び出しオブジェクトに対して "accept" メソッドを呼び出します。

```java
Context appContext = this.getApplicationContext();
Call incomingCall = retrieveIncomingCall();
incomingCall.accept(context).get();
```

ビデオ カメラを使用して着信を受け入れるには:

```java
Context appContext = this.getApplicationContext();
Call incomingCall = retrieveIncomingCall();
AcceptCallOptions acceptCallOptions = new AcceptCallOptions();
VideoDeviceInfo desiredCamera = callClient.getDeviceManager().get().getCameraList().get(0);
acceptCallOptions.setVideoOptions(new VideoOptions(new LocalVideoStream(desiredCamera, appContext)));
incomingCall.accept(context, acceptCallOptions).get();
```

着信通話は、`callAgent` オブジェクトの `CallsUpdated` イベントをサブスクライブし、追加された通話をループ処理することによって取得できます。

```java
// Assuming "callAgent" is an instance property obtained by calling the 'createCallAgent' method on CallClient instance 
public Call retrieveIncomingCall() {
    Call incomingCall;
    callAgent.addOnCallsUpdatedListener(new CallsUpdatedListener() {
        void onCallsUpdated(CallsUpdatedEvent callsUpdatedEvent) {
            // Look for incoming call
            List<Call> calls = callsUpdatedEvent.getAddedCalls();
            for (Call call : calls) {
                if (call.getState() == CallState.Incoming) {
                    incomingCall = call;
                    break;
                }
            }
        }
    });
    return incomingCall;
}
```


## <a name="push-notifications"></a>プッシュ通知

### <a name="overview"></a>概要
モバイル プッシュ通知は、モバイル デバイスに表示されるポップアップ通知です。 通話に関しては、VoIP (ボイス オーバー IP 通話) でのプッシュ通知に焦点を絞ります。 プッシュ通知の登録を行い、プッシュ通知を処理してから、プッシュ通知を登録解除します。

### <a name="prerequisites"></a>前提条件

Cloud Messaging (FCM) が有効になっている Firebase アカウントが設定されており、Firebase Cloud Messaging サービスが Azure Notification Hubs インスタンスに接続されているものとします。 詳細については、「[Communication Services の通知](../../../concepts/notifications.md)」を参照してください。
また、このチュートリアルでは、Android Studio バージョン 3.6 以降を使用してアプリケーションがビルドされているものとします。

Firebase Cloud Messaging から通知メッセージを受信するには、Android アプリケーションに対する一連のアクセス許可が必要です。 お使いの `AndroidManifest.xml` ファイルの *<manifest ...>* の直後、または *</application>* タグの下に、次の一連のアクセス許可を追加します。

```XML
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
```

### <a name="register-for-push-notifications"></a>プッシュ通知に登録する

プッシュ通知を登録するには、アプリケーションは、デバイス登録トークンを使用して *CallAgent* インスタンスの `registerPushNotification()` を呼び出す必要があります。

デバイス登録トークンを取得するには、お使いのアプリケーション モジュールの *build.gradle* ファイルの `dependencies` セクションに次の行を追加して、Firebase クライアント ライブラリを追加します。

```
    // Add the client library for Firebase Cloud Messaging
    implementation 'com.google.firebase:firebase-core:16.0.8'
    implementation 'com.google.firebase:firebase-messaging:20.2.4'
```

まだない場合は、お使いのプロジェクト レベルの *build.gradle* ファイルの `dependencies` セクションに以下を追加します。

```
    classpath 'com.google.gms:google-services:4.3.3'
```

まだない場合、ファイルの先頭に次のプラグインを追加します。

```
apply plugin: 'com.google.gms.google-services'
```

ツール バーの *[今すぐ同期]* を選択します。 次のコード スニペットを追加し、クライアント アプリケーション インスタンス用に Firebase Cloud Messaging クライアント ライブラリで生成されたデバイス登録トークンを取得します。メイン Activity のヘッダーには、インスタンス用に次の import を必ず追加するようにしてください。 これらは、スニペットでトークンを取得するために必要です。

```
import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.iid.FirebaseInstanceId;
import com.google.firebase.iid.InstanceIdResult;
```

トークンを取得するには、このスニペットを追加します。

```
        FirebaseInstanceId.getInstance().getInstanceId()
                .addOnCompleteListener(new OnCompleteListener<InstanceIdResult>() {
                    @Override
                    public void onComplete(@NonNull Task<InstanceIdResult> task) {
                        if (!task.isSuccessful()) {
                            Log.w("PushNotification", "getInstanceId failed", task.getException());
                            return;
                        }

                        // Get new Instance ID token
                        String deviceToken = task.getResult().getToken();
                        // Log
                        Log.d("PushNotification", "Device Registration token retrieved successfully");
                    }
                });
```
着信通話プッシュ通知用の通話サービス クライアント ライブラリに、デバイス登録トークンを登録します。

```java
String deviceRegistrationToken = "<Device Token from previous section>";
try {
    callAgent.registerPushNotification(deviceRegistrationToken).get();
}
catch(Exception e) {
    System.out.println("Something went wrong while registering for Incoming Calls Push Notifications.")
}
```

### <a name="push-notification-handling"></a>プッシュ通知を処理する

着信通話プッシュ通知を受信するには、ペイロードを設定して *CallAgent* インスタンスで *handlePushNotification()* を呼び出します。

Firebase Cloud Messaging からペイロードを取得するには、*FirebaseMessagingService* Firebase クライアント ライブラリ クラスを拡張し、`onMessageReceived` メソッドをオーバーライドする、新しいサービスをまず作成 ([ファイル] > [新規] > [サービス] > [サービス]) します。 このメソッドは、Firebase Cloud Messaging によってアプリケーションにプッシュ通知が配信されると呼び出されるイベント ハンドラーです。

```java
public class MyFirebaseMessagingService extends FirebaseMessagingService {
    private java.util.Map<String, String> pushNotificationMessageDataFromFCM;

    @Override
    public void onMessageReceived(RemoteMessage remoteMessage) {
        // Check if message contains a notification payload.
        if (remoteMessage.getNotification() != null) {
            Log.d("PushNotification", "Message Notification Body: " + remoteMessage.getNotification().getBody());
        }
        else {
            pushNotificationMessageDataFromFCM = remoteMessage.getData();
        }
    }
}
```
次のサービス定義を `AndroidManifest.xml` ファイルの <application> タグ内に追加します。

```
        <service
            android:name=".MyFirebaseMessagingService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT" />
            </intent-filter>
        </service>
```

- ペイロードを取得したら、*CallAgent* インスタンスで *handlePushNotification* メソッドを呼び出すことによって処理されるように、*Communication Services* のクライアント ライブラリに渡すことができます。 `CallAgent` インスタンスを作成するには、`CallClient` クラスで `createCallAgent(...)` メソッドを呼び出します。

```java
try {
    callAgent.handlePushNotification(pushNotificationMessageDataFromFCM).get();
}
catch(Exception e) {
    System.out.println("Something went wrong while handling the Incoming Calls Push Notifications.");
}
```

プッシュ通知メッセージの処理が成功し、すべてのイベント ハンドラーが適切に登録されると、アプリケーションによって発信されます。

### <a name="unregister-push-notifications"></a>プッシュ通知の登録を解除する

アプリケーションによって、プッシュ通知の登録はいつでも解除できます。 登録を解除するには、callAgent で `unregisterPushNotification()` メソッドを呼び出します。

```java
try {
    callAgent.unregisterPushNotifications().get();
}
catch(Exception e) {
    System.out.println("Something went wrong while un-registering for all Incoming Calls Push Notifications.")
}
```

## <a name="call-management"></a>通話の管理
通話の間に、通話のプロパティにアクセスしてさまざまな操作を実行し、動画やオーディオに関連する設定を管理できます。

### <a name="call-properties"></a>通話のプロパティ

この通話の一意の ID を取得します。

```java
String callId = call.getCallId();
```

通話の他の参加者について知るには、`call` インスタンスの `remoteParticipant` コレクションを調べます。

```java
List<RemoteParticipant> remoteParticipants = call.getRemoteParticipants();
```

通話が着信の場合の呼び出し元の ID です。

```java
CommunicationIdentifier callerId = call.getCallerId();
```

通話の状態を取得します。 

```java
CallState callState = call.getState();
```

これにより、通話の現在の状態を表す文字列が返されます。
* "None" - 通話の初期状態です
* "Incoming" - 通話を着信中であり、受諾または拒否する必要があることを示します
* "Connecting" - 通話が発信または受諾された後の初期遷移状態です
* "Ringing" - 発信通話の場合 - リモート参加者に対して通話が発信されていることを示します。そちら側ではこれは "Incoming" です
* "EarlyMedia" - 通話が接続される前の、アナウンスの再生状態を示します
* "Connected" - 通話は接続されています
* "Hold" - 通話は保留になっており、ローカル エンドポイントとリモート参加者の間でメディアは送信されていません
* "Disconnecting" - 通話は、"Disconnected" 状態になる前の移行状態です
* "Disconnected" - 通話の最終状態です


通話が終了した理由を確認するには、`callEndReason` プロパティを調べます。 これには、コードとサブコードが含まれます。 

```java
CallEndReason callEndReason = call.getCallEndReason();
int code = callEndReason.getCode();
int subCode = callEndReason.getSubCode();
```

現在の通話が着信通話かどうかを確認するには、`isIncoming` プロパティを調べます。

```java
boolean isIncoming = call.getIsIncoming();
```

現在マイクがミュートされているかどうかを確認するには、`muted` プロパティを調べます。

```java
boolean muted = call.getIsMicrophoneMuted();
```

アクティブな動画ストリームを調べるには、`localVideoStreams` コレクションを確認します。

```java
List<LocalVideoStream> localVideoStreams = call.getLocalVideoStreams();
```

### <a name="mute-and-unmute"></a>ミュートとミュート解除

ローカル エンドポイントをミュートまたはミュート解除するには、非同期 API の `mute` と `unmute` を使用できます。

```java
call.mute().get();
call.unmute().get();
```

### <a name="start-and-stop-sending-local-video"></a>ローカル動画の送信を開始および停止する

動画を開始するには、`deviceManager` オブジェクトの `getCameraList` API を使用して、カメラを列挙する必要があります。 次に、目的のカメラを渡して `LocalVideoStream` の新しいインスタンスを作成し、それを引数として `startVideo` API に渡します。

```java
VideoDeviceInfo desiredCamera = <get-video-device>;
Context appContext = this.getApplicationContext();
currentVideoStream = new LocalVideoStream(desiredCamera, appContext);
videoOptions = new VideoOptions(currentVideoStream);
Future startVideoFuture = call.startVideo(currentVideoStream);
startVideoFuture.get();
```

動画の送信が正常に開始されると、通話インスタンスの `localVideoStreams` コレクションに `LocalVideoStream` インスタンスが追加されます。

```java
currentVideoStream == call.getLocalVideoStreams().get(0);
```

ローカル動画を停止するには、`localVideoStreams` コレクションで使用可能な `localVideoStream` インスタンスを渡します。

```java
call.stopVideo(localVideoStream).get();
```

`localVideoStream` インスタンスで `switchSource` を呼び出すことにより、動画の送信中に別のカメラ デバイスに切り替えることができます。
```java
localVideoStream.switchSource(source).get();
```

## <a name="remote-participants-management"></a>リモート参加者の管理

すべてのリモート参加者は `RemoteParticipant` 型で表され、通話インスタンスの `remoteParticipants` コレクションを通して使用できます。

### <a name="list-participants-in-a-call"></a>通話の参加者の一覧を取得する
`remoteParticipants` コレクションで、特定の通話におけるリモート参加者の一覧が返されます。
```java
List<RemoteParticipant> remoteParticipants = call.getRemoteParticipants(); // [remoteParticipant, remoteParticipant....]
```

### <a name="remote-participant-properties"></a>リモート参加者のプロパティ
特定のリモート参加者には、プロパティのセットとコレクションが関連付けられています。

* このリモート参加者の識別子を取得します。
ID は "Identifier" 型の 1 つです。
```java
CommunicationIdentifier participantIdentity = remoteParticipant.getIdentifier();
```

* このリモート参加者の状態を取得します。
```java
ParticipantState state = remoteParticipant.getState();
```
状態は次のいずれかです
* "Idle" - 初期状態です
* "Connecting" - 参加者が通話に接続している間の遷移状態です
* "Connected" - 参加者は通話に接続されています
* "Hold" - 参加者は保留中です
* "EarlyMedia" - 参加者が通話に接続される前に、アナウンスが再生されています
* "Disconnected" - 最終状態 - 参加者は通話から切断されました


* 参加者が通話を終了した理由を確認するには、`callEndReason` プロパティを調べます。
```java
CallEndReason callEndReason = remoteParticipant.getCallEndReason();
```

* このリモート参加者がミュートされているかどうかを確認するには、`isMuted` プロパティを調べます。
```java
boolean isParticipantMuted = remoteParticipant.getIsMuted();
```

* このリモート参加者が話しているかどうかを確認するには、`isSpeaking` プロパティを調べます。
```java
boolean isParticipantSpeaking = remoteParticipant.getIsSpeaking();
```

* 特定の参加者がこの通話で送信しているすべての動画ストリームを調べるには、`videoStreams` コレクションを確認します。
```java
List<RemoteVideoStream> videoStreams = remoteParticipant.getVideoStreams(); // [RemoteVideoStream, RemoteVideoStream, ...]
```


### <a name="add-a-participant-to-a-call"></a>通話に参加者を追加する

通話に参加者を追加するには (ユーザーまたは電話番号のいずれか)、`addParticipant` を呼び出します。 これにより、リモート参加者インスタンスが同期的に返されます。

```java
const acsUser = new CommunicationUser("<acs user id>");
const acsPhone = new PhoneNumber("<phone number>");
RemoteParticipant remoteParticipant1 = call.addParticipant(acsUser);
RemoteParticipant remoteParticipant2 = call.addParticipant(acsPhone);
```

### <a name="remove-participant-from-a-call"></a>通話から参加者を削除する
通話から参加者を削除するには (ユーザーまたは電話番号のいずれか)、`removeParticipant` を呼び出します。
参加者が通話から削除されると、非同期的に解決されます。
参加者は、`remoteParticipants` コレクションからも削除されます。
```java
RemoteParticipant remoteParticipant = call.getParticipants().get(0);
call.removeParticipant(acsUser).get();
call.removeParticipant(acsPhone).get();
```

## <a name="render-remote-participant-video-streams"></a>リモート参加者の動画ストリームをレンダリングする
リモート参加者の動画ストリームと画面共有ストリームの一覧を取得するには、`videoStreams` コレクションを調べます。
```java
RemoteParticipant remoteParticipant = call.getRemoteParticipants().get(0);
RemoteVideoStream remoteParticipantStream = remoteParticipant.getVideoStreams().get(0);
MediaStreamType streamType = remoteParticipantStream.getType(); // of type MediaStreamType.Video or MediaStreamType.ScreenSharing
```
 
リモート参加者からの `RemoteVideoStream` をレンダリングするには、`OnVideoStreamsUpdated` イベントをサブスクライブする必要があります。

イベント内で `isAvailable` プロパティが true に変更された場合、リモート参加者が現在ストリームを送信していることを示します。 それが発生したら、`Renderer` の新しいインスタンスを作成し、非同期 `createView` API を使用して新しい `RendererView` を作成し、お使いのアプリケーションの UI の任意の場所に `view.target` をアタッチします。

リモート ストリームの使用可能性が変わるたびに、レンダラー全体を破棄するか、特定の `RendererView` を破棄するか、それらを保持するかを選択できますが、これによって空の動画フレームが表示されます。

```java
Renderer remoteVideoRenderer = new Renderer(remoteParticipantStream, appContext);
View uiView = remoteVideoRenderer.createView(new RenderingOptions(ScalingMode.Fit));
layout.addView(uiView);

remoteParticipant.addOnVideoStreamsUpdatedListener(e -> onRemoteParticipantVideoStreamsUpdated(p, e));

void onRemoteParticipantVideoStreamsUpdated(RemoteParticipant participant, RemoteVideoStreamsEvent args) {
    for(RemoteVideoStream stream : args.getAddedRemoteVideoStreams()) {
        if(stream.getIsAvailable()) {
            startRenderingVideo();
        } else {
            renderer.dispose();
        }
    }
}
```

### <a name="remote-video-stream-properties"></a>リモート動画ストリームのプロパティ
リモート動画ストリームにはいくつかのプロパティがあります

* `Id` - リモート動画ストリームの ID です
```java
int id = remoteVideoStream.getId();
```

* `MediaStreamType` - "Video" または "ScreenSharing" になります
```java
MediaStreamType type = remoteVideoStream.getType();
```

* `isAvailable` - リモート参加者のエンドポイントでストリームをアクティブに送信されているかどうかを示します
```java
boolean availability = remoteVideoStream.getIsAvailable();
```

### <a name="renderer-methods-and-properties"></a>Renderer のメソッドとプロパティ
Renderer オブジェクトには次の API があります

* 後でアプリケーションの UI にアタッチしてリモート動画ストリームをレンダリングできる `RendererView` インスタンスを作成します。
```java
// Create a view for a video stream
renderer.createView()
```
* レンダラーと、このレンダラーに関連付けられているすべての `RendererView` を破棄します。 UI から関連付けられているすべてのビューを削除したときに呼び出します。
```java
renderer.dispose()
```

* `StreamSize` - リモート動画ストリームのサイズ (幅と高さ)
```java
StreamSize renderStreamSize = remoteVideoStream.getSize();
int width = renderStreamSize.getWidth();
int height = renderStreamSize.getHeight();
```


### <a name="rendererview-methods-and-properties"></a>RendererView のメソッドとプロパティ
`RendererView` を作成するときに、このビューに適用される `scalingMode` と `mirrored` プロパティを指定できます。スケーリング モードは "Stretch"、"Crop"、"Fit" です。`mirrored` を `true` に設定すると、レンダリングされたストリームは垂直方向に反転されます。

```java
Renderer remoteVideoRenderer = new Renderer(remoteVideoStream, appContext);
RendererView rendererView = remoteVideoRenderer.createView(new RenderingOptions(ScalingMode.Fit));
```

作成した RendererView は、次のスニペットを使用してアプリケーションの UI にアタッチできます。
```java
layout.addView(rendererView);
```

後で、RendererView オブジェクトの `updateScalingMode` API を呼び出し、ScalingMode.Stretch、ScalingMode.Crop、ScalingMode.Fit のいずれかを引数として指定することで、スケーリング モードを更新できます。
```java
// Update the scale mode for this view.
rendererView.updateScalingMode(ScalingMode.Crop)
```


## <a name="device-management"></a>デバイス管理

`DeviceManager` を使用すると、オーディオと動画のストリームを送信する呼び出しで使用できるローカル デバイスを列挙できます。 また、ネイティブ ブラウザー API を使用してマイクやカメラにアクセスするために、ユーザーにアクセス許可を要求することもできます。

`callClient.getDeviceManager()` メソッドを呼び出すことによって `deviceManager` にアクセスできます。
> [!WARNING]
> 現在、DeviceManager にアクセスするには、`callAgent` オブジェクトを最初にインスタンス化する必要があります

```java
DeviceManager deviceManager = callClient.getDeviceManager().get();
```

### <a name="enumerate-local-devices"></a>ローカル デバイスを列挙する

ローカル デバイスにアクセスするには、デバイス マネージャーで列挙メソッドを使用します。 列挙は同期アクションです。

```java
//  Get a list of available video devices for use.
List<VideoDeviceInfo> localCameras = deviceManager.getCameraList(); // [VideoDeviceInfo, VideoDeviceInfo...]

// Get a list of available microphone devices for use.
List<AudioDeviceInfo> localMicrophones = deviceManager.getMicrophoneList(); // [AudioDeviceInfo, AudioDeviceInfo...]

// Get a list of available speaker devices for use.
List<AudioDeviceInfo> localSpeakers = deviceManager.getSpeakerList(); // [AudioDeviceInfo, AudioDeviceInfo...]
```

### <a name="set-default-microphonespeaker"></a>既定のマイクとスピーカーを設定する

デバイス マネージャーを使用すると、通話の開始時に使用される既定のデバイスを設定できます。
クライアントの既定値が設定されていない場合、Communication Services は OS の既定値にフォールバックします。

```java

// Get the microphone device that is being used.
AudioDeviceInfo defaultMicrophone = deviceManager.getMicrophoneList().get(0);

// Set the microphone device to use.
deviceManager.setMicrophone(defaultMicrophone);

// Get the speaker device that is being used.
AudioDeviceInfo defaultSpeaker = deviceManager.getSpeakerList().get(0);

// Set the speaker device to use.
deviceManager.setSpeaker(defaultSpeaker);
```

### <a name="local-camera-preview"></a>ローカル カメラのプレビュー

`DeviceManager` と `Renderer` を使用して、ローカル カメラからのストリームのレンダリングを開始できます。 このストリームは、他の参加者には送信されません。ローカル プレビュー フィードです。 これは、非同期アクションです。

```java
VideoDeviceInfo videoDevice = <get-video-device>;
Context appContext = this.getApplicationContext();
currentVideoStream = new LocalVideoStream(videoDevice, appContext);
videoOptions = new VideoOptions(currentVideoStream);

Renderer previewRenderer = new Renderer(currentVideoStream, appContext);
View uiView = previewRenderer.createView(new RenderingOptions(ScalingMode.Fit));

// Attach the uiView to a viewable location on the app at this point
layout.addView(uiView);
```

## <a name="eventing-model"></a>イベント モデル
値が変更されたときに通知を受け取るように、ほとんどのプロパティとコレクションをサブスクライブすることができます。

### <a name="properties"></a>Properties
`property changed` イベントをサブスクライブするには:

```java
// subscribe
PropertyChangedListener callStateChangeListener = new PropertyChangedListener()
{
    @Override
    public void onPropertyChanged(PropertyChangedEvent args)
    {
        Log.d("The call state has changed.");
    }
}
call.addOnCallStateChangedListener(callStateChangeListener);

//unsubscribe
call.removeOnCallStateChangedListener(callStateChangeListener);
```

### <a name="collections"></a>コレクション
`collection updated` イベントをサブスクライブするには:

```java
LocalVideoStreamsChangedListener localVideoStreamsChangedListener = new LocalVideoStreamsChangedListener()
{
    @Override
    public void onLocalVideoStreamsUpdated(LocalVideoStreamsEvent localVideoStreamsEventArgs) {
        Log.d(localVideoStreamsEventArgs.getAddedStreams().size());
        Log.d(localVideoStreamsEventArgs.getRemovedStreams().size());
    }
}
call.addOnLocalVideoStreamsChangedListener(localVideoStreamsChangedListener);
// To unsubscribe
call.removeOnLocalVideoStreamsChangedListener(localVideoStreamsChangedListener);
```
