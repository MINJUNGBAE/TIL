### Context
* 단편화된 메모나 학습 내용을 기록할 때마다 수동으로 문서화하고 GitHub에 업로드하는 과정의 비효율성을 해결하고자 함.
* n8n을 활용하여 Discord 메시지 수신부터 AI를 활용한 Markdown 포맷 변환, GitHub 커밋 및 README 업데이트까지 이어지는 전체 자동화 파이프라인(Pipeline)을 첫 워크플로우로 성공적으로 구축함.

### Core
* Discord Trigger Node
  * Discord 채널에서 메시지 수신 이벤트가 발생할 때 워크플로우를 시작하도록 트리거(Trigger)를 설정함.
  * 메시지 내용을 텍스트 데이터로 추출하여 다음 노드로 전달함.
* AI Agent Node
  * 전달받은 원시 데이터를 사전에 정의된 프롬프트를 통해 TIL 형식의 구조화된 데이터로 변환함.
  * LLM(대형 언어 모델)을 호출하여 텍스트 포맷팅 및 내용 구조화를 수행함.
* GitHub Node
  * 파일 생성(Create File) 오퍼레이션을 사용하여 변환된 TIL 문서를 지정된 저장소(Repository)에 커밋(Commit)함.
  * 파일 업데이트(Update File) 오퍼레이션을 통해 최상위 README 파일을 불러오고, 새롭게 생성된 파일의 인덱스를 추가하여 다시 커밋함.
* Discord Node
  * 모든 작업이 정상적으로 완료되었음을 알리는 피드백 메시지를 발신하여 워크플로우 루프를 종료함.

### Insight
* n8n 기반의 노드 아키텍처는 처음 접하더라도 각 노드가 요구하는 입력(Input) 데이터와 반환하는 출력(Output) 구조만 명확하게 이해하면 매우 직관적인 설계가 가능함을 확인하였음.
* 노드 간 데이터 페이로드(Payload)의 흐름을 파악하는 것이 복잡한 워크플로우를 구성하고 디버깅하는 데 가장 중요한 핵심 요소임.
* 강력한 자동화 개념과 n8n 활용법의 기초를 제공해 준 후츠릿(Hutsrit)에게 큰 감사를 표함.
* **출처:** [n8n Discord Node Documentation](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.discord/)
* **출처:** [n8n GitHub Node Documentation](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.github/)
* **출처:** [n8n Advanced AI Documentation](https://docs.n8n.io/advanced-ai/)