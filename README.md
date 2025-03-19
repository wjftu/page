logging.file.name=logs/myapp.log

<configuration>
    <!-- 引用 Spring Boot 的 logging.file.name 属性 -->
    <springProperty scope="context" name="LOG_FILE" source="logging.file.name" defaultValue="logs/myapp.log" />

    <!-- 控制台输出 -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- 文件输出 -->
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOG_FILE}</file>  <!-- 使用 ${LOG_FILE} 作为日志文件路径 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 归档文件命名规则 -->
            <fileNamePattern>${LOG_FILE}-%d{yyyy-MM-dd}-%i.gz</fileNamePattern>
            <!-- 日志文件保留天数 -->
            <maxHistory>30</maxHistory>
            <!-- 日志文件大小限制 -->
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>10MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- 日志级别配置 -->
    <root level="INFO">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
    </root>
</configuration>
