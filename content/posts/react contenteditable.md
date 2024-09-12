---
title: react contenteditable
date: 2024-08-22
tags:
  - fruit
  - fe
---

React에서 순수하게 `contenteditable`을 사용한다면 아래 같이 코드를 작성할 수 있다.

```jsx
const Editable = () => {
  const [content, setContent] = React.useState("")
  
  const onContentBlur = (e) => {
    setContent(e.currentTarget.innerHTML)
  }
  
  return (
    <div 
      contentEditable
      onBlur={onContentBlur}
      dangerouslySetInnerHTML={{__html: content}}
	/>
  )
}
```

그냥 `innerText` 혹은 `innerHTML`을 사용한다면 React의 라이프사이클이 제대로 반영되지 않아 예상치 못한 DOM 구조로 수정될 수 있다.

그래서 React에선 [`dangerouslySetInnerHTML`](https://reactjs.org/docs/dom-elements.html?ref=blixt-dev#dangerouslysetinnerhtml)을 사용하도록 권장을 하고 있다.

속성명에 dangerously가 붙여진 만큼 여전히 예상치 못한 DOM 동작이 수행될 수 있다. 수정하다보면 DOM 깊이가 너무 깊어지는 등 이슈가 있다. 직접 이 이슈들을 대응하는 것은 리소스가 많이 들게 도니다.

이를 쉽게 다루기 위해서  [**`react-contenteditable`**](https://github.com/lovasoa/react-contenteditable?tab=readme-ov-file) 라이브러리를 활용해볼 수 있다.

[코드 내부](https://github.com/lovasoa/react-contenteditable/blob/master/src/react-contenteditable.tsx)를 살펴보면, `normalizeHtml`, `replaceCaret` 로직이 있으며 클래스 컴포넌트를 활용하여 더 정교하게 React 라이프사이클을 다루고 있다.

사용 예시는 아래와 같다.

```jsx
export default function Text({ element }: Props) {
  const text = useRef("");

  const handleChange = (e) => {
    text.current = e.target.value;
  };

  const handleBlur = () => {
    console.log(text.current);
  };

  return (
    <ContentEditable
      html={text.current}
      onBlur={handleBlur}
      onChange={handleChange}
    />
  );
}
```


`dangerouslySetInnerHTML` 설명에서도 나와 있듯이 사용자가 `innerHTML`을 다루게 될 때 반드시 XSS 공격을 예방해야 한다.

[[sanitize-html]]도 사용하여 XSS 공격을 예방할 수 있다.
초기 HTML 랜딩시, HTML을 저장시에 `sanitize`을 해주면 된다.

이를 활용한 코드는 아래와 같다.

```tsx
"use client";

import { useCallback, useRef } from "react";
import ContentEditable, {
  type ContentEditableEvent,
} from "react-contenteditable";
import sanitizeHtml from "sanitize-html";
import ElementWrapper from "~/components/editor/elements/element-wrapper";
import { useEditor } from "~/components/editor/provider";
import type { InferEditorElement } from "~/components/editor/type";

type Props = {
  element: InferEditorElement<"text">;
};

export default function Text({ element }: Props) {
  const { dispatch, editor } = useEditor();

  const sanitize = useCallback((html: string) => {
    return sanitizeHtml(html, {
      allowedTags: ["a", "p", "br", "div", "b"],
      allowedAttributes: { a: ["href"], p: ["style"] },
    });
  }, []);

  const text = useRef(sanitize(element.content.innerText));

  const handleChange = (e: ContentEditableEvent) => {
    text.current = e.target.value;
  };

  const handleBlur = () => {
    const textHtml = sanitize(text.current);
    text.current = textHtml;
    dispatch({
      type: "UPDATE_ELEMENT",
      payload: {
        elementDetails: {
          ...element,
          content: {
            innerText: textHtml,
          },
        },
      },
    });
  };

  return (
    <ElementWrapper element={element}>
      <ContentEditable
        className="w-full outline-none"
        disabled={editor.state.isPreviewMode}
        html={text.current}
        onBlur={handleBlur}
        onChange={handleChange}
      />
    </ElementWrapper>
  );
}
```

참고:
https://blixtdev.com/how-to-use-contenteditable-with-react/