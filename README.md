# platform-useraccount-svc
## Summary

User Account Service is to manage the lifecycle of user account. 

APIs in Account Microservice will be consumed by Application Services to compose business scenarios such as login and hire
- Authentication Service will call API to validate an account is active or not 

## Service Design 
https://confluence.successfactors.com/display/AAR/Account+in+microservice

## API 
### Validate Account Profile
#### Design 
https://confluence.successfactors.com/display/ENG/Integration+between+Authentication+Service+and+UserAccount+Service
#### Service Endpoint
- local dev: http://127.0.0.1:8080/rest/internal/useraccount/v1/userAccountProfile
- DCE-engMS: https://platform-useraccount-svc.microservices.hcm-eng.c.eu-de-2.cloud.sap/rest/internal/useraccount/v1/userAccountProfile
#### Open API v3 and Swagger Config
https://platform-useraccount-svc.microservices.hcm-eng.c.eu-de-2.cloud.sap/v3/api-docs

## CI-CD info 
- Jenkins: https://jenkins.tools.hcm-eng.c.eu-de-2.cloud.sap/job/platformfoundations/job/useraccount/job/pfs-useraccount-svc/job/master/
- ArgoCD: https://argocd.tools.hcm-eng.c.eu-de-2.cloud.sap/applications/useraccount-svc
- SonarQube: https://sonar.wdf.sap.corp/dashboard?id=sf-ms-pfs-useraccount-svc&branch=master
- Security Scan: https://jenkins-security.tools.hcm-eng.c.eu-de-2.cloud.sap/job/security-scan/

## Local Development 
### Build
```bash
$ ./gradlew build  
```
Note: account service only supports Java 11 now 

### Start Services
You can choose the following as you like to start account service. If everything going well, you will be able to access backend API via http://localhost:8080.
#### Intellij Idea  
Manually start hana first and run the com.successfactors.platform.useraccount.AccountApplication.main method 
#### Gradlew 
Manually start hana first and run application from command line with gradlew: 
```bash
$ ./gradlew bootrun 
```

#### Docker-compose 
account service is stated with hana as default. 
```bash
$ ./start_dev_env.sh 
```

and stop them with: 
```bash
$ docker-compose down 
```
### API test 
The api of userAccountProfile is protected by JWT:
- Mock Bizx JWT with Symmetric Key: https://plumberservice.microservices.hcm-eng.c.eu-de-2.cloud.sap/public/mockBizxJwtToken?userId=admin&tenantId=BizXTest&tenantSchema=BIZX_BIZXTEST&tenantDataSource=dbPool1&immutableTenantId=BizXTest&langTag=en_US 
- Mock Bizx JWT with Asymmetric Key: https://plumberservice.microservices.hcm-eng.c.eu-de-2.cloud.sap/public/mockBizxJwtToken/asymmetric?userId=admin&tenantId=BizXTest&tenantSchema=BIZX_BIZXTEST&tenantDataSource=dbPool1&immutableTenantId=BizXTest&langTag=en_US

# databricks-skills
