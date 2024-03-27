build.gradle에 dependencies에 아래 추가 후 Load Gradle Changes 하면 됨
<br>
```
 testImplementation 'org.springframework.boot:spring-boot-starter-test'
	//JUnit4 추가
	testImplementation("org.junit.vintage:junit-vintage-engine") {
		exclude group: "org.hamcrest", module: "hamcrest-core"
	}
