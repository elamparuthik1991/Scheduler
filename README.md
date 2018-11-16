# Scheduler
Scheduler time based running...

## 1. Configuration ExampleApplication.java
we need to configure in application "ExampleApplication.java"

```java
package com.example.pro;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.web.support.SpringBootServletInitializer;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.domain.AuditorAware;
import org.springframework.data.jpa.repository.config.EnableJpaAuditing;
import org.springframework.scheduling.annotation.EnableScheduling;

//@EnableScheduling is for enable scheduler...
@EnableScheduling
@Configuration
@SpringBootApplication
@EnableAutoConfiguration
public class ExampleApplication extends SpringBootServletInitializer {

	@Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(SmartMeterApplication.class);
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(SmartMeterApplication.class, args);
    }
```


## 2.ScheduleJobForExample.java
we need to configure @Component in begining of the class and @Scheduled to run according to the timing in class name "ScheduleJobForExample.java"
```java
package com.haroob.smartmeter.scheduler;

import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.List;
import java.util.concurrent.TimeUnit;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class ScheduleJobForExample {

	@Autowired
	private CustomerRepository customerRepository;
	
	private static final Logger LOGGER = LoggerFactory.getLogger(ScheduleJobForExample.class);

//	@Scheduled(fixedRateString = "${meter.update.reading.fixedRate.in.milliseconds}")
	@Scheduled(cron = "0 0 14 * * ?")//"0 0 12 * * ?" = 12 pm; "0 0 1 * * ?" = 1 am
	public void perform() throws InvalidDataException, IOException, ParseException {
		LOGGER.debug("ScheduleJob starts with time interval : " + checkMeterLogEntryTime);
```

		

## Conclusion
End of this integration.

## References
To make edit this document please use [edit readme.md](https://www.makeareadme.com/#rendered-1).
