---
title: VanillaJS Modal 만들기
date: 2024-10-16
tags:
  - seed
---

```js
/* eslint-disable jsdoc/require-returns */
import { setElementStyles } from '@utils/dom';

/**
 * 전체 화면을 덮는 `레이어` 입니다.
 * @param {Object} options 레이어 옵션
 * @param {string} [options.rootId='js-layer'] 레이어의 루트 요소 ID
 * @param {string} [options.zIndex='110000'] z-index 값
 * @param {string} [options.backgroundColor='rgba(0,0,0,.5)'] 배경색
 * @param {(contentEl: HTMLElement) => void} [options.mountContent] 컨텐츠를 마운트하는 함수
 * @param {(error: Error) => void} [options.onMountError] 에러 발생 시 호출될 콜백 함수
 * @param {Object} [options.contentStyle] 컨텐츠 요소에 적용할 추가 스타일
 * @example
 * import { generateLayer } from '@components/common/Layer';
 *
 * // LoadingLayer.js
 * const LoadingLayer = generateLayer({...});
 *
 * // 사용법
 * LoadingLayer.show()
 * LoadingLayer.hide()
 */
export const generateLayer = ({
    rootId = 'js-layer',
    zIndex = '110000',
    backgroundColor = 'rgba(0,0,0,.5)',
    mountContent = (contentEl) => console.log(contentEl),
    onMountError = (error) => console.error('Layer error:', error),
    contentStyle = {},
}) => {
    let isOpen = false;
    let root = null;
    let content = null;
    let hideTimer = null;
    let removeBackdropClickListener = null;

    const listenBackdropEvent = (callback) => {
        const handler = () => {
            if (typeof callback === 'function') {
                callback();
            } else {
                hide();
            }
        };

        const onClickBackdrop = (e) => {
            if (e.target === root) {
                handler();
            }
        };

        const onKeydownEsc = (e) => {
            if (e.key === 'Escape') {
                handler();
            }
        };

        root.addEventListener('click', onClickBackdrop);
        window.addEventListener('keydown', onKeydownEsc);

        removeBackdropClickListener = () => {
            root.removeEventListener('click', onClickBackdrop);
            window.removeEventListener('keydown', onKeydownEsc);
        };
    };

    const cleanupListenBackdropEvent = () => {
        removeBackdropClickListener?.();
        removeBackdropClickListener = null;
    };

    const mount = () => {
        try {
            document.querySelectorAll(`#${rootId}`).forEach((existRoot) => {
                existRoot.remove();
            });

            root = document.createElement('div');
            root.setAttribute('id', rootId);

            content = document.createElement('div');
            setElementStyles(content, {
                zIndex,
                position: 'absolute',
                top: '50%',
                left: '50%',
                transform: 'translate(-50%, -50%)',
                opacity: '0',
                transitionProperty: 'opacity',
                transitionTimingFunction: 'ease-out',
                ...contentStyle,
            });
            mountContent(content);
            root.appendChild(content);

            document.body.appendChild(root);
        } catch (error) {
            onMountError(error);
            destroy();
        }
    };

    /**
     * 다이얼로그 레이어를 표시합니다.
     * @param {Object} option 레이어 표시 옵션
     * @param {number} [option.duration=170] 애니메이션 지속 시간 (밀리초)
     * @param {boolean} [option.hasBackdrop=true] 배경 레이어를 표시할지 여부
     * @param {boolean|function} [option.onBackdropEvent=false] 배경 레이어 클릭 및 esc 입력시 수행하는 이벤트, true 시 레이어를 숨기는 액션이 수행됩니다.
     */
    const show = ({
        duration = 170,
        hasBackdrop = true,
        onBackdropEvent = false,
    } = {}) => {
        if (isOpen) {
            return;
        }

        if (!root) {
            mount();
        }

        if (hasBackdrop) {
            setElementStyles(root, {
                zIndex,
                position: 'fixed',
                top: '0',
                bottom: '0',
                left: '0',
                right: '0',
                backgroundColor: 'rgba(0,0,0,0)',
                transitionProperty: 'background-color',
                transitionDuration: `${duration}ms`,
                transitionTimingFunction: 'ease-out',
            });
        } else {
            root.removeAttribute('style');
        }

        isOpen = true;
        root.style.display = 'block';
        content.style.transitionDuration = `${duration}ms`;
        requestAnimationFrame(() => {
            root.style.backgroundColor = backgroundColor;
            content.style.opacity = '1';
        });

        cleanupListenBackdropEvent();

        if (onBackdropEvent) {
            listenBackdropEvent(onBackdropEvent);
        }
    };

    const cleanupHideTimer = () => {
        if (hideTimer) {
            clearTimeout(hideTimer);
            hideTimer = null;
        }
    };

    /**
     * 레이어를 숨깁니다.
     * @param {Object} option - 레이어 숨김 옵션
     * @param {number} [option.duration=150] - 애니메이션 지속 시간 (밀리초)
     */
    const hide = ({
        duration = 150,
    } = {}) => {
        if (!root || !isOpen) {
            return;
        }

        isOpen = false;
        cleanupListenBackdropEvent();
        cleanupHideTimer();

        requestAnimationFrame(() => {
            setElementStyles(root, {
                backgroundColor: 'rgba(0,0,0,0)',
                transitionDuration: `${duration}ms`,
            });
            setElementStyles(content, {
                opacity: '0',
                transitionDuration: `${duration}ms`,
            });
            hideTimer = setTimeout(() => {
                root.style.display = 'none';
                hideTimer = null;
            }, duration);
        });
    };

    const destroy = () => {
        if (!root) {
            return;
        }

        isOpen = false;
        cleanupListenBackdropEvent();
        cleanupHideTimer();
        root.remove();
        root = null;
        content = null;
    };

    return {
        show,
        hide,
        destroy,
    };
};
```