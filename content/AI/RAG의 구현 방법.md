---
title: RAG의 구현 방법
date: 2024-09-04
tags:
  - seed
---

전체 프로세스는 아래와 같다.

1. 질문을 바탕으로 벡터 저장소에서 관련 문서를 검색한다.
2. 검색된 문서들을 LLM의 컨텍스트로 사용한다.
3. LLM이 주어진 컨텍스트와 질문을 바탕으로 답변을 생성한다.
4. 생성된 답변을 사용자에게 반환한다.

[[LangChain]] 에서 유용한 도구를 많이 제공해주기에 이를 잘 활용하면 된다.

```ts
import { ChatPromptTemplate } from "@langchain/core/prompts";
import { ChatOpenAI } from "@langchain/openai";
import { createStuffDocumentsChain } from "langchain/chains/combine_documents";
import { createRetrievalChain } from "langchain/chains/retrieval";
import { MemoryVectorStore } from "langchain/vectorstores/memory";

export async function buildRAGChain(vectorStore: MemoryVectorStore) {
  // 1. 검색기(Retriever) 설정
  // vectorStore에서 상위 3개의 관련 문서를 검색하는 retriever를 생성
  const retriever = vectorStore.asRetriever(3);

  // 2. 언어 모델(LLM) 초기화
  const llm = new ChatOpenAI({ modelName: "gpt-4o-mini", temperature: 0 });

  // 3. 프롬프트 생성
  // AI 어시스턴트의 역할과 응답 방식을 지정하는 시스템 메시지 템플릿
  const systemTemplate = [
    `You are an assistant for question-answering tasks. `,
    `Use the following pieces of retrieved context to answer `,
    `the question. If you don't know the answer, say that you `,
    `don't know. Use three sentences maximum and keep the `,
    `answer concise.`,
    `\n\n`,
    `{context}`,
  ].join("");

  // 시스템 메시지와 사용자 입력을 위한 템플릿을 정의
  const prompt = ChatPromptTemplate.fromMessages([
    ["system", systemTemplate],
    ["human", "{input}"],
  ]);

  // 4. 질문-답변 체인 생성
  // LLM과 프롬프트를 결합하여 검색된 문서를 처리하는 체인 생성
  const questionAnswerChain = await createStuffDocumentsChain({ llm, prompt });

  // 5. RAG 체인 생성
  // 검색기와 질문-답변 체인을 결합하여 최종적인 RAG 체인 생성
  const chain = createRetrievalChain({
    retriever,
    combineDocsChain: questionAnswerChain,
  });

  // 6. 완성된 RAG 체인 반환
  return chain;
}
```
