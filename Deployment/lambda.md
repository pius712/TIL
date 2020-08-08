# AWS Lambda

AWS Lambda는 ec2처럼 직접 서버를 구축하여 관리할 필요가 없이 사용가능한 클라우드 서비스이다. 필요시에만 코드를 실행시킬 수 있다. 
AWS 자체적으로 서버 및 운영 체제 유지 관리, 용량 프로비저닝 및 자동 조정, 코드 및 보안 패치 배포, 코드 모니터링 및 로깅 등 모든 컴퓨팅 리소스 관리를 수행하기 때문에, 코드만 제공하면 된다.

AWS Lambda를 사용하여 Amazon S3 버킷 또는 Amazon DynamoDB 테이블의 데이터 변경과 같은 이벤트에 대한 응답으로 코드를 실행할 수 있다. Amazon API Gateway를 사용하여 HTTP 요청에 대한 응답으로 코드를 실행할 수도 있으며, 또는 AWS SDK를 사용하여 만든 API 호출을 통해 코드를 호출할 수 있습니다. 

## Lambda Application

AWS Lambda 애플리케이션의 구성
- Lambda 함수
- 이벤트 소스 및 기타 리소스의 조합  

 AWS CloudFormation 및 기타 도구를 사용해 애플리케이션의 구성 요소를 하나의 리소스로 배포해 관리할 수 있는 단일 패키지로 수집할 수 있습니다. 애플리케이션은 Lambda 프로젝트를 이동하기 쉽게 만들어 AWS CodePipeline, AWS CodeBuild 및 AWS Serverless Application Model 명령줄 인터페이스(SAM CLI) 등과 같은 추가 개발자 도구와 통합이 가능하게 합니다.

- `AWS Serverless Application Repository`는 몇 번만 클릭하여 간편하게 계정에 배포할 수 있는 Lambda 애플리케이션 모음을 제공합니다. 리포지토리에는 바로 사용할 수 있는 애플리케이션과 프로젝트의 시작 지점으로 사용할 수 있는 샘플이 들어 있습니다. 또한 자체 프로젝트를 제출해 포함할 수도 있습니다.

- `AWS CloudFormation`에서는 애플리케이션의 리소스를 정의하는 템플릿을 생성할 수 있고 애플리케이션을 스택으로 관리할 수 있습니다. 애플리케이션 스택에서는 리소스를 더욱 안전하게 추가 또는 수정할 수 있습니다. 한 부분이라도 업데이트에 실패하면 AWS CloudFormation에서는 이전 구성으로 자동으로 롤백합니다. AWS CloudFormation 파라미터를 사용해 동일한 템플릿에서 애플리케이션을 위한 여러 환경을 생성할 수 있습니다. AWS SAM은 Lambda 애플리케이션 개발에 중점을 둔 간소화된 구문으로 AWS CloudFormation을 확장합니다.

- `AWS CLI 및 SAM CLI`는 Lambda 애플리케이션 스택을 관리하기 위한 명령줄 도구입니다. AWS CloudFormation API를 사용해 애플리케이션 스택을 관리하기 위한 명령 이외에 AWS CLI는 배포 패키지 업로드 및 템플릿 업데이트 등과 같은 작업을 간소화하는 상위 수준 명령을 지원합니다. AWS SAM CLI는 템플릿 확인 및 로컬 테스트를 포함하여 추가 함수를 제공합니다.

## 기본 개념

### Function

아래와 같은 핸들러를 가지고 있고, event가 들어오면 이 함수를 실행해서 response를 보내준다. 

```js
exports.handler = async (event) => {
    // TODO implement
  const response = {
      statusCode: 200,
      body: JSON.stringify('hello lambda'),
  };
  return response;
};
```

### Event

이벤트는 처리할 함수에 대한 데이터가 포함된 JSON이다. Lambda 런타임은 이벤트를 객체로 변환한 후 함수 코드에 전달합니다. 함수를 호출할 때, 이벤트의 구조와 내용을 결정합니다.

