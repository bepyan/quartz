
```js
// DOM 요소에 액션 이벤트 속성 추가
export const addActionEventAttribute = (target, action, actionName) => {
    target.setAttribute(`data-action-${action}`, actionName);
};

// 데이터 속성을 가진 상위 요소 찾기
const getDataTarget = (container, target, data) => {
    let actionTarget = target;
    while (actionTarget && actionTarget !== container && !actionTarget.hasAttribute(data)) {
        actionTarget = actionTarget.parentElement;
    }
    return actionTarget;
};

// 이벤트 리스너 설정
export const listenActionEvent = (root, action, actions) => {
    root.addEventListener(action, (e) => {
        const target = getDataTarget(root, e.target, `data-action-${action}`);
        if (!target) return;
        
        const actionName = target.getAttribute(`data-action-${action}`);
        if (actionName in actions) {
            actions[actionName](target, e);
        }
    });
};
```
