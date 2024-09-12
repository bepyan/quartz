[[RAG]]의 검색기로, 
주어진 쿼리에 대해 가장 관련성 높은 정보를 대규모 문서 집합에서 효율적으로 찾아내는 컴포넌트이다.

주어진 문서에서 사용자의 질문과 관련된 정보를 신속하게 찾아내는 용도로 많이 활용된다.

**주요 기능**

- 텍스트 인덱싱: 대량의 문서를 효율적으로 검색할 수 있는 형태로 변환
- 유사도 계산: 쿼리와 문서 간의 관련성을 수치화
- 랭킹: 가장 관련성 높은 문서들을 선별

사전에 문서를 벡터로 변환하여 벡터 데이터베이스에 저장하고,
입력 쿼리를 벡터로 변환하여 벡터 데이터베이스에서 유사한 문서 검색하고,
가장 관련성 높은 문서(ex: 상위 3개)를 선별한다.

코드로 보면 대충 아래와 같다.

```ts
import { RecursiveCharacterTextSplitter } from "langchain/text_splitter";
import { MemoryVectorStore } from "langchain/vectorstores/memory";

const docs = await textSplitter.createDocuments(texts);
const embeddings = new OpenAIEmbeddings();
const vectorStore = await MemoryVectorStore.fromDocuments(docs, embeddings);

// vectorStore에서 상위 3개의 관련 문서를 검색하는 retriever를 생성
const retriever = vectorStore.asRetriever(3);
```
