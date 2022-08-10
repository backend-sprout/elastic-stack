# 로그백 태그 설명 

* configuration : 로그백 설정을 위한 태그 
* appender : log의 형태를 설정, 로그 메시지가 출력될 대상을 결정하는 요소
* root, logger : appender를 참조하여 package와 level을 설정한다.
    * root : 전역 설정
    * loggerf : 지역 설정
        * additivity 값은 root 설정 상속 유무 설정.(default = true)


```
<configuration>
  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder>
      <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
  </appender>

  <root level="debug">
    <appender-ref ref="STDOUT" />
  </root>
</configuration>
```
