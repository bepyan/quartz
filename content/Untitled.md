

```
const path = require('node:path');

const isDev = process.env.NODE_ENV === 'development';

module.exports = {
    stories: ['../stories/**/*.stories.js'],
    addons: [],
    framework: '@storybook/svelte',
    core: {
        builder: '@storybook/builder-vite',
        disableTelemetry: true,
    },
    features: {
        storyStoreV7: true,
    },
    async viteFinal(config) {
        config.base = process.env.BASE_PATH || config.base;

        return {
            ...config,
            resolve: {
                alias: [
                    {
                        find: '~',
                        replacement: path.resolve(__dirname, '../src/main/webapp/WEB-INF'),
                    },
                ],
            },
        };
    },
    svelteOptions: {
        onwarn: (warning, defaultHandler) => {
            if (warning.code.includes('a11y')) return;

            defaultHandler(warning);
        },
    },
    previewHead: (head) => {
        const relativePath = isDev ? '/src/main/webapp/WEB-INF/static' : '..';

        return `
            ${head}
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/bootstrap.3.3.7.min.css">
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/bootstrap-switch.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/prism-darcula.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/jquery-ui.min.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/common.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/bootstrap-select.min.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/bootstrap-colorpicker.min.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/flatpickr.min.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/flatpickr.light.min.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/checkbox_radio_img_sprite.css" />
            <link rel="stylesheet" type="text/css" href="${relativePath}/css/Chart.css" />
            
            <script type="text/javascript" src="//t1.daumcdn.net/keditor/photos-web/dist/0.2.7/KeditorPhotosEditor.min.js"></script>
            <script type="text/javascript" src="${relativePath}/js/libraries/jquery.min-2.1.1.js"></script>
            <script type="text/javascript" src="${relativePath}/js/libraries/jquery.dataTables.min.js"></script>
            <script type="text/javascript" src="${relativePath}/js/libraries/bootstrap-switch.js"></script>
            <script type="text/javascript" src="${relativePath}/js/jquery-ui.js"></script>
            <script type="text/javascript" src="${relativePath}/js/libraries/handlebars.min-v3.0.0.js"></script>
            <script type="text/javascript" src="${relativePath}/js/bootstrap.3.3.7.min.js"></script>
            <script type="text/javascript" src="${relativePath}/js/common.js"></script>
            <script type="text/javascript" src="${relativePath}/js/admin.form.js"></script>
            <script type="text/javascript" src="${relativePath}/js/bootstrap-select.min.js"></script>
            <script type="text/javascript" src="${relativePath}/js/bootstrap-colorpicker.min.js"></script>
            <script type="text/javascript" src="${relativePath}/js/flatpickr.min.js"></script>
            <script type="text/javascript" src="${relativePath}/js/flatpickr.ko.min.js"></script>
            <script type="text/javascript" src="${relativePath}/js/Chart2.9.4.js"></script>
            <script type="text/javascript" src="${relativePath}/js/palette.js"></script>
            <script type="text/javascript" src="${relativePath}/js/admin.chart.js"></script>
        `;
    },
};

```