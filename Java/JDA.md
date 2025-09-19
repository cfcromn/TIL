## JDA란?

디스코드 API를 자바로 다룰 수 있게 해주는 라이브러리이다

HTTP REST API + WebSocket 이벤트를 자바스럽게 감싸서 메서도 호출이나 이벤트 리스너를 활용해 디스코드 봇을 쉽게 만들 수 있게 해준다

## 사용법

### build.gradle에 의존성을 추가한다.

```java
dependencies {
    implementation 'net.dv8tion:JDA:5.0.0-beta.20'
}
```

### 봇 실행 코드

```java
import net.dv8tion.jda.api.JDABuilder;
import net.dv8tion.jda.api.entities.Activity;

public class Bot {
    public static void main(String[] args) throws Exception {
        JDABuilder.createDefault("YOUR_BOT_TOKEN")
            .setActivity(Activity.playing("Test"))
            .addEventListeners(new MyListener())
            .build();
    }
}
```

createDefault(token) : 토근으로 JDA 인스턴스 빌드를 생성

.setActivity(...) : 디스코드 상태 메시지 설정

.addEventListeners(new MyListener()) : 이벤트를 받을 리스너 등록

.build() : WebSocket 연결 시작해서 봇 실행

### 이벤트 리스너 작성

```java
import net.dv8tion.jda.api.events.message.MessageReceivedEvent;
import net.dv8tion.jda.api.hooks.ListenerAdapter;

public class MyListener extends ListenerAdapter {
    @Override
    public void onMessageReceived(MessageReceivedEvent event) {
        if (!event.getAuthor().isBot() && event.getMessage().getContentRaw().equals("ping")) {
            event.getChannel().sendMessage("pong!").queue();
        }
    }
}
```

ListenerAdapter : JDA가 제공하는 기본 리스너로 필요한 이벤트만 오버라이드 하면 된다

onMessageReceived(...) : 메시지 도착시 호출되는 콜백

!event.getAuthor().isBot() : 봇이 보낸 메시지는 무시

getContentRaw().equals("ping") : 메시지 본문이 정확히 “ping”인지 검사

sendMessage(...).queue() : 비동기로 메시지 전송

.queue() : 성공/실패 콜백을 받을 수 있다 

## JDA에서 제공하는 기능

- 서버 연결 및 관리와 봇 상태나 활동 설정,  봇 권한 제어를 제공한다
- 텍스트 채널, DM 채널에 메시지를 보내거나 수정하거나 삭제 할 수 있다
- 유저 정보 조회 가능
- 멤버 강퇴/밴, 역할 추가/제거
- 여러가지 이벤트를 제공한다
- /를 이용한 명령어 형태의 Slach Command를 등록 할 수 있다
- 디스코드 음성 채널 입장/ 퇴장, 오디오 송출, 마이크 입력 받기가 가능하다
- 필요시 Discord REST 엔드포인트를 직접 호출이 가능하다