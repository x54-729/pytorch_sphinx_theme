# 简介
本仓库 fork 自 https://github.com/pytorch/pytorch_sphinx_theme 并进行更改来适应 `fastNLP` 的文档需求。
改动见 `CHANGELOG.md`。

## 使用方法

以主仓库 [fastNLP](https://github.com/fastnlp/fastNLP) 为例，需要切换至 `docs/` 下，然后进行本地安装：

```
pip install -e git+https://github.com/x54-729/pytorch_sphinx_theme.git#egg=pytorch_sphinx_theme
pip install sphinx_copybutton
```

然后在 `conf.py` 中添加：

```python
import pytorch_sphinx_theme

html_theme = 'pytorch_sphinx_theme'
html_theme_path = [pytorch_sphinx_theme.get_html_theme_path()]

# Ignore >>> when copying code
copybutton_prompt_text = r'>>> |\.\.\. '
copybutton_prompt_is_regexp = True
```

### 网页 logo

`fastNLP` 的 logo 为 `_static/image/fnlp-logo` ，在 `_static/css/readthedocs.css` 中添加下面的样式可以设置网页 logo（展示在网页的左上角）
```css
.header-logo {
    background-image: url("../image/fnlp-logo.png");
    background-size: 130px 40px;
    height: 40px;
    width: 130px;
}
```

还需要在 `conf.py` 中添加下面的设置：
```python
html_static_path = ['_static']
html_css_files = ['css/readthedocs.css']
```

想要改变 logo 的跳转路径可以调整 `conf.py` 中的 `html_theme_options` 的 `logo_url`。

`menu` 字段可以显示网页上方的菜单栏。目前 `fastNLP` 暂时只有 `Github` 一项；其它下拉菜单的设置方法在注释中。

```python
html_theme_options = {
    'logo_url': 'http://www.fastnlp.top/',
    'menu': [
        # A link
        {
            'name': 'GitHub',
            'url': 'https://github.com/fastnlp/fastNLP'
        }, 
        # {
        #     'name': 'Projects',
        #     'children': [
        #         # A vanilla dropdown item
        #         {
        #             'name': 'MMCV',
        #             'url': 'https://github.com/open-mmlab/mmcv',
        #         },
        #         # A dropdown item with a description
        #         {
        #             'name': 'MMDetection',
        #             'url': 'https://github.com/open-mmlab/mmdetection',
        #             'description': 'Object detection toolbox and benchmark'
        #         },
        #     ], 
        #     # Optional, determining whether this dropdown menu will always be
        #     # highlighted. 
        #     'active': True,
        # },
    ],
    # Specify the language of shared menu
    'menu_lang': 'cn',
}
```

### 模板文件

在仓库的 `pytorch_sphinx_theme/` 下面存放着多个网页模板文件：

- `breadcrumbs.html`：在各模块文档上方显示的类似 `Docs>fastNLP.core` 的一栏，展示了访问的层级
- `fonts.html`：
- `footer.html`：
- `layout.html`：整个网页的框架。在其中可以改变网页标签栏的图片
    -  `<link rel="shortcut icon" href="{{ pathto('_static/images/fnlp-title.png', 1) }}" />`
    - `pytorch_sphinx_theme/static/images/fnlp-title.png` 为网页标签栏的图片；
- `mathjax_config.html`：数学公式的设置
- `search.html`：搜索页面
- `searchbox.html`：侧边栏的搜索框
- `versions.html`：左下角的多版本切换模块
- `theme_variables.jinja`：设置不同语言下侧边栏的设置，目前为空；`OpenMMLab` 对不同产品的跳转是在这里实现的。