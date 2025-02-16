---
layout: post
title: "Predicting AFL Matches"
date: 2023-07-03
permalink: '/sideprojects/afl-prediction'
---

In this project, I create a machine learning model to predict the outcome of AFL matches.
The following has been imported from a Jupyter notebook, found [here](https://github.com/TomJDove/afl_prediction).

<html lang="en">
<head><meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>afl</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .pm { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation.Marker */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
  scrollbar-width: thin;
}

/* tiny scrollbar */

.jp-scrollbar-tiny::-webkit-scrollbar,
.jp-scrollbar-tiny::-webkit-scrollbar-corner {
  background-color: transparent;
  height: 4px;
  width: 4px;
}

.jp-scrollbar-tiny::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:horizontal {
  border-left: 0 solid transparent;
  border-right: 0 solid transparent;
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:vertical {
  border-top: 0 solid transparent;
  border-bottom: 0 solid transparent;
}

/*
 * Lumino
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
}

.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.lm-AccordionPanel[data-orientation='horizontal'] > .lm-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-CommandPalette-search {
  flex: 0 0 auto;
}

.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}

.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}

.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}

.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-close-icon {
  border: 1px solid transparent;
  background-color: transparent;
  position: absolute;
  z-index: 1;
  right: 3%;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 7px 0;
  display: none;
  vertical-align: middle;
  outline: 0;
  cursor: pointer;
}
.lm-close-icon:after {
  content: 'X';
  display: block;
  width: 15px;
  height: 15px;
  text-align: center;
  color: #000;
  font-weight: normal;
  font-size: 12px;
  cursor: pointer;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-DockPanel {
  z-index: 0;
}

.lm-DockPanel-widget {
  z-index: 0;
}

.lm-DockPanel-tabBar {
  z-index: 1;
}

.lm-DockPanel-handle {
  z-index: 2;
}

.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}

.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}

.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}

.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}

.lm-Menu-item {
  display: table-row;
}

.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}

.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}

.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}

.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

.lm-MenuBar-item {
  box-sizing: border-box;
}

.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}

.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}

.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}

.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}

.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-SplitPanel-child {
  z-index: 0;
}

.lm-SplitPanel-handle {
  z-index: 1;
}

.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
  align-items: flex-end;
}

.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
  align-items: flex-end;
}

.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}

.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}

.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}

.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
  touch-action: none; /* Disable native Drag/Drop */
}

.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}

.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

.lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
}

.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar-addButton.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}

.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}

.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

.lm-TabBar-tabLabel .lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
  background: inherit;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabPanel-tabBar {
  z-index: 1;
}

.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.jp-Collapse-header {
  padding: 1px 12px;
  background-color: var(--jp-layout-color1);
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  text-transform: uppercase;
  user-select: none;
}

.jp-Collapser-icon {
  height: 16px;
}

.jp-Collapse-header-collapsed .jp-Collapser-icon {
  transform: rotate(-90deg);
  margin: auto 0;
}

.jp-Collapser-title {
  line-height: 25px;
}

.jp-Collapse-contents {
  padding: 0 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add-above: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5MikiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik00Ljc1IDQuOTMwNjZINi42MjVWNi44MDU2NkM2LjYyNSA3LjAxMTkxIDYuNzkzNzUgNy4xODA2NiA3IDcuMTgwNjZDNy4yMDYyNSA3LjE4MDY2IDcuMzc1IDcuMDExOTEgNy4zNzUgNi44MDU2NlY0LjkzMDY2SDkuMjVDOS40NTYyNSA0LjkzMDY2IDkuNjI1IDQuNzYxOTEgOS42MjUgNC41NTU2NkM5LjYyNSA0LjM0OTQxIDkuNDU2MjUgNC4xODA2NiA5LjI1IDQuMTgwNjZINy4zNzVWMi4zMDU2NkM3LjM3NSAyLjA5OTQxIDcuMjA2MjUgMS45MzA2NiA3IDEuOTMwNjZDNi43OTM3NSAxLjkzMDY2IDYuNjI1IDIuMDk5NDEgNi42MjUgMi4zMDU2NlY0LjE4MDY2SDQuNzVDNC41NDM3NSA0LjE4MDY2IDQuMzc1IDQuMzQ5NDEgNC4zNzUgNC41NTU2NkM0LjM3NSA0Ljc2MTkxIDQuNTQzNzUgNC45MzA2NiA0Ljc1IDQuOTMwNjZaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC43Ii8+CjwvZz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgOS41VjExLjVMMi41IDExLjVWOS41TDExLjUgOS41Wk0xMiA4QzEyLjU1MjMgOCAxMyA4LjQ0NzcyIDEzIDlWMTJDMTMgMTIuNTUyMyAxMi41NTIzIDEzIDEyIDEzTDIgMTNDMS40NDc3MiAxMyAxIDEyLjU1MjMgMSAxMlY5QzEgOC40NDc3MiAxLjQ0NzcxIDggMiA4TDEyIDhaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5MiI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KC0xIDAgMCAxIDEwIDEuNTU1NjYpIi8+CjwvY2xpcFBhdGg+CjwvZGVmcz4KPC9zdmc+Cg==);
  --jp-icon-add-below: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5OCkiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik05LjI1IDEwLjA2OTNMNy4zNzUgMTAuMDY5M0w3LjM3NSA4LjE5NDM0QzcuMzc1IDcuOTg4MDkgNy4yMDYyNSA3LjgxOTM0IDcgNy44MTkzNEM2Ljc5Mzc1IDcuODE5MzQgNi42MjUgNy45ODgwOSA2LjYyNSA4LjE5NDM0TDYuNjI1IDEwLjA2OTNMNC43NSAxMC4wNjkzQzQuNTQzNzUgMTAuMDY5MyA0LjM3NSAxMC4yMzgxIDQuMzc1IDEwLjQ0NDNDNC4zNzUgMTAuNjUwNiA0LjU0Mzc1IDEwLjgxOTMgNC43NSAxMC44MTkzTDYuNjI1IDEwLjgxOTNMNi42MjUgMTIuNjk0M0M2LjYyNSAxMi45MDA2IDYuNzkzNzUgMTMuMDY5MyA3IDEzLjA2OTNDNy4yMDYyNSAxMy4wNjkzIDcuMzc1IDEyLjkwMDYgNy4zNzUgMTIuNjk0M0w3LjM3NSAxMC44MTkzTDkuMjUgMTAuODE5M0M5LjQ1NjI1IDEwLjgxOTMgOS42MjUgMTAuNjUwNiA5LjYyNSAxMC40NDQzQzkuNjI1IDEwLjIzODEgOS40NTYyNSAxMC4wNjkzIDkuMjUgMTAuMDY5M1oiIGZpbGw9IiM2MTYxNjEiIHN0cm9rZT0iIzYxNjE2MSIgc3Ryb2tlLXdpZHRoPSIwLjciLz4KPC9nPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMi41IDUuNUwyLjUgMy41TDExLjUgMy41TDExLjUgNS41TDIuNSA1LjVaTTIgN0MxLjQ0NzcyIDcgMSA2LjU1MjI4IDEgNkwxIDNDMSAyLjQ0NzcyIDEuNDQ3NzIgMiAyIDJMMTIgMkMxMi41NTIzIDIgMTMgMi40NDc3MiAxMyAzTDEzIDZDMTMgNi41NTIyOSAxMi41NTIzIDcgMTIgN0wyIDdaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5OCI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KDEgMS43NDg0NmUtMDcgMS43NDg0NmUtMDcgLTEgNCAxMy40NDQzKSIvPgo8L2NsaXBQYXRoPgo8L2RlZnM+Cjwvc3ZnPgo=);
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bell: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE2IDE2IiB2ZXJzaW9uPSIxLjEiPgogICA8cGF0aCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzMzMzMzIgogICAgICBkPSJtOCAwLjI5Yy0xLjQgMC0yLjcgMC43My0zLjYgMS44LTEuMiAxLjUtMS40IDMuNC0xLjUgNS4yLTAuMTggMi4yLTAuNDQgNC0yLjMgNS4zbDAuMjggMS4zaDVjMC4wMjYgMC42NiAwLjMyIDEuMSAwLjcxIDEuNSAwLjg0IDAuNjEgMiAwLjYxIDIuOCAwIDAuNTItMC40IDAuNi0xIDAuNzEtMS41aDVsMC4yOC0xLjNjLTEuOS0wLjk3LTIuMi0zLjMtMi4zLTUuMy0wLjEzLTEuOC0wLjI2LTMuNy0xLjUtNS4yLTAuODUtMS0yLjItMS44LTMuNi0xLjh6bTAgMS40YzAuODggMCAxLjkgMC41NSAyLjUgMS4zIDAuODggMS4xIDEuMSAyLjcgMS4yIDQuNCAwLjEzIDEuNyAwLjIzIDMuNiAxLjMgNS4yaC0xMGMxLjEtMS42IDEuMi0zLjQgMS4zLTUuMiAwLjEzLTEuNyAwLjMtMy4zIDEuMi00LjQgMC41OS0wLjcyIDEuNi0xLjMgMi41LTEuM3ptLTAuNzQgMTJoMS41Yy0wLjAwMTUgMC4yOCAwLjAxNSAwLjc5LTAuNzQgMC43OS0wLjczIDAuMDAxNi0wLjcyLTAuNTMtMC43NC0wLjc5eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-bug-dot: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiPgogICAgICAgIDxwYXRoIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMTcuMTkgOEgyMFYxMEgxNy45MUMxNy45NiAxMC4zMyAxOCAxMC42NiAxOCAxMVYxMkgyMFYxNEgxOC41SDE4VjE0LjAyNzVDMTUuNzUgMTQuMjc2MiAxNCAxNi4xODM3IDE0IDE4LjVDMTQgMTkuMjA4IDE0LjE2MzUgMTkuODc3OSAxNC40NTQ5IDIwLjQ3MzlDMTMuNzA2MyAyMC44MTE3IDEyLjg3NTcgMjEgMTIgMjFDOS43OCAyMSA3Ljg1IDE5Ljc5IDYuODEgMThINFYxNkg2LjA5QzYuMDQgMTUuNjcgNiAxNS4zNCA2IDE1VjE0SDRWMTJINlYxMUM2IDEwLjY2IDYuMDQgMTAuMzMgNi4wOSAxMEg0VjhINi44MUM3LjI2IDcuMjIgNy44OCA2LjU1IDguNjIgNi4wNEw3IDQuNDFMOC40MSAzTDEwLjU5IDUuMTdDMTEuMDQgNS4wNiAxMS41MSA1IDEyIDVDMTIuNDkgNSAxMi45NiA1LjA2IDEzLjQyIDUuMTdMMTUuNTkgM0wxNyA0LjQxTDE1LjM3IDYuMDRDMTYuMTIgNi41NSAxNi43NCA3LjIyIDE3LjE5IDhaTTEwIDE2SDE0VjE0SDEwVjE2Wk0xMCAxMkgxNFYxMEgxMFYxMloiIGZpbGw9IiM2MTYxNjEiLz4KICAgICAgICA8cGF0aCBkPSJNMjIgMTguNUMyMiAyMC40MzMgMjAuNDMzIDIyIDE4LjUgMjJDMTYuNTY3IDIyIDE1IDIwLjQzMyAxNSAxOC41QzE1IDE2LjU2NyAxNi41NjcgMTUgMTguNSAxNUMyMC40MzMgMTUgMjIgMTYuNTY3IDIyIDE4LjVaIiBmaWxsPSIjNjE2MTYxIi8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yMCA4aC0yLjgxYy0uNDUtLjc4LTEuMDctMS40NS0xLjgyLTEuOTZMMTcgNC40MSAxNS41OSAzbC0yLjE3IDIuMTdDMTIuOTYgNS4wNiAxMi40OSA1IDEyIDVjLS40OSAwLS45Ni4wNi0xLjQxLjE3TDguNDEgMyA3IDQuNDFsMS42MiAxLjYzQzcuODggNi41NSA3LjI2IDcuMjIgNi44MSA4SDR2MmgyLjA5Yy0uMDUuMzMtLjA5LjY2LS4wOSAxdjFINHYyaDJ2MWMwIC4zNC4wNC42Ny4wOSAxSDR2MmgyLjgxYzEuMDQgMS43OSAyLjk3IDMgNS4xOSAzczQuMTUtMS4yMSA1LjE5LTNIMjB2LTJoLTIuMDljLjA1LS4zMy4wOS0uNjYuMDktMXYtMWgydi0yaC0ydi0xYzAtLjM0LS4wNC0uNjctLjA5LTFIMjBWOHptLTYgOGgtNHYtMmg0djJ6bTAtNGgtNHYtMmg0djJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik05IDE2LjE3TDQuODMgMTJsLTEuNDIgMS40MUw5IDE5IDIxIDdsLTEuNDEtMS40MXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBzaGFwZS1yZW5kZXJpbmc9Imdlb21ldHJpY1ByZWNpc2lvbiI+CiAgICA8cGF0aCBkPSJNNi41OSwzLjQxTDIsOEw2LjU5LDEyLjZMOCwxMS4xOEw0LjgyLDhMOCw0LjgyTDYuNTksMy40MU0xMi40MSwzLjQxTDExLDQuODJMMTQuMTgsOEwxMSwxMS4xOEwxMi40MSwxMi42TDE3LDhMMTIuNDEsMy40MU0yMS41OSwxMS41OUwxMy41LDE5LjY4TDkuODMsMTZMOC40MiwxNy40MUwxMy41LDIyLjVMMjMsMTNMMjEuNTksMTEuNTlaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTExLjQgMTguNkw2LjggMTRMMTEuNCA5LjRMMTAgOEw0IDE0TDEwIDIwTDExLjQgMTguNlpNMTYuNiAxOC42TDIxLjIgMTRMMTYuNiA5LjRMMTggOEwyNCAxNEwxOCAyMEwxNi42IDE4LjZWMTguNloiLz4KCTwvZz4KPC9zdmc+Cg==);
  --jp-icon-collapse-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNNiAxM3YyaDh2LTJ6IiAvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1jb25zb2xlLWljb24tYmFja2dyb3VuZC1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtY29uc29sZS1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIj4KICAgIDxwYXRoIGQ9Ik0xMDUgMTI3LjNoNDB2MTIuOGgtNDB6TTUxLjEgNzdMNzQgOTkuOWwtMjMuMyAyMy4zIDEwLjUgMTAuNSAyMy4zLTIzLjNMOTUgOTkuOSA4NC41IDg5LjQgNjEuNiA2Ni41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copyright: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCI+CiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0xMS44OCw5LjE0YzEuMjgsMC4wNiwxLjYxLDEuMTUsMS42MywxLjY2aDEuNzljLTAuMDgtMS45OC0xLjQ5LTMuMTktMy40NS0zLjE5QzkuNjQsNy42MSw4LDksOCwxMi4xNCBjMCwxLjk0LDAuOTMsNC4yNCwzLjg0LDQuMjRjMi4yMiwwLDMuNDEtMS42NSwzLjQ0LTIuOTVoLTEuNzljLTAuMDMsMC41OS0wLjQ1LDEuMzgtMS42MywxLjQ0QzEwLjU1LDE0LjgzLDEwLDEzLjgxLDEwLDEyLjE0IEMxMCw5LjI1LDExLjI4LDkuMTYsMTEuODgsOS4xNHogTTEyLDJDNi40OCwyLDIsNi40OCwyLDEyczQuNDgsMTAsMTAsMTBzMTAtNC40OCwxMC0xMFMxNy41MiwyLDEyLDJ6IE0xMiwyMGMtNC40MSwwLTgtMy41OS04LTggczMuNTktOCw4LThzOCwzLjU5LDgsOFMxNi40MSwyMCwxMiwyMHoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-delete: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CiAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIiAvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjI2MjYyIiBkPSJNNiAxOWMwIDEuMS45IDIgMiAyaDhjMS4xIDAgMi0uOSAyLTJWN0g2djEyek0xOSA0aC0zLjVsLTEtMWgtNWwtMSAxSDV2MmgxNFY0eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-duplicate: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTIuNzk5OTggMC44NzVIOC44OTU4MkM5LjIwMDYxIDAuODc1IDkuNDQ5OTggMS4xMzkxNCA5LjQ0OTk4IDEuNDYxOThDOS40NDk5OCAxLjc4NDgyIDkuMjAwNjEgMi4wNDg5NiA4Ljg5NTgyIDIuMDQ4OTZIMy4zNTQxNUMzLjA0OTM2IDIuMDQ4OTYgMi43OTk5OCAyLjMxMzEgMi43OTk5OCAyLjYzNTk0VjkuNjc5NjlDMi43OTk5OCAxMC4wMDI1IDIuNTUwNjEgMTAuMjY2NyAyLjI0NTgyIDEwLjI2NjdDMS45NDEwMyAxMC4yNjY3IDEuNjkxNjUgMTAuMDAyNSAxLjY5MTY1IDkuNjc5NjlWMi4wNDg5NkMxLjY5MTY1IDEuNDAzMjggMi4xOTA0IDAuODc1IDIuNzk5OTggMC44NzVaTTUuMzY2NjUgMTEuOVY0LjU1SDExLjA4MzNWMTEuOUg1LjM2NjY1Wk00LjE0MTY1IDQuMTQxNjdDNC4xNDE2NSAzLjY5MDYzIDQuNTA3MjggMy4zMjUgNC45NTgzMiAzLjMyNUgxMS40OTE3QzExLjk0MjcgMy4zMjUgMTIuMzA4MyAzLjY5MDYzIDEyLjMwODMgNC4xNDE2N1YxMi4zMDgzQzEyLjMwODMgMTIuNzU5NCAxMS45NDI3IDEzLjEyNSAxMS40OTE3IDEzLjEyNUg0Ljk1ODMyQzQuNTA3MjggMTMuMTI1IDQuMTQxNjUgMTIuNzU5NCA0LjE0MTY1IDEyLjMwODNWNC4xNDE2N1oiIGZpbGw9IiM2MTYxNjEiLz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNOS40MzU3NCA4LjI2NTA3SDguMzY0MzFWOS4zMzY1QzguMzY0MzEgOS40NTQzNSA4LjI2Nzg4IDkuNTUwNzggOC4xNTAwMiA5LjU1MDc4QzguMDMyMTcgOS41NTA3OCA3LjkzNTc0IDkuNDU0MzUgNy45MzU3NCA5LjMzNjVWOC4yNjUwN0g2Ljg2NDMxQzYuNzQ2NDUgOC4yNjUwNyA2LjY1MDAyIDguMTY4NjQgNi42NTAwMiA4LjA1MDc4QzYuNjUwMDIgNy45MzI5MiA2Ljc0NjQ1IDcuODM2NSA2Ljg2NDMxIDcuODM2NUg3LjkzNTc0VjYuNzY1MDdDNy45MzU3NCA2LjY0NzIxIDguMDMyMTcgNi41NTA3OCA4LjE1MDAyIDYuNTUwNzhDOC4yNjc4OCA2LjU1MDc4IDguMzY0MzEgNi42NDcyMSA4LjM2NDMxIDYuNzY1MDdWNy44MzY1SDkuNDM1NzRDOS41NTM2IDcuODM2NSA5LjY1MDAyIDcuOTMyOTIgOS42NTAwMiA4LjA1MDc4QzkuNjUwMDIgOC4xNjg2NCA5LjU1MzYgOC4yNjUwNyA5LjQzNTc0IDguMjY1MDdaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC41Ii8+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-error: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjE5IiByPSIyIi8+PHBhdGggZD0iTTEwIDNoNHYxMmgtNHoiLz48L2c+CjxwYXRoIGZpbGw9Im5vbmUiIGQ9Ik0wIDBoMjR2MjRIMHoiLz4KPC9zdmc+Cg==);
  --jp-icon-expand-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNMTEgMTBIOXYzSDZ2MmgzdjNoMnYtM2gzdi0yaC0zeiIgLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-dot: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWRvdCIgZmlsbD0iI0ZGRiI+CiAgICA8Y2lyY2xlIGN4PSIxOCIgY3k9IjE3IiByPSIzIj48L2NpcmNsZT4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-filter: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-folder-favorite: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgwVjB6IiBmaWxsPSJub25lIi8+PHBhdGggY2xhc3M9ImpwLWljb24zIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxNjE2MSIgZD0iTTIwIDZoLThsLTItMkg0Yy0xLjEgMC0yIC45LTIgMnYxMmMwIDEuMS45IDIgMiAyaDE2YzEuMSAwIDItLjkgMi0yVjhjMC0xLjEtLjktMi0yLTJ6bS0yLjA2IDExTDE1IDE1LjI4IDEyLjA2IDE3bC43OC0zLjMzLTIuNTktMi4yNCAzLjQxLS4yOUwxNSA4bDEuMzQgMy4xNCAzLjQxLjI5LTIuNTkgMi4yNC43OCAzLjMzeiIvPgo8L3N2Zz4K);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-home: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPjxwYXRoIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xMCAyMHYtNmg0djZoNXYtOGgzTDEyIDMgMiAxMmgzdjh6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-info: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUwLjk3OCA1MC45NzgiPgoJPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KCQk8cGF0aCBkPSJNNDMuNTIsNy40NThDMzguNzExLDIuNjQ4LDMyLjMwNywwLDI1LjQ4OSwwQzE4LjY3LDAsMTIuMjY2LDIuNjQ4LDcuNDU4LDcuNDU4CgkJCWMtOS45NDMsOS45NDEtOS45NDMsMjYuMTE5LDAsMzYuMDYyYzQuODA5LDQuODA5LDExLjIxMiw3LjQ1NiwxOC4wMzEsNy40NThjMCwwLDAuMDAxLDAsMC4wMDIsMAoJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoKCQkJIE00Mi4xMDYsNDIuMTA1Yy00LjQzMiw0LjQzMS0xMC4zMzIsNi44NzItMTYuNjE1LDYuODcyaC0wLjAwMmMtNi4yODUtMC4wMDEtMTIuMTg3LTIuNDQxLTE2LjYxNy02Ljg3MgoJCQljLTkuMTYyLTkuMTYzLTkuMTYyLTI0LjA3MSwwLTMzLjIzM0MxMy4zMDMsNC40NCwxOS4yMDQsMiwyNS40ODksMmM2LjI4NCwwLDEyLjE4NiwyLjQ0LDE2LjYxNyw2Ljg3MgoJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4KCQk8cGF0aCBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1MwoJCQljMC40NjgtMC41MzYsMC45MjMtMS4wNjIsMS4zNjctMS41NzVjMC42MjYtMC43NTMsMS4xMDQtMS40NzgsMS40MzYtMi4xNzVjMC4zMzEtMC43MDcsMC40OTUtMS41NDEsMC40OTUtMi41CgkJCWMwLTEuMDk2LTAuMjYtMi4wODgtMC43NzktMi45NzljLTAuNTY1LTAuODc5LTEuNTAxLTEuMzM2LTIuODA2LTEuMzY5Yy0xLjgwMiwwLjA1Ny0yLjk4NSwwLjY2Ny0zLjU1LDEuODMyCgkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkKCQkJYzEuMDYyLTEuNjQsMi44NTUtMi40ODEsNS4zNzgtMi41MjdjMi4xNiwwLjAyMywzLjg3NCwwLjYwOCw1LjE0MSwxLjc1OGMxLjI3OCwxLjE2LDEuOTI5LDIuNzY0LDEuOTUsNC44MTEKCQkJYzAsMS4xNDItMC4xMzcsMi4xMTEtMC40MSwyLjkxMWMtMC4zMDksMC44NDUtMC43MzEsMS41OTMtMS4yNjgsMi4yNDNjLTAuNDkyLDAuNjUtMS4wNjgsMS4zMTgtMS43MywyLjAwMgoJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5CgkJCUMyNi41ODksMzIuMjE4LDIzLjU3OCwzMi4yMTgsMjMuNTc4LDMyLjIxOHogTTIzLjU3OCwzOC4yMnYtMy40ODRoMy4wNzZ2My40ODRIMjMuNTc4eiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaW5zcGVjdG9yLWljb24tY29sb3IganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtanNvbi1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0Y5QTgyNSI+CiAgICA8cGF0aCBkPSJNMjAuMiAxMS44Yy0xLjYgMC0xLjcuNS0xLjcgMSAwIC40LjEuOS4xIDEuMy4xLjUuMS45LjEgMS4zIDAgMS43LTEuNCAyLjMtMy41IDIuM2gtLjl2LTEuOWguNWMxLjEgMCAxLjQgMCAxLjQtLjggMC0uMyAwLS42LS4xLTEgMC0uNC0uMS0uOC0uMS0xLjIgMC0xLjMgMC0xLjggMS4zLTItMS4zLS4yLTEuMy0uNy0xLjMtMiAwLS40LjEtLjguMS0xLjIuMS0uNC4xLS43LjEtMSAwLS44LS40LS43LTEuNC0uOGgtLjVWNC4xaC45YzIuMiAwIDMuNS43IDMuNSAyLjMgMCAuNC0uMS45LS4xIDEuMy0uMS41LS4xLjktLjEgMS4zIDAgLjUuMiAxIDEuNyAxdjEuOHpNMS44IDEwLjFjMS42IDAgMS43LS41IDEuNy0xIDAtLjQtLjEtLjktLjEtMS4zLS4xLS41LS4xLS45LS4xLTEuMyAwLTEuNiAxLjQtMi4zIDMuNS0yLjNoLjl2MS45aC0uNWMtMSAwLTEuNCAwLTEuNC44IDAgLjMgMCAuNi4xIDEgMCAuMi4xLjYuMSAxIDAgMS4zIDAgMS44LTEuMyAyQzYgMTEuMiA2IDExLjcgNiAxM2MwIC40LS4xLjgtLjEgMS4yLS4xLjMtLjEuNy0uMSAxIDAgLjguMy44IDEuNC44aC41djEuOWgtLjljLTIuMSAwLTMuNS0uNi0zLjUtMi4zIDAtLjQuMS0uOS4xLTEuMy4xLS41LjEtLjkuMS0xLjMgMC0uNS0uMi0xLTEuNy0xdi0xLjl6Ii8+CiAgICA8Y2lyY2xlIGN4PSIxMSIgY3k9IjEzLjgiIHI9IjIuMSIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSI4LjIiIHI9IjIuMSIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-julia: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDMyNSAzMDAiPgogIDxnIGNsYXNzPSJqcC1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjY2IzYzMzIj4KICAgIDxwYXRoIGQ9Ik0gMTUwLjg5ODQzOCAyMjUgQyAxNTAuODk4NDM4IDI2Ni40MjE4NzUgMTE3LjMyMDMxMiAzMDAgNzUuODk4NDM4IDMwMCBDIDM0LjQ3NjU2MiAzMDAgMC44OTg0MzggMjY2LjQyMTg3NSAwLjg5ODQzOCAyMjUgQyAwLjg5ODQzOCAxODMuNTc4MTI1IDM0LjQ3NjU2MiAxNTAgNzUuODk4NDM4IDE1MCBDIDExNy4zMjAzMTIgMTUwIDE1MC44OTg0MzggMTgzLjU3ODEyNSAxNTAuODk4NDM4IDIyNSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzM4OTgyNiI+CiAgICA8cGF0aCBkPSJNIDIzNy41IDc1IEMgMjM3LjUgMTE2LjQyMTg3NSAyMDMuOTIxODc1IDE1MCAxNjIuNSAxNTAgQyAxMjEuMDc4MTI1IDE1MCA4Ny41IDExNi40MjE4NzUgODcuNSA3NSBDIDg3LjUgMzMuNTc4MTI1IDEyMS4wNzgxMjUgMCAxNjIuNSAwIEMgMjAzLjkyMTg3NSAwIDIzNy41IDMzLjU3ODEyNSAyMzcuNSA3NSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzk1NThiMiI+CiAgICA8cGF0aCBkPSJNIDMyNC4xMDE1NjIgMjI1IEMgMzI0LjEwMTU2MiAyNjYuNDIxODc1IDI5MC41MjM0MzggMzAwIDI0OS4xMDE1NjIgMzAwIEMgMjA3LjY3OTY4OCAzMDAgMTc0LjEwMTU2MiAyNjYuNDIxODc1IDE3NC4xMDE1NjIgMjI1IEMgMTc0LjEwMTU2MiAxODMuNTc4MTI1IDIwNy42Nzk2ODggMTUwIDI0OS4xMDE1NjIgMTUwIEMgMjkwLjUyMzQzOCAxNTAgMzI0LjEwMTU2MiAxODMuNTc4MTI1IDMyNC4xMDE1NjIgMjI1Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgPGcgY2xhc3M9ImpwLWp1cHl0ZXItaWNvbi1jb2xvciIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgIDxnIGNsYXNzPSJqcC1qdXB5dGVyLWljb24tY29sb3IiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launch: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMzIgMzIiIHdpZHRoPSIzMiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yNiwyOEg2YTIuMDAyNywyLjAwMjcsMCwwLDEtMi0yVjZBMi4wMDI3LDIuMDAyNywwLDAsMSw2LDRIMTZWNkg2VjI2SDI2VjE2aDJWMjZBMi4wMDI3LDIuMDAyNywwLDAsMSwyNiwyOFoiLz4KICAgIDxwb2x5Z29uIHBvaW50cz0iMjAgMiAyMCA0IDI2LjU4NiA0IDE4IDEyLjU4NiAxOS40MTQgMTQgMjggNS40MTQgMjggMTIgMzAgMTIgMzAgMiAyMCAyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4K);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-move-down: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMTIuNDcxIDcuNTI4OTlDMTIuNzYzMiA3LjIzNjg0IDEyLjc2MzIgNi43NjMxNiAxMi40NzEgNi40NzEwMVY2LjQ3MTAxQzEyLjE3OSA2LjE3OTA1IDExLjcwNTcgNi4xNzg4NCAxMS40MTM1IDYuNDcwNTRMNy43NSAxMC4xMjc1VjEuNzVDNy43NSAxLjMzNTc5IDcuNDE0MjEgMSA3IDFWMUM2LjU4NTc5IDEgNi4yNSAxLjMzNTc5IDYuMjUgMS43NVYxMC4xMjc1TDIuNTk3MjYgNi40NjgyMkMyLjMwMzM4IDYuMTczODEgMS44MjY0MSA2LjE3MzU5IDEuNTMyMjYgNi40Njc3NFY2LjQ2Nzc0QzEuMjM4MyA2Ljc2MTcgMS4yMzgzIDcuMjM4MyAxLjUzMjI2IDcuNTMyMjZMNi4yOTI4OSAxMi4yOTI5QzYuNjgzNDIgMTIuNjgzNCA3LjMxNjU4IDEyLjY4MzQgNy43MDcxMSAxMi4yOTI5TDEyLjQ3MSA3LjUyODk5WiIgZmlsbD0iIzYxNjE2MSIvPgo8L3N2Zz4K);
  --jp-icon-move-up: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMS41Mjg5OSA2LjQ3MTAxQzEuMjM2ODQgNi43NjMxNiAxLjIzNjg0IDcuMjM2ODQgMS41Mjg5OSA3LjUyODk5VjcuNTI4OTlDMS44MjA5NSA3LjgyMDk1IDIuMjk0MjYgNy44MjExNiAyLjU4NjQ5IDcuNTI5NDZMNi4yNSAzLjg3MjVWMTIuMjVDNi4yNSAxMi42NjQyIDYuNTg1NzkgMTMgNyAxM1YxM0M3LjQxNDIxIDEzIDcuNzUgMTIuNjY0MiA3Ljc1IDEyLjI1VjMuODcyNUwxMS40MDI3IDcuNTMxNzhDMTEuNjk2NiA3LjgyNjE5IDEyLjE3MzYgNy44MjY0MSAxMi40Njc3IDcuNTMyMjZWNy41MzIyNkMxMi43NjE3IDcuMjM4MyAxMi43NjE3IDYuNzYxNyAxMi40Njc3IDYuNDY3NzRMNy43MDcxMSAxLjcwNzExQzcuMzE2NTggMS4zMTY1OCA2LjY4MzQyIDEuMzE2NTggNi4yOTI4OSAxLjcwNzExTDEuNTI4OTkgNi40NzEwMVoiIGZpbGw9IiM2MTYxNjEiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtbm90ZWJvb2staWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-numbering: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTQgMTlINlYxOS41SDVWMjAuNUg2VjIxSDRWMjJIN1YxOEg0VjE5Wk01IDEwSDZWNkg0VjdINVYxMFpNNCAxM0g1LjhMNCAxNS4xVjE2SDdWMTVINS4yTDcgMTIuOVYxMkg0VjEzWk05IDdWOUgyM1Y3SDlaTTkgMjFIMjNWMTlIOVYyMVpNOSAxNUgyM1YxM0g5VjE1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-offline-bolt: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDIuMDJjLTUuNTEgMC05Ljk4IDQuNDctOS45OCA5Ljk4czQuNDcgOS45OCA5Ljk4IDkuOTggOS45OC00LjQ3IDkuOTgtOS45OFMxNy41MSAyLjAyIDEyIDIuMDJ6TTExLjQ4IDIwdi02LjI2SDhMMTMgNHY2LjI2aDMuMzVMMTEuNDggMjB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-pdf: url(data:image/svg+xml;base64,PHN2ZwogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMiIgd2lkdGg9IjE2Ij4KICAgIDxwYXRoIHRyYW5zZm9ybT0icm90YXRlKDQ1KSIgY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0ZGMkEyQSIKICAgICAgIGQ9Im0gMjIuMzQ0MzY5LC0zLjAxNjM2NDIgaCA1LjYzODYwNCB2IDEuNTc5MjQzMyBoIC0zLjU0OTIyNyB2IDEuNTA4NjkyOTkgaCAzLjMzNzU3NiBWIDEuNjUwODE1NCBoIC0zLjMzNzU3NiB2IDMuNDM1MjYxMyBoIC0yLjA4OTM3NyB6IG0gLTcuMTM2NDQ0LDEuNTc5MjQzMyB2IDQuOTQzOTU0MyBoIDAuNzQ4OTIgcSAxLjI4MDc2MSwwIDEuOTUzNzAzLC0wLjYzNDk1MzUgMC42NzgzNjksLTAuNjM0OTUzNSAwLjY3ODM2OSwtMS44NDUxNjQxIDAsLTEuMjA0NzgzNTUgLTAuNjcyOTQyLC0xLjgzNDMxMDExIC0wLjY3Mjk0MiwtMC42Mjk1MjY1OSAtMS45NTkxMywtMC42Mjk1MjY1OSB6IG0gLTIuMDg5Mzc3LC0xLjU3OTI0MzMgaCAyLjIwMzM0MyBxIDEuODQ1MTY0LDAgMi43NDYwMzksMC4yNjU5MjA3IDAuOTA2MzAxLDAuMjYwNDkzNyAxLjU1MjEwOCwwLjg5MDAyMDMgMC41Njk4MywwLjU0ODEyMjMgMC44NDY2MDUsMS4yNjQ0ODAwNiAwLjI3Njc3NCwwLjcxNjM1NzgxIDAuMjc2Nzc0LDEuNjIyNjU4OTQgMCwwLjkxNzE1NTEgLTAuMjc2Nzc0LDEuNjM4OTM5OSAtMC4yNzY3NzUsMC43MTYzNTc4IC0wLjg0NjYwNSwxLjI2NDQ4IC0wLjY1MTIzNCwwLjYyOTUyNjYgLTEuNTYyOTYyLDAuODk1NDQ3MyAtMC45MTE3MjgsMC4yNjA0OTM3IC0yLjczNTE4NSwwLjI2MDQ5MzcgaCAtMi4yMDMzNDMgeiBtIC04LjE0NTg1NjUsMCBoIDMuNDY3ODIzIHEgMS41NDY2ODE2LDAgMi4zNzE1Nzg1LDAuNjg5MjIzIDAuODMwMzI0LDAuNjgzNzk2MSAwLjgzMDMyNCwxLjk1MzcwMzE0IDAsMS4yNzUzMzM5NyAtMC44MzAzMjQsMS45NjQ1NTcwNiBRIDkuOTg3MTk2MSwyLjI3NDkxNSA4LjQ0MDUxNDUsMi4yNzQ5MTUgSCA3LjA2MjA2ODQgViA1LjA4NjA3NjcgSCA0Ljk3MjY5MTUgWiBtIDIuMDg5Mzc2OSwxLjUxNDExOTkgdiAyLjI2MzAzOTQzIGggMS4xNTU5NDEgcSAwLjYwNzgxODgsMCAwLjkzODg2MjksLTAuMjkzMDU1NDcgMC4zMzEwNDQxLC0wLjI5ODQ4MjQxIDAuMzMxMDQ0MSwtMC44NDExNzc3MiAwLC0wLjU0MjY5NTMxIC0wLjMzMTA0NDEsLTAuODM1NzUwNzQgLTAuMzMxMDQ0MSwtMC4yOTMwNTU1IC0wLjkzODg2MjksLTAuMjkzMDU1NSB6IgovPgo8L3N2Zz4K);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iLTEwIC0xMCAxMzEuMTYxMzYxNjk0MzM1OTQgMTMyLjM4ODk5OTkzODk2NDg0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzA2OTk4IiBkPSJNIDU0LjkxODc4NSw5LjE5Mjc0MjFlLTQgQyA1MC4zMzUxMzIsMC4wMjIyMTcyNyA0NS45NTc4NDYsMC40MTMxMzY5NyA0Mi4xMDYyODUsMS4wOTQ2NjkzIDMwLjc2MDA2OSwzLjA5OTE3MzEgMjguNzAwMDM2LDcuMjk0NzcxNCAyOC43MDAwMzUsMTUuMDMyMTY5IHYgMTAuMjE4NzUgaCAyNi44MTI1IHYgMy40MDYyNSBoIC0yNi44MTI1IC0xMC4wNjI1IGMgLTcuNzkyNDU5LDAgLTE0LjYxNTc1ODgsNC42ODM3MTcgLTE2Ljc0OTk5OTgsMTMuNTkzNzUgLTIuNDYxODE5OTgsMTAuMjEyOTY2IC0yLjU3MTAxNTA4LDE2LjU4NjAyMyAwLDI3LjI1IDEuOTA1OTI4Myw3LjkzNzg1MiA2LjQ1NzU0MzIsMTMuNTkzNzQ4IDE0LjI0OTk5OTgsMTMuNTkzNzUgaCA5LjIxODc1IHYgLTEyLjI1IGMgMCwtOC44NDk5MDIgNy42NTcxNDQsLTE2LjY1NjI0OCAxNi43NSwtMTYuNjU2MjUgaCAyNi43ODEyNSBjIDcuNDU0OTUxLDAgMTMuNDA2MjUzLC02LjEzODE2NCAxMy40MDYyNSwtMTMuNjI1IHYgLTI1LjUzMTI1IGMgMCwtNy4yNjYzMzg2IC02LjEyOTk4LC0xMi43MjQ3NzcxIC0xMy40MDYyNSwtMTMuOTM3NDk5NyBDIDY0LjI4MTU0OCwwLjMyNzk0Mzk3IDU5LjUwMjQzOCwtMC4wMjAzNzkwMyA1NC45MTg3ODUsOS4xOTI3NDIxZS00IFogbSAtMTQuNSw4LjIxODc1MDEyNTc5IGMgMi43Njk1NDcsMCA1LjAzMTI1LDIuMjk4NjQ1NiA1LjAzMTI1LDUuMTI0OTk5NiAtMmUtNiwyLjgxNjMzNiAtMi4yNjE3MDMsNS4wOTM3NSAtNS4wMzEyNSw1LjA5Mzc1IC0yLjc3OTQ3NiwtMWUtNiAtNS4wMzEyNSwtMi4yNzc0MTUgLTUuMDMxMjUsLTUuMDkzNzUgLTEwZS03LC0yLjgyNjM1MyAyLjI1MTc3NCwtNS4xMjQ5OTk2IDUuMDMxMjUsLTUuMTI0OTk5NiB6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2ZmZDQzYiIgZD0ibSA4NS42Mzc1MzUsMjguNjU3MTY5IHYgMTEuOTA2MjUgYyAwLDkuMjMwNzU1IC03LjgyNTg5NSwxNi45OTk5OTkgLTE2Ljc1LDE3IGggLTI2Ljc4MTI1IGMgLTcuMzM1ODMzLDAgLTEzLjQwNjI0OSw2LjI3ODQ4MyAtMTMuNDA2MjUsMTMuNjI1IHYgMjUuNTMxMjQ3IGMgMCw3LjI2NjM0NCA2LjMxODU4OCwxMS41NDAzMjQgMTMuNDA2MjUsMTMuNjI1MDA0IDguNDg3MzMxLDIuNDk1NjEgMTYuNjI2MjM3LDIuOTQ2NjMgMjYuNzgxMjUsMCA2Ljc1MDE1NSwtMS45NTQzOSAxMy40MDYyNTMsLTUuODg3NjEgMTMuNDA2MjUsLTEzLjYyNTAwNCBWIDg2LjUwMDkxOSBoIC0yNi43ODEyNSB2IC0zLjQwNjI1IGggMjYuNzgxMjUgMTMuNDA2MjU0IGMgNy43OTI0NjEsMCAxMC42OTYyNTEsLTUuNDM1NDA4IDEzLjQwNjI0MSwtMTMuNTkzNzUgMi43OTkzMywtOC4zOTg4ODYgMi42ODAyMiwtMTYuNDc1Nzc2IDAsLTI3LjI1IC0xLjkyNTc4LC03Ljc1NzQ0MSAtNS42MDM4NywtMTMuNTkzNzUgLTEzLjQwNjI0MSwtMTMuNTkzNzUgeiBtIC0xNS4wNjI1LDY0LjY1NjI1IGMgMi43Nzk0NzgsM2UtNiA1LjAzMTI1LDIuMjc3NDE3IDUuMDMxMjUsNS4wOTM3NDcgLTJlLTYsMi44MjYzNTQgLTIuMjUxNzc1LDUuMTI1MDA0IC01LjAzMTI1LDUuMTI1MDA0IC0yLjc2OTU1LDAgLTUuMDMxMjUsLTIuMjk4NjUgLTUuMDMxMjUsLTUuMTI1MDA0IDJlLTYsLTIuODE2MzMgMi4yNjE2OTcsLTUuMDkzNzQ3IDUuMDMxMjUsLTUuMDkzNzQ3IHoiLz4KPC9zdmc+Cg==);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-redo: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIi8+PHBhdGggZD0iTTE4LjQgMTAuNkMxNi41NSA4Ljk5IDE0LjE1IDggMTEuNSA4Yy00LjY1IDAtOC41OCAzLjAzLTkuOTYgNy4yMkwzLjkgMTZjMS4wNS0zLjE5IDQuMDUtNS41IDcuNi01LjUgMS45NSAwIDMuNzMuNzIgNS4xMiAxLjg4TDEzIDE2aDlWN2wtMy42IDMuNnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-share: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTSAxOCAyIEMgMTYuMzU0OTkgMiAxNSAzLjM1NDk5MDQgMTUgNSBDIDE1IDUuMTkwOTUyOSAxNS4wMjE3OTEgNS4zNzcxMjI0IDE1LjA1NjY0MSA1LjU1ODU5MzggTCA3LjkyMTg3NSA5LjcyMDcwMzEgQyA3LjM5ODUzOTkgOS4yNzc4NTM5IDYuNzMyMDc3MSA5IDYgOSBDIDQuMzU0OTkwNCA5IDMgMTAuMzU0OTkgMyAxMiBDIDMgMTMuNjQ1MDEgNC4zNTQ5OTA0IDE1IDYgMTUgQyA2LjczMjA3NzEgMTUgNy4zOTg1Mzk5IDE0LjcyMjE0NiA3LjkyMTg3NSAxNC4yNzkyOTcgTCAxNS4wNTY2NDEgMTguNDM5NDUzIEMgMTUuMDIxNTU1IDE4LjYyMTUxNCAxNSAxOC44MDgzODYgMTUgMTkgQyAxNSAyMC42NDUwMSAxNi4zNTQ5OSAyMiAxOCAyMiBDIDE5LjY0NTAxIDIyIDIxIDIwLjY0NTAxIDIxIDE5IEMgMjEgMTcuMzU0OTkgMTkuNjQ1MDEgMTYgMTggMTYgQyAxNy4yNjc0OCAxNiAxNi42MDE1OTMgMTYuMjc5MzI4IDE2LjA3ODEyNSAxNi43MjI2NTYgTCA4Ljk0MzM1OTQgMTIuNTU4NTk0IEMgOC45NzgyMDk1IDEyLjM3NzEyMiA5IDEyLjE5MDk1MyA5IDEyIEMgOSAxMS44MDkwNDcgOC45NzgyMDk1IDExLjYyMjg3OCA4Ljk0MzM1OTQgMTEuNDQxNDA2IEwgMTYuMDc4MTI1IDcuMjc5Mjk2OSBDIDE2LjYwMTQ2IDcuNzIyMTQ2MSAxNy4yNjc5MjMgOCAxOCA4IEMgMTkuNjQ1MDEgOCAyMSA2LjY0NTAwOTYgMjEgNSBDIDIxIDMuMzU0OTkwNCAxOS42NDUwMSAyIDE4IDIgeiBNIDE4IDQgQyAxOC41NjQxMjkgNCAxOSA0LjQzNTg3MDYgMTkgNSBDIDE5IDUuNTY0MTI5NCAxOC41NjQxMjkgNiAxOCA2IEMgMTcuNDM1ODcxIDYgMTcgNS41NjQxMjk0IDE3IDUgQyAxNyA0LjQzNTg3MDYgMTcuNDM1ODcxIDQgMTggNCB6IE0gNiAxMSBDIDYuNTY0MTI5NCAxMSA3IDExLjQzNTg3MSA3IDEyIEMgNyAxMi41NjQxMjkgNi41NjQxMjk0IDEzIDYgMTMgQyA1LjQzNTg3MDYgMTMgNSAxMi41NjQxMjkgNSAxMiBDIDUgMTEuNDM1ODcxIDUuNDM1ODcwNiAxMSA2IDExIHogTSAxOCAxOCBDIDE4LjU2NDEyOSAxOCAxOSAxOC40MzU4NzEgMTkgMTkgQyAxOSAxOS41NjQxMjkgMTguNTY0MTI5IDIwIDE4IDIwIEMgMTcuNDM1ODcxIDIwIDE3IDE5LjU2NDEyOSAxNyAxOSBDIDE3IDE4LjQzNTg3MSAxNy40MzU4NzEgMTggMTggMTggeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-table-rows: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMSw4SDNWNGgxOFY4eiBNMjEsMTBIM3Y0aDE4VjEweiBNMjEsMTZIM3Y0aDE4VjE2eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-tag: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjgiIGhlaWdodD0iMjgiIHZpZXdCb3g9IjAgMCA0MyAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTI4LjgzMzIgMTIuMzM0TDMyLjk5OTggMTYuNTAwN0wzNy4xNjY1IDEyLjMzNEgyOC44MzMyWiIvPgoJCTxwYXRoIGQ9Ik0xNi4yMDk1IDIxLjYxMDRDMTUuNjg3MyAyMi4xMjk5IDE0Ljg0NDMgMjIuMTI5OSAxNC4zMjQ4IDIxLjYxMDRMNi45ODI5IDE0LjcyNDVDNi41NzI0IDE0LjMzOTQgNi4wODMxMyAxMy42MDk4IDYuMDQ3ODYgMTMuMDQ4MkM1Ljk1MzQ3IDExLjUyODggNi4wMjAwMiA4LjYxOTQ0IDYuMDY2MjEgNy4wNzY5NUM2LjA4MjgxIDYuNTE0NzcgNi41NTU0OCA2LjA0MzQ3IDcuMTE4MDQgNi4wMzA1NUM5LjA4ODYzIDUuOTg0NzMgMTMuMjYzOCA1LjkzNTc5IDEzLjY1MTggNi4zMjQyNUwyMS43MzY5IDEzLjYzOUMyMi4yNTYgMTQuMTU4NSAyMS43ODUxIDE1LjQ3MjQgMjEuMjYyIDE1Ljk5NDZMMTYuMjA5NSAyMS42MTA0Wk05Ljc3NTg1IDguMjY1QzkuMzM1NTEgNy44MjU2NiA4LjYyMzUxIDcuODI1NjYgOC4xODI4IDguMjY1QzcuNzQzNDYgOC43MDU3MSA3Ljc0MzQ2IDkuNDE3MzMgOC4xODI4IDkuODU2NjdDOC42MjM4MiAxMC4yOTY0IDkuMzM1ODIgMTAuMjk2NCA5Ljc3NTg1IDkuODU2NjdDMTAuMjE1NiA5LjQxNzMzIDEwLjIxNTYgOC43MDUzMyA5Ljc3NTg1IDguMjY1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1iYWNrZ3JvdW5kLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgd2lkdGg9IjIwIiBoZWlnaHQ9IjIwIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyIDIpIiBmaWxsPSIjMzMzMzMzIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUtaW52ZXJzZSIgZD0iTTUuMDU2NjQgOC43NjE3MkM1LjA1NjY0IDguNTk3NjYgNS4wMzEyNSA4LjQ1MzEyIDQuOTgwNDcgOC4zMjgxMkM0LjkzMzU5IDguMTk5MjIgNC44NTU0NyA4LjA4MjAzIDQuNzQ2MDkgNy45NzY1NkM0LjY0MDYyIDcuODcxMDkgNC41IDcuNzc1MzkgNC4zMjQyMiA3LjY4OTQ1QzQuMTUyMzQgNy41OTk2MSAzLjk0MzM2IDcuNTExNzIgMy42OTcyNyA3LjQyNTc4QzMuMzAyNzMgNy4yODUxNiAyLjk0MzM2IDcuMTM2NzIgMi42MTkxNCA2Ljk4MDQ3QzIuMjk0OTIgNi44MjQyMiAyLjAxNzU4IDYuNjQyNTggMS43ODcxMSA2LjQzNTU1QzEuNTYwNTUgNi4yMjg1MiAxLjM4NDc3IDUuOTg4MjggMS4yNTk3NyA1LjcxNDg0QzEuMTM0NzcgNS40Mzc1IDEuMDcyMjcgNS4xMDkzOCAxLjA3MjI3IDQuNzMwNDdDMS4wNzIyNyA0LjM5ODQ0IDEuMTI4OTEgNC4wOTU3IDEuMjQyMTkgMy44MjIyN0MxLjM1NTQ3IDMuNTQ0OTIgMS41MTU2MiAzLjMwNDY5IDEuNzIyNjYgMy4xMDE1NkMxLjkyOTY5IDIuODk4NDQgMi4xNzk2OSAyLjczNDM3IDIuNDcyNjYgMi42MDkzOEMyLjc2NTYyIDIuNDg0MzggMy4wOTE4IDIuNDA0MyAzLjQ1MTE3IDIuMzY5MTRWMS4xMDkzOEg0LjM4ODY3VjIuMzgwODZDNC43NDAyMyAyLjQyNzczIDUuMDU2NjQgMi41MjM0NCA1LjMzNzg5IDIuNjY3OTdDNS42MTkxNCAyLjgxMjUgNS44NTc0MiAzLjAwMTk1IDYuMDUyNzMgMy4yMzYzM0M2LjI1MTk1IDMuNDY2OCA2LjQwNDMgMy43NDAyMyA2LjUwOTc3IDQuMDU2NjRDNi42MTkxNCA0LjM2OTE0IDYuNjczODMgNC43MjA3IDYuNjczODMgNS4xMTEzM0g1LjA0NDkyQzUuMDQ0OTIgNC42Mzg2NyA0LjkzNzUgNC4yODEyNSA0LjcyMjY2IDQuMDM5MDZDNC41MDc4MSAzLjc5Mjk3IDQuMjE2OCAzLjY2OTkyIDMuODQ5NjEgMy42Njk5MkMzLjY1MDM5IDMuNjY5OTIgMy40NzY1NiAzLjY5NzI3IDMuMzI4MTIgMy43NTE5NUMzLjE4MzU5IDMuODAyNzMgMy4wNjQ0NSAzLjg3Njk1IDIuOTcwNyAzLjk3NDYxQzIuODc2OTUgNC4wNjgzNiAyLjgwNjY0IDQuMTc5NjkgMi43NTk3NyA0LjMwODU5QzIuNzE2OCA0LjQzNzUgMi42OTUzMSA0LjU3ODEyIDIuNjk1MzEgNC43MzA0N0MyLjY5NTMxIDQuODgyODEgMi43MTY4IDUuMDE5NTMgMi43NTk3NyA1LjE0MDYyQzIuODA2NjQgNS4yNTc4MSAyLjg4MjgxIDUuMzY3MTkgMi45ODgyOCA1LjQ2ODc1QzMuMDk3NjYgNS41NzAzMSAzLjI0MDIzIDUuNjY3OTcgMy40MTYwMiA1Ljc2MTcyQzMuNTkxOCA1Ljg1MTU2IDMuODEwNTUgNS45NDMzNiA0LjA3MjI3IDYuMDM3MTFDNC40NjY4IDYuMTg1NTUgNC44MjQyMiA2LjMzOTg0IDUuMTQ0NTMgNi41QzUuNDY0ODQgNi42NTYyNSA1LjczODI4IDYuODM5ODQgNS45NjQ4NCA3LjA1MDc4QzYuMTk1MzEgNy4yNTc4MSA2LjM3MTA5IDcuNSA2LjQ5MjE5IDcuNzc3MzRDNi42MTcxOSA4LjA1MDc4IDYuNjc5NjkgOC4zNzUgNi42Nzk2OSA4Ljc1QzYuNjc5NjkgOS4wOTM3NSA2LjYyMzA1IDkuNDA0MyA2LjUwOTc3IDkuNjgxNjRDNi4zOTY0OCA5Ljk1NTA4IDYuMjM0MzggMTAuMTkxNCA2LjAyMzQ0IDEwLjM5MDZDNS44MTI1IDEwLjU4OTggNS41NTg1OSAxMC43NSA1LjI2MTcyIDEwLjg3MTFDNC45NjQ4NCAxMC45ODgzIDQuNjMyODEgMTEuMDY0NSA0LjI2NTYyIDExLjA5OTZWMTIuMjQ4SDMuMzMzOThWMTEuMDk5NkMzLjAwMTk1IDExLjA2ODQgMi42Nzk2OSAxMC45OTYxIDIuMzY3MTkgMTAuODgyOEMyLjA1NDY5IDEwLjc2NTYgMS43NzczNCAxMC41OTc3IDEuNTM1MTYgMTAuMzc4OUMxLjI5Njg4IDEwLjE2MDIgMS4xMDU0NyA5Ljg4NDc3IDAuOTYwOTM4IDkuNTUyNzNDMC44MTY0MDYgOS4yMTY4IDAuNzQ0MTQxIDguODE0NDUgMC43NDQxNDEgOC4zNDU3SDIuMzc4OTFDMi4zNzg5MSA4LjYyNjk1IDIuNDE5OTIgOC44NjMyOCAyLjUwMTk1IDkuMDU0NjlDMi41ODM5OCA5LjI0MjE5IDIuNjg5NDUgOS4zOTI1OCAyLjgxODM2IDkuNTA1ODZDMi45NTExNyA5LjYxNTIzIDMuMTAxNTYgOS42OTMzNiAzLjI2OTUzIDkuNzQwMjNDMy40Mzc1IDkuNzg3MTEgMy42MDkzOCA5LjgxMDU1IDMuNzg1MTYgOS44MTA1NUM0LjIwMzEyIDkuODEwNTUgNC41MTk1MyA5LjcxMjg5IDQuNzM0MzggOS41MTc1OEM0Ljk0OTIyIDkuMzIyMjcgNS4wNTY2NCA5LjA3MDMxIDUuMDU2NjQgOC43NjE3MlpNMTMuNDE4IDEyLjI3MTVIOC4wNzQyMlYxMUgxMy40MThWMTIuMjcxNVoiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMuOTUyNjQgNikiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo=);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtdGV4dC1lZGl0b3ItaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xNSAxNUgzdjJoMTJ2LTJ6bTAtOEgzdjJoMTJWN3pNMyAxM2gxOHYtMkgzdjJ6bTAgOGgxOHYtMkgzdjJ6TTMgM3YyaDE4VjNIM3oiLz4KPC9zdmc+Cg==);
  --jp-icon-toc: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik03LDVIMjFWN0g3VjVNNywxM1YxMUgyMVYxM0g3TTQsNC41QTEuNSwxLjUgMCAwLDEgNS41LDZBMS41LDEuNSAwIDAsMSA0LDcuNUExLjUsMS41IDAgMCwxIDIuNSw2QTEuNSwxLjUgMCAwLDEgNCw0LjVNNCwxMC41QTEuNSwxLjUgMCAwLDEgNS41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMy41QTEuNSwxLjUgMCAwLDEgMi41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMC41TTcsMTlWMTdIMjFWMTlIN000LDE2LjVBMS41LDEuNSAwIDAsMSA1LjUsMThBMS41LDEuNSAwIDAsMSA0LDE5LjVBMS41LDEuNSAwIDAsMSAyLjUsMThBMS41LDEuNSAwIDAsMSA0LDE2LjVaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tree-view: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMiAxMVYzaC03djNIOVYzSDJ2OGg3VjhoMnYxMGg0djNoN3YtOGgtN3YzaC0yVjhoMnYzeiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-user: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE2IDdhNCA0IDAgMTEtOCAwIDQgNCAwIDAxOCAwek0xMiAxNGE3IDcgMCAwMC03IDdoMTRhNyA3IDAgMDAtNy03eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-users: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAwIDM2IDI0IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogPGcgY2xhc3M9ImpwLWljb24zIiB0cmFuc2Zvcm09Im1hdHJpeCgxLjczMjcgMCAwIDEuNzMyNyAtMy42MjgyIC4wOTk1NzcpIiBmaWxsPSIjNjE2MTYxIj4KICA8cGF0aCB0cmFuc2Zvcm09Im1hdHJpeCgxLjUsMCwwLDEuNSwwLC02KSIgZD0ibTEyLjE4NiA3LjUwOThjLTEuMDUzNSAwLTEuOTc1NyAwLjU2NjUtMi40Nzg1IDEuNDEwMiAwLjc1MDYxIDAuMzEyNzcgMS4zOTc0IDAuODI2NDggMS44NzMgMS40NzI3aDMuNDg2M2MwLTEuNTkyLTEuMjg4OS0yLjg4MjgtMi44ODA5LTIuODgyOHoiLz4KICA8cGF0aCBkPSJtMjAuNDY1IDIuMzg5NWEyLjE4ODUgMi4xODg1IDAgMCAxLTIuMTg4NCAyLjE4ODUgMi4xODg1IDIuMTg4NSAwIDAgMS0yLjE4ODUtMi4xODg1IDIuMTg4NSAyLjE4ODUgMCAwIDEgMi4xODg1LTIuMTg4NSAyLjE4ODUgMi4xODg1IDAgMCAxIDIuMTg4NCAyLjE4ODV6Ii8+CiAgPHBhdGggdHJhbnNmb3JtPSJtYXRyaXgoMS41LDAsMCwxLjUsMCwtNikiIGQ9Im0zLjU4OTggOC40MjE5Yy0xLjExMjYgMC0yLjAxMzcgMC45MDExMS0yLjAxMzcgMi4wMTM3aDIuODE0NWMwLjI2Nzk3LTAuMzczMDkgMC41OTA3LTAuNzA0MzUgMC45NTg5OC0wLjk3ODUyLTAuMzQ0MzMtMC42MTY4OC0xLjAwMzEtMS4wMzUyLTEuNzU5OC0xLjAzNTJ6Ii8+CiAgPHBhdGggZD0ibTYuOTE1NCA0LjYyM2ExLjUyOTQgMS41Mjk0IDAgMCAxLTEuNTI5NCAxLjUyOTQgMS41Mjk0IDEuNTI5NCAwIDAgMS0xLjUyOTQtMS41Mjk0IDEuNTI5NCAxLjUyOTQgMCAwIDEgMS41Mjk0LTEuNTI5NCAxLjUyOTQgMS41Mjk0IDAgMCAxIDEuNTI5NCAxLjUyOTR6Ii8+CiAgPHBhdGggZD0ibTYuMTM1IDEzLjUzNWMwLTMuMjM5MiAyLjYyNTktNS44NjUgNS44NjUtNS44NjUgMy4yMzkyIDAgNS44NjUgMi42MjU5IDUuODY1IDUuODY1eiIvPgogIDxjaXJjbGUgY3g9IjEyIiBjeT0iMy43Njg1IiByPSIyLjk2ODUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-word: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KIDxnIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzQxNDE0MSI+CiAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiA8L2c+CiA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSguNDMgLjA0MDEpIiBmaWxsPSIjZmZmIj4KICA8cGF0aCBkPSJtNC4xNCA4Ljc2cTAuMDY4Mi0xLjg5IDIuNDItMS44OSAxLjE2IDAgMS42OCAwLjQyIDAuNTY3IDAuNDEgMC41NjcgMS4xNnYzLjQ3cTAgMC40NjIgMC41MTQgMC40NjIgMC4xMDMgMCAwLjItMC4wMjMxdjAuNzE0cS0wLjM5OSAwLjEwMy0wLjY1MSAwLjEwMy0wLjQ1MiAwLTAuNjkzLTAuMjItMC4yMzEtMC4yLTAuMjg0LTAuNjYyLTAuOTU2IDAuODcyLTIgMC44NzItMC45MDMgMC0xLjQ3LTAuNDcyLTAuNTI1LTAuNDcyLTAuNTI1LTEuMjYgMC0wLjI2MiAwLjA0NTItMC40NzIgMC4wNTY3LTAuMjIgMC4xMTYtMC4zNzggMC4wNjgyLTAuMTY4IDAuMjMxLTAuMzA0IDAuMTU4LTAuMTQ3IDAuMjYyLTAuMjQyIDAuMTE2LTAuMDkxNCAwLjM2OC0wLjE2OCAwLjI2Mi0wLjA5MTQgMC4zOTktMC4xMjYgMC4xMzYtMC4wNDUyIDAuNDcyLTAuMTAzIDAuMzM2LTAuMDU3OCAwLjUwNC0wLjA3OTggMC4xNTgtMC4wMjMxIDAuNTY3LTAuMDc5OCAwLjU1Ni0wLjA2ODIgMC43NzctMC4yMjEgMC4yMi0wLjE1MiAwLjIyLTAuNDQxdi0wLjI1MnEwLTAuNDMtMC4zNTctMC42NjItMC4zMzYtMC4yMzEtMC45NzYtMC4yMzEtMC42NjIgMC0wLjk5OCAwLjI2Mi0wLjMzNiAwLjI1Mi0wLjM5OSAwLjc5OHptMS44OSAzLjY4cTAuNzg4IDAgMS4yNi0wLjQxIDAuNTA0LTAuNDIgMC41MDQtMC45MDN2LTEuMDVxLTAuMjg0IDAuMTM2LTAuODYxIDAuMjMxLTAuNTY3IDAuMDkxNC0wLjk4NyAwLjE1OC0wLjQyIDAuMDY4Mi0wLjc2NiAwLjMyNi0wLjMzNiAwLjI1Mi0wLjMzNiAwLjcwNHQwLjMwNCAwLjcwNCAwLjg2MSAwLjI1MnoiIHN0cm9rZS13aWR0aD0iMS4wNSIvPgogIDxwYXRoIGQ9Im0xMCA0LjU2aDAuOTQ1djMuMTVxMC42NTEtMC45NzYgMS44OS0wLjk3NiAxLjE2IDAgMS44OSAwLjg0IDAuNjgyIDAuODQgMC42ODIgMi4zMSAwIDEuNDctMC43MDQgMi40Mi0wLjcwNCAwLjg4Mi0xLjg5IDAuODgyLTEuMjYgMC0xLjg5LTEuMDJ2MC43NjZoLTAuODV6bTIuNjIgMy4wNHEtMC43NDYgMC0xLjE2IDAuNjQtMC40NTIgMC42My0wLjQ1MiAxLjY4IDAgMS4wNSAwLjQ1MiAxLjY4dDEuMTYgMC42M3EwLjc3NyAwIDEuMjYtMC42MyAwLjQ5NC0wLjY0IDAuNDk0LTEuNjggMC0xLjA1LTAuNDcyLTEuNjgtMC40NjItMC42NC0xLjI2LTAuNjR6IiBzdHJva2Utd2lkdGg9IjEuMDUiLz4KICA8cGF0aCBkPSJtMi43MyAxNS44IDEzLjYgMC4wMDgxYzAuMDA2OSAwIDAtMi42IDAtMi42IDAtMC4wMDc4LTEuMTUgMC0xLjE1IDAtMC4wMDY5IDAtMC4wMDgzIDEuNS0wLjAwODMgMS41LTJlLTMgLTAuMDAxNC0xMS4zLTAuMDAxNC0xMS4zLTAuMDAxNGwtMC4wMDU5Mi0xLjVjMC0wLjAwNzgtMS4xNyAwLjAwMTMtMS4xNyAwLjAwMTN6IiBzdHJva2Utd2lkdGg9Ii45NzUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddAboveIcon {
  background-image: var(--jp-icon-add-above);
}

.jp-AddBelowIcon {
  background-image: var(--jp-icon-add-below);
}

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}

.jp-BellIcon {
  background-image: var(--jp-icon-bell);
}

.jp-BugDotIcon {
  background-image: var(--jp-icon-bug-dot);
}

.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}

.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}

.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}

.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}

.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}

.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}

.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}

.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}

.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}

.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}

.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}

.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}

.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}

.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}

.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}

.jp-CodeCheckIcon {
  background-image: var(--jp-icon-code-check);
}

.jp-CodeIcon {
  background-image: var(--jp-icon-code);
}

.jp-CollapseAllIcon {
  background-image: var(--jp-icon-collapse-all);
}

.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}

.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}

.jp-CopyrightIcon {
  background-image: var(--jp-icon-copyright);
}

.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}

.jp-DeleteIcon {
  background-image: var(--jp-icon-delete);
}

.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}

.jp-DuplicateIcon {
  background-image: var(--jp-icon-duplicate);
}

.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}

.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}

.jp-ErrorIcon {
  background-image: var(--jp-icon-error);
}

.jp-ExpandAllIcon {
  background-image: var(--jp-icon-expand-all);
}

.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}

.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}

.jp-FileIcon {
  background-image: var(--jp-icon-file);
}

.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}

.jp-FilterDotIcon {
  background-image: var(--jp-icon-filter-dot);
}

.jp-FilterIcon {
  background-image: var(--jp-icon-filter);
}

.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}

.jp-FolderFavoriteIcon {
  background-image: var(--jp-icon-folder-favorite);
}

.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}

.jp-HomeIcon {
  background-image: var(--jp-icon-home);
}

.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}

.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}

.jp-InfoIcon {
  background-image: var(--jp-icon-info);
}

.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}

.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}

.jp-JuliaIcon {
  background-image: var(--jp-icon-julia);
}

.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}

.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}

.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}

.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}

.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}

.jp-LaunchIcon {
  background-image: var(--jp-icon-launch);
}

.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}

.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}

.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}

.jp-ListIcon {
  background-image: var(--jp-icon-list);
}

.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}

.jp-MoveDownIcon {
  background-image: var(--jp-icon-move-down);
}

.jp-MoveUpIcon {
  background-image: var(--jp-icon-move-up);
}

.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}

.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}

.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}

.jp-NumberingIcon {
  background-image: var(--jp-icon-numbering);
}

.jp-OfflineBoltIcon {
  background-image: var(--jp-icon-offline-bolt);
}

.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}

.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}

.jp-PdfIcon {
  background-image: var(--jp-icon-pdf);
}

.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}

.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}

.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}

.jp-RedoIcon {
  background-image: var(--jp-icon-redo);
}

.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}

.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}

.jp-RunIcon {
  background-image: var(--jp-icon-run);
}

.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}

.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}

.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}

.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}

.jp-ShareIcon {
  background-image: var(--jp-icon-share);
}

.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}

.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}

.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}

.jp-TableRowsIcon {
  background-image: var(--jp-icon-table-rows);
}

.jp-TagIcon {
  background-image: var(--jp-icon-tag);
}

.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}

.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}

.jp-TocIcon {
  background-image: var(--jp-icon-toc);
}

.jp-TreeViewIcon {
  background-image: var(--jp-icon-tree-view);
}

.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}

.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}

.jp-UserIcon {
  background-image: var(--jp-icon-user);
}

.jp-UsersIcon {
  background-image: var(--jp-icon-users);
}

.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}

.jp-WordIcon {
  background-image: var(--jp-icon-word);
}

.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.lm-TabBar .lm-TabBar-addButton {
  align-items: center;
  display: flex;
  padding: 4px;
  padding-bottom: 5px;
  margin-right: 1px;
  background-color: var(--jp-layout-color2);
}

.lm-TabBar .lm-TabBar-addButton:hover {
  background-color: var(--jp-layout-color1);
}

.lm-DockPanel-tabBar .lm-TabBar-tab {
  width: var(--jp-private-horizontal-tab-width);
}

.lm-DockPanel-tabBar .lm-TabBar-content {
  flex: unset;
}

.lm-DockPanel-tabBar[data-orientation='horizontal'] {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}

/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}

.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}

.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}

.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}

.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}

.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}

.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}

.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}

.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}

/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}

.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}

.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}

.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}

.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}

.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}

.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}

/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

.jp-icon-dot[fill] {
  fill: var(--jp-warn-color0);
}

.jp-jupyter-icon-color[fill] {
  fill: var(--jp-jupyter-icon-color, var(--jp-warn-color0));
}

.jp-notebook-icon-color[fill] {
  fill: var(--jp-notebook-icon-color, var(--jp-warn-color0));
}

.jp-json-icon-color[fill] {
  fill: var(--jp-json-icon-color, var(--jp-warn-color1));
}

.jp-console-icon-color[fill] {
  fill: var(--jp-console-icon-color, white);
}

.jp-console-icon-background-color[fill] {
  fill: var(--jp-console-icon-background-color, var(--jp-brand-color1));
}

.jp-terminal-icon-color[fill] {
  fill: var(--jp-terminal-icon-color, var(--jp-layout-color2));
}

.jp-terminal-icon-background-color[fill] {
  fill: var(
    --jp-terminal-icon-background-color,
    var(--jp-inverse-layout-color2)
  );
}

.jp-text-editor-icon-color[fill] {
  fill: var(--jp-text-editor-icon-color, var(--jp-inverse-layout-color3));
}

.jp-inspector-icon-color[fill] {
  fill: var(--jp-inspector-icon-color, var(--jp-inverse-layout-color3));
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* stylelint-disable selector-max-class, selector-max-compound-selectors */

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}

.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* stylelint-enable selector-max-class, selector-max-compound-selectors */

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) .jp-icon-hoverShow-content {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FormGroup-content fieldset {
  border: none;
  padding: 0;
  min-width: 0;
  width: 100%;
}

/* stylelint-disable selector-max-type */

.jp-FormGroup-content fieldset .jp-inputFieldWrapper input,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper select,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper textarea {
  font-size: var(--jp-content-font-size2);
  border-color: var(--jp-input-border-color);
  border-style: solid;
  border-radius: var(--jp-border-radius);
  border-width: 1px;
  padding: 6px 8px;
  background: none;
  color: var(--jp-ui-font-color0);
  height: inherit;
}

.jp-FormGroup-content fieldset input[type='checkbox'] {
  position: relative;
  top: 2px;
  margin-left: 0;
}

.jp-FormGroup-content button.jp-mod-styled {
  cursor: pointer;
}

.jp-FormGroup-content .checkbox label {
  cursor: pointer;
  font-size: var(--jp-content-font-size1);
}

.jp-FormGroup-content .jp-root > fieldset > legend {
  display: none;
}

.jp-FormGroup-content .jp-root > fieldset > p {
  display: none;
}

/** copy of `input.jp-mod-styled:focus` style */
.jp-FormGroup-content fieldset input:focus,
.jp-FormGroup-content fieldset select:focus {
  -moz-outline-radius: unset;
  outline: var(--jp-border-width) solid var(--md-blue-500);
  outline-offset: -1px;
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-FormGroup-content fieldset input:hover:not(:focus),
.jp-FormGroup-content fieldset select:hover:not(:focus) {
  background-color: var(--jp-border-color2);
}

/* stylelint-enable selector-max-type */

.jp-FormGroup-content .checkbox .field-description {
  /* Disable default description field for checkbox:
   because other widgets do not have description fields,
   we add descriptions to each widget on the field level.
  */
  display: none;
}

.jp-FormGroup-content #root__description {
  display: none;
}

.jp-FormGroup-content .jp-modifiedIndicator {
  width: 5px;
  background-color: var(--jp-brand-color2);
  margin-top: 0;
  margin-left: calc(var(--jp-private-settingeditor-modifier-indent) * -1);
  flex-shrink: 0;
}

.jp-FormGroup-content .jp-modifiedIndicator.jp-errorIndicator {
  background-color: var(--jp-error-color0);
  margin-right: 0.5em;
}

/* RJSF ARRAY style */

.jp-arrayFieldWrapper legend {
  font-size: var(--jp-content-font-size2);
  color: var(--jp-ui-font-color0);
  flex-basis: 100%;
  padding: 4px 0;
  font-weight: var(--jp-content-heading-font-weight);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-arrayFieldWrapper .field-description {
  padding: 4px 0;
  white-space: pre-wrap;
}

.jp-arrayFieldWrapper .array-item {
  width: 100%;
  border: 1px solid var(--jp-border-color2);
  border-radius: 4px;
  margin: 4px;
}

.jp-ArrayOperations {
  display: flex;
  margin-left: 8px;
}

.jp-ArrayOperationsButton {
  margin: 2px;
}

.jp-ArrayOperationsButton .jp-icon3[fill] {
  fill: var(--jp-ui-font-color0);
}

button.jp-ArrayOperationsButton.jp-mod-styled:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

/* RJSF form validation error */

.jp-FormGroup-content .validationErrors {
  color: var(--jp-error-color0);
}

/* Hide panel level error as duplicated the field level error */
.jp-FormGroup-content .panel.errors {
  display: none;
}

/* RJSF normal content (settings-editor) */

.jp-FormGroup-contentNormal {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-FormGroup-contentItem {
  margin-left: 7px;
  color: var(--jp-ui-font-color0);
}

.jp-FormGroup-contentNormal .jp-FormGroup-description {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-default {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-fieldLabel {
  font-size: var(--jp-content-font-size1);
  font-weight: normal;
  min-width: 120px;
}

.jp-FormGroup-contentNormal fieldset:not(:first-child) {
  margin-left: 7px;
}

.jp-FormGroup-contentNormal .field-array-of-string .array-item {
  /* Display `jp-ArrayOperations` buttons side-by-side with content except
    for small screens where flex-wrap will place them one below the other.
  */
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-objectFieldWrapper .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

/* RJSF compact content (metadata-form) */

.jp-FormGroup-content.jp-FormGroup-contentCompact {
  width: 100%;
}

.jp-FormGroup-contentCompact .form-group {
  display: flex;
  padding: 0.5em 0.2em 0.5em 0;
}

.jp-FormGroup-contentCompact
  .jp-FormGroup-compactTitle
  .jp-FormGroup-description {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color2);
}

.jp-FormGroup-contentCompact .jp-FormGroup-fieldLabel {
  padding-bottom: 0.3em;
}

.jp-FormGroup-contentCompact .jp-inputFieldWrapper .form-control {
  width: 100%;
  box-sizing: border-box;
}

.jp-FormGroup-contentCompact .jp-arrayFieldWrapper .jp-FormGroup-compactTitle {
  padding-bottom: 7px;
}

.jp-FormGroup-contentCompact
  .jp-objectFieldWrapper
  .jp-objectFieldWrapper
  .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

.jp-FormGroup-contentCompact ul.error-detail {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
  padding-inline-start: 1em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-SidePanel {
  display: flex;
  flex-direction: column;
  min-width: var(--jp-sidebar-min-width);
  overflow-y: auto;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size1);
}

.jp-SidePanel-header {
  flex: 0 0 auto;
  display: flex;
  border-bottom: var(--jp-border-width) solid var(--jp-border-color2);
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin: 0;
  padding: 2px;
  text-transform: uppercase;
}

.jp-SidePanel-toolbar {
  flex: 0 0 auto;
}

.jp-SidePanel-content {
  flex: 1 1 auto;
}

.jp-SidePanel-toolbar,
.jp-AccordionPanel-toolbar {
  height: var(--jp-private-toolbar-height);
}

.jp-SidePanel-toolbar.jp-Toolbar-micro {
  display: none;
}

.lm-AccordionPanel .jp-AccordionPanel-title {
  box-sizing: border-box;
  line-height: 25px;
  margin: 0;
  display: flex;
  align-items: center;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  font-size: var(--jp-ui-font-size0);
}

.jp-AccordionPanel-title {
  cursor: pointer;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  text-transform: uppercase;
}

.lm-AccordionPanel[data-orientation='horizontal'] > .jp-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleLabel {
  user-select: none;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleCollapser {
  transform: rotate(-90deg);
  margin: auto 0;
  height: 16px;
}

.jp-AccordionPanel-title.lm-mod-expanded .lm-AccordionPanel-titleCollapser {
  transform: rotate(0deg);
}

.lm-AccordionPanel .jp-AccordionPanel-toolbar {
  background: none;
  box-shadow: none;
  border: none;
  margin-left: auto;
}

.lm-AccordionPanel .lm-SplitPanel-handle:hover {
  background: var(--jp-layout-color3);
}

.jp-text-truncated {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent::before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent::after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input[type='checkbox'].jp-mod-styled {
  appearance: checkbox;
  -webkit-appearance: checkbox;
  -moz-appearance: checkbox;
  height: auto;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper:not(.multiple) {
  height: 28px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select.jp-mod-styled:not([multiple]) {
  height: 32px;
}

select.jp-mod-styled[multiple] {
  max-height: 200px;
  overflow-y: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-switch {
  display: flex;
  align-items: center;
  padding-left: 4px;
  padding-right: 4px;
  font-size: var(--jp-ui-font-size1);
  background-color: transparent;
  color: var(--jp-ui-font-color1);
  border: none;
  height: 20px;
}

.jp-switch:hover {
  background-color: var(--jp-layout-color2);
}

.jp-switch-label {
  margin-right: 5px;
  font-family: var(--jp-ui-font-family);
}

.jp-switch-track {
  cursor: pointer;
  background-color: var(--jp-switch-color, var(--jp-border-color1));
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
  height: 16px;
  width: 35px;
  position: relative;
}

.jp-switch-track::before {
  content: '';
  position: absolute;
  height: 10px;
  width: 10px;
  margin: 3px;
  left: 0;
  background-color: var(--jp-ui-inverse-font-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

.jp-switch[aria-checked='true'] .jp-switch-track {
  background-color: var(--jp-switch-true-position-color, var(--jp-warn-color0));
}

.jp-switch[aria-checked='true'] .jp-switch-track::before {
  /* track width (35) - margins (3 + 3) - thumb width (10) */
  left: 19px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 8;
  overflow-x: hidden;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0;
  margin: 0;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0 6px;
  margin: 0;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent > span {
  padding: 0;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar.jp-Toolbar-micro {
  padding: 0;
  min-height: 0;
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar {
  border: none;
  box-shadow: none;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-WindowedPanel-outer {
  position: relative;
  overflow-y: auto;
}

.jp-WindowedPanel-inner {
  position: relative;
}

.jp-WindowedPanel-window {
  position: absolute;
  left: 0;
  right: 0;
  overflow: visible;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

body {
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
}

/* Disable native link decoration styles everywhere outside of dialog boxes */
a {
  text-decoration: unset;
  color: unset;
}

a:hover {
  text-decoration: unset;
  color: unset;
}

/* Accessibility for links inside dialog box text */
.jp-Dialog-content a {
  text-decoration: revert;
  color: var(--jp-content-link-color);
}

.jp-Dialog-content a:hover {
  text-decoration: revert;
}

/* Styles for ui-components */
.jp-Button {
  color: var(--jp-ui-font-color2);
  border-radius: var(--jp-border-radius);
  padding: 0 12px;
  font-size: var(--jp-ui-font-size1);

  /* Copy from blueprint 3 */
  display: inline-flex;
  flex-direction: row;
  border: none;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  text-align: left;
  vertical-align: middle;
  min-height: 30px;
  min-width: 30px;
}

.jp-Button:disabled {
  cursor: not-allowed;
}

.jp-Button:empty {
  padding: 0 !important;
}

.jp-Button.jp-mod-small {
  min-height: 24px;
  min-width: 24px;
  font-size: 12px;
  padding: 0 7px;
}

/* Use our own theme for hover styles */
.jp-Button.jp-mod-minimal:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Button.jp-mod-minimal {
  background: none;
}

.jp-InputGroup {
  display: block;
  position: relative;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border: none;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
  padding-bottom: 0;
  padding-top: 0;
  padding-left: 10px;
  padding-right: 28px;
  position: relative;
  width: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  font-weight: 400;
  height: 30px;
  line-height: 30px;
  outline: none;
  vertical-align: middle;
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input:disabled {
  cursor: not-allowed;
  resize: block;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input:disabled ~ span {
  cursor: not-allowed;
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color2);
}

.jp-InputGroupAction {
  position: absolute;
  bottom: 1px;
  right: 0;
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
  cursor: not-allowed;
  resize: block;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled ~ span {
  cursor: not-allowed;
}

/* Use our own theme for hover and option styles */
/* stylelint-disable-next-line selector-max-type */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}

select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-StatusBar-Widget {
  display: flex;
  align-items: center;
  background: var(--jp-layout-color2);
  min-height: var(--jp-statusbar-height);
  justify-content: space-between;
  padding: 0 10px;
}

.jp-StatusBar-Left {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-StatusBar-Middle {
  display: flex;
  align-items: center;
}

.jp-StatusBar-Right {
  display: flex;
  align-items: center;
  flex-direction: row-reverse;
}

.jp-StatusBar-Item {
  max-height: var(--jp-statusbar-height);
  margin: 0 2px;
  height: var(--jp-statusbar-height);
  white-space: nowrap;
  text-overflow: ellipsis;
  color: var(--jp-ui-font-color1);
  padding: 0 6px;
}

.jp-mod-highlighted:hover {
  background-color: var(--jp-layout-color3);
}

.jp-mod-clicked {
  background-color: var(--jp-brand-color1);
}

.jp-mod-clicked:hover {
  background-color: var(--jp-brand-color0);
}

.jp-mod-clicked .jp-StatusBar-TextItem {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-StatusBar-HoverItem {
  box-shadow: '0px 4px 4px rgba(0, 0, 0, 0.25)';
}

.jp-StatusBar-TextItem {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  line-height: 24px;
  color: var(--jp-ui-font-color1);
}

.jp-StatusBar-GroupItem {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-Statusbar-ProgressCircle svg {
  display: block;
  margin: 0 auto;
  width: 16px;
  height: 24px;
  align-self: normal;
}

.jp-Statusbar-ProgressCircle path {
  fill: var(--jp-inverse-layout-color3);
}

.jp-Statusbar-ProgressBar-progress-bar {
  height: 10px;
  width: 100px;
  border: solid 0.25px var(--jp-brand-color2);
  border-radius: 3px;
  overflow: hidden;
  align-self: center;
}

.jp-Statusbar-ProgressBar-progress-bar > div {
  background-color: var(--jp-brand-color2);
  background-image: linear-gradient(
    -45deg,
    rgba(255, 255, 255, 0.2) 25%,
    transparent 25%,
    transparent 50%,
    rgba(255, 255, 255, 0.2) 50%,
    rgba(255, 255, 255, 0.2) 75%,
    transparent 75%,
    transparent
  );
  background-size: 40px 40px;
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 14px;
  color: #fff;
  text-align: center;
  animation: jp-Statusbar-ExecutionTime-progress-bar 2s linear infinite;
}

.jp-Statusbar-ProgressBar-progress-bar p {
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  line-height: 10px;
  width: 100px;
}

@keyframes jp-Statusbar-ExecutionTime-progress-bar {
  0% {
    background-position: 0 0;
  }

  100% {
    background-position: 40px 40px;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Modal variant
|----------------------------------------------------------------------------*/

.jp-ModalCommandPalette {
  position: absolute;
  z-index: 10000;
  top: 38px;
  left: 30%;
  margin: 0;
  padding: 4px;
  width: 40%;
  box-shadow: var(--jp-elevation-z4);
  border-radius: 4px;
  background: var(--jp-layout-color0);
}

.jp-ModalCommandPalette .lm-CommandPalette {
  max-height: 40vh;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-close-icon::after {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-header {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-item {
  margin-left: 4px;
  margin-right: 4px;
}

.jp-ModalCommandPalette
  .lm-CommandPalette
  .lm-CommandPalette-item.lm-mod-disabled {
  display: none;
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-SearchIconGroup {
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  padding: 5px 5px 1px;
}

.jp-SearchIconGroup svg {
  height: 20px;
  width: 20px;
}

.jp-SearchIconGroup .jp-icon3[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color2);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item.lm-mod-active {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active .jp-icon-selectable[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.6;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty::after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px 24px 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
  resize: both;
}

.jp-Dialog-content.jp-Dialog-content-small {
  max-width: 500px;
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus {
  outline: 1px solid var(--jp-accept-color-normal, var(--jp-brand-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus {
  outline: 1px solid var(--jp-warn-color-normal, var(--jp-error-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline: 1px solid var(--jp-reject-color-normal, var(--md-grey-600));
}

button.jp-Dialog-close-button {
  padding: 0;
  height: 100%;
  min-width: unset;
  min-height: unset;
}

.jp-Dialog-header {
  display: flex;
  justify-content: space-between;
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-checkbox {
  padding-right: 5px;
}

.jp-Dialog-checkbox > input:focus-visible {
  outline: 1px solid var(--jp-input-active-border-color);
  outline-offset: 1px;
}

.jp-Dialog-spacer {
  flex: 1 1 auto;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Input-Boolean-Dialog {
  flex-direction: row-reverse;
  align-items: end;
  width: 100%;
}

.jp-Input-Boolean-Dialog > label {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error {
  padding: 6px;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error > pre {
  width: auto;
  padding: 10px;
  background: var(--jp-error-color3);
  border: var(--jp-border-width) solid var(--jp-error-color1);
  border-radius: var(--jp-border-radius);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  white-space: pre-wrap;
  word-wrap: break-word;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;
  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;
  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #a0f;
  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;
  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;
  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;
  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;
  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;
  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;
  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;
  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;
  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;
  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ff0;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;
  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;
  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;
  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;
  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;
  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;
  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

:root {
  /* This is the padding value to fill the gaps between lines containing spans with background color. */
  --jp-private-code-span-padding: calc(
    (var(--jp-code-line-height) - 1) * var(--jp-code-font-size) / 2
  );
}

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0;
  padding: 0;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}

.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}

.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}

.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}

.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}

.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}

.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}

.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}

.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}

.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}

.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}

.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}

.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}

.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}

.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}

.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}

.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);

  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

/* stylelint-disable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0;
}

/* stylelint-enable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  table-layout: fixed;
  margin-left: auto;
  margin-bottom: 1em;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}

[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}

.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}

.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}

.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}

.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}

.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}

.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}

.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}

.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: var(--jp-ui-font-size0);
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-cursor-backdrop {
  position: fixed;
  width: 200px;
  height: 200px;
  margin-top: -100px;
  margin-left: -100px;
  will-change: transform;
  z-index: 100;
}

.lm-mod-drag-image {
  will-change: transform;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-lineFormSearch {
  padding: 4px 12px;
  background-color: var(--jp-layout-color2);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
  font-size: var(--jp-ui-font-size1);
}

.jp-lineFormCaption {
  font-size: var(--jp-ui-font-size0);
  line-height: var(--jp-ui-font-size1);
  margin-top: 4px;
  color: var(--jp-ui-font-color0);
}

.jp-baseLineForm {
  border: none;
  border-radius: 0;
  position: absolute;
  background-size: 16px;
  background-repeat: no-repeat;
  background-position: center;
  outline: none;
}

.jp-lineFormButtonContainer {
  top: 4px;
  right: 8px;
  height: 24px;
  padding: 0 12px;
  width: 12px;
}

.jp-lineFormButtonIcon {
  top: 0;
  right: 0;
  background-color: var(--jp-brand-color1);
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  padding: 4px 6px;
}

.jp-lineFormButton {
  top: 0;
  right: 0;
  background-color: transparent;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.jp-lineFormWrapper {
  overflow: hidden;
  padding: 0 8px;
  border: 1px solid var(--jp-border-color0);
  background-color: var(--jp-input-active-background);
  height: 22px;
}

.jp-lineFormWrapperFocusWithin {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-lineFormInput {
  background: transparent;
  width: 200px;
  height: 100%;
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  line-height: 28px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/
.jp-DocumentSearch-input {
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  font-size: var(--jp-ui-font-size1);
  background-color: var(--jp-layout-color0);
  font-family: var(--jp-ui-font-family);
  padding: 2px 1px;
  resize: none;
}

.jp-DocumentSearch-overlay {
  position: absolute;
  background-color: var(--jp-toolbar-background);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  border-left: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  top: 0;
  right: 0;
  z-index: 7;
  min-width: 405px;
  padding: 2px;
  font-size: var(--jp-ui-font-size1);

  --jp-private-document-search-button-height: 20px;
}

.jp-DocumentSearch-overlay button {
  background-color: var(--jp-toolbar-background);
  outline: 0;
}

.jp-DocumentSearch-overlay button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-overlay button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-overlay-row {
  display: flex;
  align-items: center;
  margin-bottom: 2px;
}

.jp-DocumentSearch-button-content {
  display: inline-block;
  cursor: pointer;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-button-content svg {
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-input-wrapper {
  border: var(--jp-border-width) solid var(--jp-border-color0);
  display: flex;
  background-color: var(--jp-layout-color0);
  margin: 2px;
}

.jp-DocumentSearch-input-wrapper:focus-within {
  border-color: var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper {
  all: initial;
  overflow: hidden;
  display: inline-block;
  border: none;
  box-sizing: border-box;
}

.jp-DocumentSearch-toggle-wrapper {
  width: 14px;
  height: 14px;
}

.jp-DocumentSearch-button-wrapper {
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
}

.jp-DocumentSearch-toggle-wrapper:focus,
.jp-DocumentSearch-button-wrapper:focus {
  outline: var(--jp-border-width) solid
    var(--jp-cell-editor-active-border-color);
  outline-offset: -1px;
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper,
.jp-DocumentSearch-button-content:focus {
  outline: none;
}

.jp-DocumentSearch-toggle-placeholder {
  width: 5px;
}

.jp-DocumentSearch-input-button::before {
  display: block;
  padding-top: 100%;
}

.jp-DocumentSearch-input-button-off {
  opacity: var(--jp-search-toggle-off-opacity);
}

.jp-DocumentSearch-input-button-off:hover {
  opacity: var(--jp-search-toggle-hover-opacity);
}

.jp-DocumentSearch-input-button-on {
  opacity: var(--jp-search-toggle-on-opacity);
}

.jp-DocumentSearch-index-counter {
  padding-left: 10px;
  padding-right: 10px;
  user-select: none;
  min-width: 35px;
  display: inline-block;
}

.jp-DocumentSearch-up-down-wrapper {
  display: inline-block;
  padding-right: 2px;
  margin-left: auto;
  white-space: nowrap;
}

.jp-DocumentSearch-spacer {
  margin-left: auto;
}

.jp-DocumentSearch-up-down-wrapper button {
  outline: 0;
  border: none;
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
  vertical-align: middle;
  margin: 1px 5px 2px;
}

.jp-DocumentSearch-up-down-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-up-down-button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-filter-button {
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-filter-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled:hover {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-search-options {
  padding: 0 8px;
  margin-left: 3px;
  width: 100%;
  display: grid;
  justify-content: start;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  justify-items: stretch;
}

.jp-DocumentSearch-search-filter-disabled {
  color: var(--jp-ui-font-color2);
}

.jp-DocumentSearch-search-filter {
  display: flex;
  align-items: center;
  user-select: none;
}

.jp-DocumentSearch-regex-error {
  color: var(--jp-error-color0);
}

.jp-DocumentSearch-replace-button-wrapper {
  overflow: hidden;
  display: inline-block;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color0);
  margin: auto 2px;
  padding: 1px 4px;
  height: calc(var(--jp-private-document-search-button-height) + 2px);
}

.jp-DocumentSearch-replace-button-wrapper:focus {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-replace-button {
  display: inline-block;
  text-align: center;
  cursor: pointer;
  box-sizing: border-box;
  color: var(--jp-ui-font-color1);

  /* height - 2 * (padding of wrapper) */
  line-height: calc(var(--jp-private-document-search-button-height) - 2px);
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-replace-button:focus {
  outline: none;
}

.jp-DocumentSearch-replace-wrapper-class {
  margin-left: 14px;
  display: flex;
}

.jp-DocumentSearch-replace-toggle {
  border: none;
  background-color: var(--jp-toolbar-background);
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-replace-toggle:hover {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.cm-editor {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;

  /* Changed to auto to autogrow */
}

.cm-editor pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .cm-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

.jp-CodeMirrorEditor {
  cursor: text;
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.cm-editor.jp-mod-readOnly .cm-cursor {
  display: none;
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.cm-searching,
.cm-searching span {
  /* `.cm-searching span`: we need to override syntax highlighting */
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.cm-searching::selection,
.cm-searching span::selection {
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.jp-current-match > .cm-searching,
.jp-current-match > .cm-searching span,
.cm-searching > .jp-current-match,
.cm-searching > .jp-current-match span {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.jp-current-match > .cm-searching::selection,
.cm-searching > .jp-current-match::selection,
.jp-current-match > .cm-searching span::selection {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.cm-trailingspace {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAFCAYAAAB4ka1VAAAAsElEQVQIHQGlAFr/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA7+r3zKmT0/+pk9P/7+r3zAAAAAAAAAAABAAAAAAAAAAA6OPzM+/q9wAAAAAA6OPzMwAAAAAAAAAAAgAAAAAAAAAAGR8NiRQaCgAZIA0AGR8NiQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQyoYJ/SY80UAAAAASUVORK5CYII=);
  background-position: center left;
  background-repeat: repeat-x;
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/* Styles for shared cursors (remote cursor locations and selected ranges) */
.jp-CodeMirrorEditor .cm-ySelectionCaret {
  position: relative;
  border-left: 1px solid black;
  margin-left: -1px;
  margin-right: -1px;
  box-sizing: border-box;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret > .cm-ySelectionInfo {
  white-space: nowrap;
  position: absolute;
  top: -1.15em;
  padding-bottom: 0.05em;
  left: -1px;
  font-size: 0.95em;
  font-family: var(--jp-ui-font-family);
  font-weight: bold;
  line-height: normal;
  user-select: none;
  color: white;
  padding-left: 2px;
  padding-right: 2px;
  z-index: 101;
  transition: opacity 0.3s ease-in-out;
}

.jp-CodeMirrorEditor .cm-ySelectionInfo {
  transition-delay: 0.7s;
  opacity: 0;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret:hover > .cm-ySelectionInfo {
  opacity: 1;
  transition-delay: 0s;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser .jp-SidePanel-content {
  display: flex;
  flex-direction: column;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  flex-wrap: wrap;
  row-gap: 12px;
  border-bottom: none;
  height: auto;
  margin: 8px 12px 0;
  box-shadow: none;
  padding: 0;
  justify-content: flex-start;
}

.jp-FileBrowser-Panel {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 8px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0 2px;
  padding: 0 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  padding-left: 0;
  padding-right: 2px;
  align-items: center;
  height: unset;
}

.jp-FileBrowser-toolbar > .jp-Toolbar-item .jp-ToolbarButtonComponent {
  width: 40px;
}

/*-----------------------------------------------------------------------------
| Other styles
|----------------------------------------------------------------------------*/

.jp-FileDialog.jp-mod-conflict input {
  color: var(--jp-error-color1);
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

.jp-LastModified-hidden {
  display: none;
}

.jp-FileSize-hidden {
  display: none;
}

.jp-FileBrowser .lm-AccordionPanel > h3:first-child {
  display: none;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-headerItem.jp-id-filesize {
  flex: 0 0 75px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-id-narrow {
  display: none;
  flex: 0 0 5px;
  padding: 4px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
  color: var(--jp-border-color2);
}

.jp-DirListing-narrow .jp-id-narrow {
  display: block;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-content mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.jp-DirListing-content .jp-DirListing-item.jp-mod-selected mark {
  color: var(--jp-ui-inverse-font-color0);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-checkboxWrapper {
  /* Increases hit area of checkbox. */
  padding: 4px;
}

.jp-DirListing-header
  .jp-DirListing-checkboxWrapper
  + .jp-DirListing-headerItem {
  padding-left: 4px;
}

.jp-DirListing-content .jp-DirListing-checkboxWrapper {
  position: relative;
  left: -4px;
  margin: -4px 0 -4px -8px;
}

.jp-DirListing-checkboxWrapper.jp-mod-visible {
  visibility: visible;
}

/* For devices that support hovering, hide checkboxes until hovered, selected...
*/
@media (hover: hover) {
  .jp-DirListing-checkboxWrapper {
    visibility: hidden;
  }

  .jp-DirListing-item:hover .jp-DirListing-checkboxWrapper,
  .jp-DirListing-item.jp-mod-selected .jp-DirListing-checkboxWrapper {
    visibility: visible;
  }
}

.jp-DirListing-item[data-is-dot] {
  opacity: 75%;
}

.jp-DirListing-item.jp-mod-selected {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemText:focus {
  outline-width: 2px;
  outline-color: var(--jp-inverse-layout-color1);
  outline-style: solid;
  outline-offset: 1px;
}

.jp-DirListing-item.jp-mod-selected .jp-DirListing-itemText:focus {
  outline-color: var(--jp-layout-color1);
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-itemFileSize {
  flex: 0 0 90px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon::before {
  color: var(--jp-success-color1);
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.jp-mod-running.jp-mod-selected
  .jp-DirListing-itemIcon::before {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-OutputPrompt {
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-prompt {
  display: table-cell;
  vertical-align: top;
}

.jp-OutputArea-output {
  display: table-cell;
  width: 100%;
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea .jp-RenderedText {
  padding-left: 1ch;
}

/**
 * Prompt overlay.
 */

.jp-OutputArea-promptOverlay {
  position: absolute;
  top: 0;
  width: var(--jp-cell-prompt-width);
  height: 100%;
  opacity: 0.5;
}

.jp-OutputArea-promptOverlay:hover {
  background: var(--jp-layout-color2);
  box-shadow: inset 0 0 1px var(--jp-inverse-layout-color0);
  cursor: zoom-out;
}

.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay:hover {
  cursor: zoom-in;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0;
  padding: 0;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

.jp-TrimmedOutputs pre {
  background: var(--jp-layout-color3);
  font-size: calc(var(--jp-code-font-size) * 1.4);
  text-align: center;
  text-transform: uppercase;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/* Hide empty lines in the output area, for instance due to cleared widgets */
.jp-OutputArea-prompt:empty {
  padding: 0;
  border: 0;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0;
  width: 100%;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
  border-top: var(--jp-border-width) solid transparent;
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;

  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;

  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0 0.25em;
  margin: 0 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input::placeholder {
  opacity: 0;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

.jp-Stdin-input:focus::placeholder {
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

@media print {
  .jp-OutputArea-child {
    break-inside: avoid-page;
  }
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-OutputPrompt {
    display: table-row;
    text-align: left;
  }

  .jp-OutputArea-child .jp-OutputArea-output {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }
}

/* Trimmed outputs warning */
.jp-TrimmedOutputs > a {
  margin: 10px;
  text-decoration: none;
  cursor: pointer;
}

.jp-TrimmedOutputs > a:hover {
  text-decoration: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Table of Contents
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toc-active-width: 4px;
}

.jp-TableOfContents {
  display: flex;
  flex-direction: column;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  height: 100%;
}

.jp-TableOfContents-placeholder {
  text-align: center;
}

.jp-TableOfContents-placeholderContent {
  color: var(--jp-content-font-color2);
  padding: 8px;
}

.jp-TableOfContents-placeholderContent > h3 {
  margin-bottom: var(--jp-content-heading-margin-bottom);
}

.jp-TableOfContents .jp-SidePanel-content {
  overflow-y: auto;
}

.jp-TableOfContents-tree {
  margin: 4px;
}

.jp-TableOfContents ol {
  list-style-type: none;
}

/* stylelint-disable-next-line selector-max-type */
.jp-TableOfContents li > ol {
  /* Align left border with triangle icon center */
  padding-left: 11px;
}

.jp-TableOfContents-content {
  /* left margin for the active heading indicator */
  margin: 0 0 0 var(--jp-private-toc-active-width);
  padding: 0;
  background-color: var(--jp-layout-color1);
}

.jp-tocItem {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-tocItem-heading {
  display: flex;
  cursor: pointer;
}

.jp-tocItem-heading:hover {
  background-color: var(--jp-layout-color2);
}

.jp-tocItem-content {
  display: block;
  padding: 4px 0;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow-x: hidden;
}

.jp-tocItem-collapser {
  height: 20px;
  margin: 2px 2px 0;
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
}

.jp-tocItem-collapser:hover {
  background-color: var(--jp-layout-color3);
}

/* Active heading indicator */

.jp-tocItem-heading::before {
  content: ' ';
  background: transparent;
  width: var(--jp-private-toc-active-width);
  height: 24px;
  position: absolute;
  left: 0;
  border-radius: var(--jp-border-radius);
}

.jp-tocItem-heading.jp-tocItem-active::before {
  background-color: var(--jp-brand-color1);
}

.jp-tocItem-heading:hover.jp-tocItem-active::before {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;

  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0;
  bottom: 0;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Hiding collapsers in print mode.

Note: input and output wrappers have "display: block" propery in print mode.
*/

@media print {
  .jp-Collapser {
    display: none;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0;
  width: 100%;
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-InputArea-editor {
  display: table-cell;
  overflow: hidden;
  vertical-align: top;

  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  display: table-cell;
  vertical-align: top;
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-InputArea-editor {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }

  .jp-InputPrompt {
    display: table-row;
    text-align: left;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: table;
  table-layout: fixed;
  width: 100%;
}

.jp-Placeholder-prompt {
  display: table-cell;
  box-sizing: border-box;
}

.jp-Placeholder-content {
  display: table-cell;
  padding: 4px 6px;
  border: 1px solid transparent;
  border-radius: 0;
  background: none;
  box-sizing: border-box;
  cursor: pointer;
}

.jp-Placeholder-contentContainer {
  display: flex;
}

.jp-Placeholder-content:hover,
.jp-InputPlaceholder > .jp-Placeholder-content:hover {
  border-color: var(--jp-layout-color3);
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

.jp-PlaceholderText {
  white-space: nowrap;
  overflow-x: hidden;
  color: var(--jp-inverse-layout-color3);
  font-family: var(--jp-code-font-family);
}

.jp-InputPlaceholder > .jp-Placeholder-content {
  border-color: var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0;
  margin: 0;

  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 24em;
  margin-left: var(--jp-private-cell-scrolling-output-offset);
  resize: vertical;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea[style*='height'] {
  max-height: unset;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea::after {
  content: ' ';
  box-shadow: inset 0 0 6px 2px rgb(0 0 0 / 30%);
  width: 100%;
  height: 100%;
  position: sticky;
  bottom: 0;
  top: 0;
  margin-top: -50%;
  float: left;
  display: block;
  pointer-events: none;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-child {
  padding-top: 6px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  width: calc(
    var(--jp-cell-prompt-width) - var(--jp-private-cell-scrolling-output-offset)
  );
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay {
  left: calc(-1 * var(--jp-private-cell-scrolling-output-offset));
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  display: table-cell;
  width: 100%;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/* collapseHeadingButton (show always if hiddenCellsButton is _not_ shown) */
.jp-collapseHeadingButton {
  display: flex;
  min-height: var(--jp-cell-collapser-min-height);
  font-size: var(--jp-code-font-size);
  position: absolute;
  background-color: transparent;
  background-size: 25px;
  background-repeat: no-repeat;
  background-position-x: center;
  background-position-y: top;
  background-image: var(--jp-icon-caret-down);
  right: 0;
  top: 0;
  bottom: 0;
}

.jp-collapseHeadingButton.jp-mod-collapsed {
  background-image: var(--jp-icon-caret-right);
}

/*
 set the container font size to match that of content
 so that the nested collapse buttons have the right size
*/
.jp-MarkdownCell .jp-InputPrompt {
  font-size: var(--jp-content-font-size1);
}

/*
  Align collapseHeadingButton with cell top header
  The font sizes are identical to the ones in packages/rendermime/style/base.css
*/
.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='1'] {
  font-size: var(--jp-content-font-size5);
  background-position-y: calc(0.3 * var(--jp-content-font-size5));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='2'] {
  font-size: var(--jp-content-font-size4);
  background-position-y: calc(0.3 * var(--jp-content-font-size4));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='3'] {
  font-size: var(--jp-content-font-size3);
  background-position-y: calc(0.3 * var(--jp-content-font-size3));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='4'] {
  font-size: var(--jp-content-font-size2);
  background-position-y: calc(0.3 * var(--jp-content-font-size2));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='5'] {
  font-size: var(--jp-content-font-size1);
  background-position-y: top;
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='6'] {
  font-size: var(--jp-content-font-size0);
  background-position-y: top;
}

/* collapseHeadingButton (show only on (hover,active) if hiddenCellsButton is shown) */
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-collapseHeadingButton {
  display: none;
}

.jp-Notebook.jp-mod-showHiddenCellsButton
  :is(.jp-MarkdownCell:hover, .jp-mod-active)
  .jp-collapseHeadingButton {
  display: flex;
}

/* showHiddenCellsButton (only show if jp-mod-showHiddenCellsButton is set, which
is a consequence of the showHiddenCellsButton option in Notebook Settings)*/
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton {
  margin-left: calc(var(--jp-cell-prompt-width) + 2 * var(--jp-code-padding));
  margin-top: var(--jp-code-padding);
  border: 1px solid var(--jp-border-color2);
  background-color: var(--jp-border-color3) !important;
  color: var(--jp-content-font-color0) !important;
  display: flex;
}

.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton:hover {
  background-color: var(--jp-border-color2) !important;
}

.jp-showHiddenCellsButton {
  display: none;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Using block instead of flex to allow the use of the break-inside CSS property for
cell outputs.
*/

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-notebook-toolbar-padding: 2px 5px 2px 2px;
}

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: var(--jp-notebook-toolbar-padding);

  /* disable paint containment from lumino 2.0 default strict CSS containment */
  contain: style size !important;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

.jp-Toolbar-responsive-popup {
  position: absolute;
  height: fit-content;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: var(--jp-notebook-toolbar-padding);
  z-index: 1;
  right: 0;
  top: 0;
}

.jp-Toolbar > .jp-Toolbar-responsive-opener {
  margin-left: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-Notebook-ExecutionIndicator {
  position: relative;
  display: inline-block;
  height: 100%;
  z-index: 9997;
}

.jp-Notebook-ExecutionIndicator-tooltip {
  visibility: hidden;
  height: auto;
  width: max-content;
  width: -moz-max-content;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color1);
  text-align: justify;
  border-radius: 6px;
  padding: 0 5px;
  position: fixed;
  display: table;
}

.jp-Notebook-ExecutionIndicator-tooltip.up {
  transform: translateX(-50%) translateY(-100%) translateY(-32px);
}

.jp-Notebook-ExecutionIndicator-tooltip.down {
  transform: translateX(calc(-100% + 16px)) translateY(5px);
}

.jp-Notebook-ExecutionIndicator-tooltip.hidden {
  display: none;
}

.jp-Notebook-ExecutionIndicator:hover .jp-Notebook-ExecutionIndicator-tooltip {
  visibility: visible;
}

.jp-Notebook-ExecutionIndicator span {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  color: var(--jp-ui-font-color1);
  line-height: 24px;
  display: block;
}

.jp-Notebook-ExecutionIndicator-progress-bar {
  display: flex;
  justify-content: center;
  height: 100%;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*
 * Execution indicator
 */
.jp-tocItem-content::after {
  content: '';

  /* Must be identical to form a circle */
  width: 12px;
  height: 12px;
  background: none;
  border: none;
  position: absolute;
  right: 0;
}

.jp-tocItem-content[data-running='0']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background: none;
}

.jp-tocItem-content[data-running='1']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background-color: var(--jp-inverse-layout-color3);
}

.jp-tocItem-content[data-running='0'],
.jp-tocItem-content[data-running='1'] {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Notebook-footer {
  height: 27px;
  margin-left: calc(
    var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
      var(--jp-cell-padding)
  );
  width: calc(
    100% -
      (
        var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
          var(--jp-cell-padding) + var(--jp-cell-padding)
      )
  );
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  color: var(--jp-ui-font-color3);
  margin-top: 6px;
  background: none;
  cursor: pointer;
}

.jp-Notebook-footer:focus {
  border-color: var(--jp-cell-editor-active-border-color);
}

/* For devices that support hovering, hide footer until hover */
@media (hover: hover) {
  .jp-Notebook-footer {
    opacity: 0;
  }

  .jp-Notebook-footer:focus,
  .jp-Notebook-footer:hover {
    opacity: 1;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-side-by-side-output-size: 1fr;
  --jp-side-by-side-resized-cell: var(--jp-side-by-side-output-size);
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

/* stylelint-disable selector-max-class */

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-MainAreaWidget-ContainStrict .jp-Notebook * {
  contain: strict;
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* cell is dirty */
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt {
  color: var(--jp-warn-color1);
}

.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt::before {
  color: var(--jp-warn-color1);
  content: '•';
}

.jp-Notebook .jp-Cell.jp-mod-active.jp-mod-dirty .jp-Collapser {
  background: var(--jp-warn-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: block;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-ActiveCellTool {
  padding: 12px 0;
  display: flex;
}

.jp-ActiveCellTool-Content {
  flex: 1 1 auto;
}

.jp-ActiveCellTool .jp-ActiveCellTool-CellContent {
  background: var(--jp-cell-editor-background);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  min-height: 29px;
}

.jp-ActiveCellTool .jp-InputPrompt {
  min-width: calc(var(--jp-cell-prompt-width) * 0.75);
}

.jp-ActiveCellTool-CellContent > pre {
  padding: 5px 4px;
  margin: 0;
  white-space: normal;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label,
.jp-NumberSetter label {
  line-height: 1.4;
}

.jp-NotebookTools .jp-select-wrapper {
  margin-top: 4px;
  margin-bottom: 0;
}

.jp-NumberSetter input {
  width: 100%;
  margin-top: 4px;
}

.jp-NotebookTools .jp-Collapse {
  margin-top: 16px;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Side-by-side Mode (.jp-mod-sideBySide)
|----------------------------------------------------------------------------*/
.jp-mod-sideBySide.jp-Notebook .jp-Notebook-cell {
  margin-top: 3em;
  margin-bottom: 3em;
  margin-left: 5%;
  margin-right: 5%;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell {
  display: grid;
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-output-size)
    );
  grid-template-rows: auto minmax(0, 1fr) auto;
  grid-template-areas:
    'header header header'
    'input handle output'
    'footer footer footer';
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell.jp-mod-resizedCell {
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-resized-cell)
    );
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellHeader {
  grid-area: header;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-inputWrapper {
  grid-area: input;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-outputWrapper {
  /* overwrite the default margin (no vertical separation needed in side by side move */
  margin-top: 0;
  grid-area: output;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellFooter {
  grid-area: footer;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle {
  grid-area: handle;
  user-select: none;
  display: block;
  height: 100%;
  cursor: ew-resize;
  padding: 0 var(--jp-cell-padding);
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle::after {
  content: '';
  display: block;
  background: var(--jp-border-color2);
  height: 100%;
  width: 5px;
}

.jp-mod-sideBySide.jp-Notebook
  .jp-CodeCell.jp-mod-resizedCell
  .jp-CellResizeHandle::after {
  background: var(--jp-border-color0);
}

.jp-CellResizeHandle {
  display: none;
}

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Cell-Placeholder {
  padding-left: 55px;
}

.jp-Cell-Placeholder-wrapper {
  background: #fff;
  border: 1px solid;
  border-color: #e5e6e9 #dfe0e4 #d0d1d5;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  margin: 10px 15px;
}

.jp-Cell-Placeholder-wrapper-inner {
  padding: 15px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body {
  background-repeat: repeat;
  background-size: 50% auto;
}

.jp-Cell-Placeholder-wrapper-body div {
  background: #f6f7f8;
  background-image: -webkit-linear-gradient(
    left,
    #f6f7f8 0%,
    #edeef1 20%,
    #f6f7f8 40%,
    #f6f7f8 100%
  );
  background-repeat: no-repeat;
  background-size: 800px 104px;
  height: 104px;
  position: absolute;
  right: 15px;
  left: 15px;
  top: 15px;
}

div.jp-Cell-Placeholder-h1 {
  top: 20px;
  height: 20px;
  left: 15px;
  width: 150px;
}

div.jp-Cell-Placeholder-h2 {
  left: 15px;
  top: 50px;
  height: 10px;
  width: 100px;
}

div.jp-Cell-Placeholder-content-1,
div.jp-Cell-Placeholder-content-2,
div.jp-Cell-Placeholder-content-3 {
  left: 15px;
  right: 15px;
  height: 10px;
}

div.jp-Cell-Placeholder-content-1 {
  top: 100px;
}

div.jp-Cell-Placeholder-content-2 {
  top: 120px;
}

div.jp-Cell-Placeholder-content-3 {
  top: 140px;
}

</style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0 2px 1px -1px var(--jp-shadow-umbra-color),
    0 1px 1px 0 var(--jp-shadow-penumbra-color),
    0 1px 3px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0 3px 1px -2px var(--jp-shadow-umbra-color),
    0 2px 2px 0 var(--jp-shadow-penumbra-color),
    0 1px 5px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0 2px 4px -1px var(--jp-shadow-umbra-color),
    0 4px 5px 0 var(--jp-shadow-penumbra-color),
    0 1px 10px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0 3px 5px -1px var(--jp-shadow-umbra-color),
    0 6px 10px 0 var(--jp-shadow-penumbra-color),
    0 1px 18px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0 5px 5px -3px var(--jp-shadow-umbra-color),
    0 8px 10px 1px var(--jp-shadow-penumbra-color),
    0 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0 7px 8px -4px var(--jp-shadow-umbra-color),
    0 12px 17px 2px var(--jp-shadow-penumbra-color),
    0 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0 8px 10px -5px var(--jp-shadow-umbra-color),
    0 16px 24px 2px var(--jp-shadow-penumbra-color),
    0 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0 10px 13px -6px var(--jp-shadow-umbra-color),
    0 20px 31px 3px var(--jp-shadow-penumbra-color),
    0 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0 11px 15px -7px var(--jp-shadow-umbra-color),
    0 24px 38px 3px var(--jp-shadow-penumbra-color),
    0 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-inverse-border-color: var(--md-grey-600);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;
  --jp-ui-font-family: system-ui, -apple-system, blinkmacsystemfont, 'Segoe UI',
    helvetica, arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;
  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);
  --jp-content-link-color: var(--md-blue-900);
  --jp-content-font-family: system-ui, -apple-system, blinkmacsystemfont,
    'Segoe UI', helvetica, arial, sans-serif, 'Apple Color Emoji',
    'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: menlo, consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-900);
  --jp-brand-color1: var(--md-blue-700);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);
  --jp-accent-color0: var(--md-green-900);
  --jp-accent-color1: var(--md-green-700);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-900);
  --jp-warn-color1: var(--md-orange-700);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);
  --jp-error-color0: var(--md-red-900);
  --jp-error-color1: var(--md-red-700);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);
  --jp-success-color0: var(--md-green-900);
  --jp-success-color1: var(--md-green-700);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);
  --jp-info-color0: var(--md-cyan-900);
  --jp-info-color1: var(--md-cyan-700);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;
  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;
  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);
  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: var(--jp-code-font-family-default);
  --jp-cell-prompt-letter-spacing: 0;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);

  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;

  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Statusbar specific styles */

  --jp-statusbar-height: 24px;

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-inverse-border-color);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: rgb(0, 54, 109);
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #a2f;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #a2f;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /*
    RTC user specific colors.
    These colors are used for the cursor, username in the editor,
    and the icon of the user.
  */

  --jp-collaborator-color1: #ffad8e;
  --jp-collaborator-color2: #dac83d;
  --jp-collaborator-color3: #72dd76;
  --jp-collaborator-color4: #00e4d0;
  --jp-collaborator-color5: #45d4ff;
  --jp-collaborator-color6: #e2b1ff;
  --jp-collaborator-color7: #ff9de6;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 250px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);

  /* Button colors */
  --jp-accept-color-normal: var(--md-blue-700);
  --jp-accept-color-hover: var(--md-blue-800);
  --jp-accept-color-active: var(--md-blue-900);
  --jp-warn-color-normal: var(--md-red-700);
  --jp-warn-color-hover: var(--md-red-800);
  --jp-warn-color-active: var(--md-red-900);
  --jp-reject-color-normal: var(--md-grey-600);
  --jp-reject-color-hover: var(--md-grey-700);
  --jp-reject-color-active: var(--md-grey-800);

  /* File or activity icons and switch semantic variables */
  --jp-jupyter-icon-color: #f37626;
  --jp-notebook-icon-color: #f37626;
  --jp-json-icon-color: var(--md-orange-700);
  --jp-console-icon-background-color: var(--md-blue-700);
  --jp-console-icon-color: white;
  --jp-terminal-icon-background-color: var(--md-grey-800);
  --jp-terminal-icon-color: var(--md-grey-200);
  --jp-text-editor-icon-color: var(--md-grey-700);
  --jp-inspector-icon-color: var(--md-grey-700);
  --jp-switch-color: var(--md-grey-400);
  --jp-switch-true-position-color: var(--md-orange-900);
}
</style>
<style type="text/css">
/* Force rendering true colors when outputing to pdf */
* {
  -webkit-print-color-adjust: exact;
}

/* Misc */
a.anchor-link {
  display: none;
}

/* Input area styling */
.jp-InputArea {
  overflow: hidden;
}

.jp-InputArea-editor {
  overflow: hidden;
}

.cm-editor.cm-s-jupyter .highlight pre {
/* weird, but --jp-code-padding defined to be 5px but 4px horizontal padding is hardcoded for pre.cm-line */
  padding: var(--jp-code-padding) 4px;
  margin: 0;

  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  color: inherit;

}

.jp-OutputArea-output pre {
  line-height: inherit;
  font-family: inherit;
}

.jp-RenderedText pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
}

/* Hiding the collapser by default */
.jp-Collapser {
  display: none;
}

@page {
    margin: 0.5in; /* Margin for each printed piece of paper */
}

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}
</style>
<!-- Load mathjax -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-AMS_CHTML-full,Safe"> </script>
<!-- MathJax configuration -->
<script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                CommonHTML: {
                    linebreaks: {
                    automatic: true
                    }
                }
            });

            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
<!-- End of mathjax configuration --><script type="module">
  document.addEventListener("DOMContentLoaded", async () => {
    const diagrams = document.querySelectorAll(".jp-Mermaid > pre.mermaid");
    // do not load mermaidjs if not needed
    if (!diagrams.length) {
      return;
    }
    const mermaid = (await import("https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.3.1/mermaid.esm.min.mjs")).default;
    const parser = new DOMParser();

    mermaid.initialize({
      maxTextSize: 100000,
      startOnLoad: false,
      fontFamily: window
        .getComputedStyle(document.body)
        .getPropertyValue("--jp-ui-font-family"),
      theme: document.querySelector("body[data-jp-theme-light='true']")
        ? "default"
        : "dark",
    });

    let _nextMermaidId = 0;

    function makeMermaidImage(svg) {
      const img = document.createElement("img");
      const doc = parser.parseFromString(svg, "image/svg+xml");
      const svgEl = doc.querySelector("svg");
      const { maxWidth } = svgEl?.style || {};
      const firstTitle = doc.querySelector("title");
      const firstDesc = doc.querySelector("desc");

      img.setAttribute("src", `data:image/svg+xml,${encodeURIComponent(svg)}`);
      if (maxWidth) {
        img.width = parseInt(maxWidth);
      }
      if (firstTitle) {
        img.setAttribute("alt", firstTitle.textContent);
      }
      if (firstDesc) {
        const caption = document.createElement("figcaption");
        caption.className = "sr-only";
        caption.textContent = firstDesc.textContent;
        return [img, caption];
      }
      return [img];
    }

    async function makeMermaidError(text) {
      let errorMessage = "";
      try {
        await mermaid.parse(text);
      } catch (err) {
        errorMessage = `${err}`;
      }

      const result = document.createElement("details");
      result.className = 'jp-RenderedMermaid-Details';
      const summary = document.createElement("summary");
      summary.className = 'jp-RenderedMermaid-Summary';
      const pre = document.createElement("pre");
      const code = document.createElement("code");
      code.innerText = text;
      pre.appendChild(code);
      summary.appendChild(pre);
      result.appendChild(summary);

      const warning = document.createElement("pre");
      warning.innerText = errorMessage;
      result.appendChild(warning);
      return [result];
    }

    async function renderOneMarmaid(src) {
      const id = `jp-mermaid-${_nextMermaidId++}`;
      const parent = src.parentNode;
      let raw = src.textContent.trim();
      const el = document.createElement("div");
      el.style.visibility = "hidden";
      document.body.appendChild(el);
      let results = null;
      let output = null;
      try {
        const { svg } = await mermaid.render(id, raw, el);
        results = makeMermaidImage(svg);
        output = document.createElement("figure");
        results.map(output.appendChild, output);
      } catch (err) {
        parent.classList.add("jp-mod-warning");
        results = await makeMermaidError(raw);
        output = results[0];
      } finally {
        el.remove();
      }
      parent.classList.add("jp-RenderedMermaid");
      parent.appendChild(output);
    }

    void Promise.all([...diagrams].map(renderOneMarmaid));
  });
</script>
<style>
  .jp-Mermaid:not(.jp-RenderedMermaid) {
    display: none;
  }

  .jp-RenderedMermaid {
    overflow: auto;
    display: flex;
  }

  .jp-RenderedMermaid.jp-mod-warning {
    width: auto;
    padding: 0.5em;
    margin-top: 0.5em;
    border: var(--jp-border-width) solid var(--jp-warn-color2);
    border-radius: var(--jp-border-radius);
    color: var(--jp-ui-font-color1);
    font-size: var(--jp-ui-font-size1);
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  .jp-RenderedMermaid figure {
    margin: 0;
    overflow: auto;
    max-width: 100%;
  }

  .jp-RenderedMermaid img {
    max-width: 100%;
  }

  .jp-RenderedMermaid-Details > pre {
    margin-top: 1em;
  }

  .jp-RenderedMermaid-Summary {
    color: var(--jp-warn-color2);
  }

  .jp-RenderedMermaid:not(.jp-mod-warning) pre {
    display: none;
  }

  .jp-RenderedMermaid-Summary > pre {
    display: inline-block;
    white-space: normal;
  }
</style>
<!-- End of mermaid configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="AFL-Match-Prediction">AFL Match Prediction<a class="anchor-link" href="#AFL-Match-Prediction">¶</a></h1><h2 id="Introduction">Introduction<a class="anchor-link" href="#Introduction">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>The Australian Football League (AFL) is one of the most watched and betted on sporting leagues in Australia.
In this project, we train a machine learning model to predict the outcome of an AFL game using data from 2000 to the current day.</p>
<p>We try several models: random forest classifier, logistic regression, state vector machines, and neural networks.</p>
<p>Based on our data and the chosen extracted features, logistic regression was found to be the best predictor.
When evaluated on the test set, containing matches from 2019 and later, this classifer had an accuracy of 65.77%.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Obtaining-Data">Obtaining Data<a class="anchor-link" href="#Obtaining-Data">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>First we will use the PyAFL package to extract data on AFL matches.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [2]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [13]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">pyAFL.seasons.models</span> <span class="kn">import</span> <span class="n">Season</span>

<span class="k">def</span> <span class="nf">getAFLData</span><span class="p">(</span><span class="n">startYear</span> <span class="o">=</span> <span class="mi">2000</span><span class="p">,</span> <span class="n">endYear</span> <span class="o">=</span> <span class="mi">2022</span><span class="p">):</span>
       <span class="n">season_dfs</span> <span class="o">=</span> <span class="p">[]</span>
       <span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Date'</span><span class="p">,</span> <span class="s1">'Round'</span><span class="p">,</span> <span class="s1">'Home team'</span><span class="p">,</span> <span class="s1">'Away Team'</span><span class="p">,</span><span class="s1">'Home team score'</span><span class="p">,</span> <span class="s1">'Away team score'</span><span class="p">]</span>
       <span class="n">newColumns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Date'</span><span class="p">,</span> <span class="s1">'Round'</span><span class="p">,</span> <span class="s1">'Home Team'</span><span class="p">,</span> <span class="s1">'Away Team'</span><span class="p">,</span> <span class="s1">'Home Score'</span><span class="p">,</span> <span class="s1">'Away Score'</span><span class="p">]</span>

       <span class="k">for</span> <span class="n">year</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">startYear</span><span class="p">,</span> <span class="n">endYear</span><span class="o">+</span><span class="mi">1</span><span class="p">):</span>
              <span class="n">stats</span> <span class="o">=</span> <span class="n">Season</span><span class="p">(</span><span class="n">year</span><span class="p">)</span><span class="o">.</span><span class="n">get_season_stats</span><span class="p">()</span><span class="o">.</span><span class="n">match_summary</span>
              <span class="n">season_dfs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">stats</span><span class="p">[</span><span class="n">columns</span><span class="p">])</span>

       <span class="n">match_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">(</span><span class="n">season_dfs</span><span class="p">)</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">columns</span><span class="p">,</span> <span class="n">newColumns</span><span class="p">)))</span>

       <span class="c1"># Add a column which says whether the home or away team won (or a draw)</span>
       <span class="n">match_df</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">]</span> <span class="o">=</span> <span class="s2">"Home"</span>
       <span class="n">match_df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">match_df</span><span class="p">[</span><span class="s2">"Home Score"</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">match_df</span><span class="p">[</span><span class="s2">"Away Score"</span><span class="p">],</span> <span class="s2">"Winner"</span><span class="p">]</span> <span class="o">=</span> <span class="s2">"Away"</span>
       <span class="n">match_df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">match_df</span><span class="p">[</span><span class="s2">"Home Score"</span><span class="p">]</span> <span class="o">==</span> <span class="n">match_df</span><span class="p">[</span><span class="s2">"Away Score"</span><span class="p">],</span> <span class="s2">"Winner"</span><span class="p">]</span> <span class="o">=</span> <span class="s2">"Draw"</span>

       <span class="c1"># Add a column that says the year (season)</span>
       <span class="n">match_df</span><span class="p">[</span><span class="s1">'Season'</span><span class="p">]</span> <span class="o">=</span> <span class="n">match_df</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">year</span>
       
       <span class="c1"># In some entries, North Melbourne is labelled as 'Kangaroos'</span>
       <span class="n">match_df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Home Team'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'Kangaroos'</span><span class="p">,</span> <span class="s1">'Home Team'</span><span class="p">]</span> <span class="o">=</span> <span class="s1">'North Melbourne'</span>
       <span class="n">match_df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Away Team'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'Kangaroos'</span><span class="p">,</span> <span class="s1">'Away Team'</span><span class="p">]</span> <span class="o">=</span> <span class="s1">'North Melbourne'</span>

       <span class="k">return</span> <span class="n">match_df</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>The following is function to calculate some basic features which we will use in our machine learning model.
The features we calculate are as follows (each statistic is calculated for both the home and away team):</p>
<ul>
<li>The number of points scored by and against the team in the current season.</li>
<li>The average number of points scored by and against the team in the last n games, with n ranging from 1 to 5.</li>
<li>The performance of the team in the current season. Performance is calculated as follows: 2 points is given for a win, 1 point for a draw, and zero points for a loss.</li>
<li>The average performance of the team in the last n games, with n ranging from 1 to 5.</li>
<li>The position of the team in a ranking of all the teams based on their performance this season.</li>
</ul>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [14]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">processMatchData</span><span class="p">(</span><span class="n">match_df</span><span class="p">):</span>

    <span class="c1"># Create new dataframe 'teams_df', containing the match data for individual teams.</span>
    <span class="c1"># Start by getting the home teams.</span>
    <span class="n">homeCols</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"Date"</span><span class="p">,</span> <span class="s1">'Season'</span><span class="p">,</span> <span class="s1">'Round'</span><span class="p">,</span> <span class="s2">"Home Team"</span><span class="p">,</span> <span class="s2">"Home Score"</span><span class="p">,</span> <span class="s2">"Away Score"</span><span class="p">]</span>
    <span class="n">colNames</span> <span class="o">=</span> <span class="p">{</span><span class="s2">"Home Team"</span><span class="p">:</span><span class="s2">"Team"</span><span class="p">,</span> <span class="s2">"Home Score"</span><span class="p">:</span><span class="s2">"Points By"</span><span class="p">,</span> <span class="s2">"Away Score"</span><span class="p">:</span><span class="s2">"Points Against"</span><span class="p">}</span>
    <span class="n">home_df</span> <span class="o">=</span> <span class="n">match_df</span><span class="p">[</span><span class="n">homeCols</span><span class="p">]</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="n">colNames</span><span class="p">)</span>
    <span class="n">home_df</span><span class="p">[</span><span class="s2">"Home/Away"</span><span class="p">]</span> <span class="o">=</span> <span class="s2">"Home"</span>
    <span class="n">home_df</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">]</span> <span class="o">=</span> <span class="n">match_df</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">]</span>

    <span class="c1"># Now get the away teams and add it to the dataframe</span>
    <span class="n">awayCols</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"Date"</span><span class="p">,</span> <span class="s1">'Season'</span><span class="p">,</span> <span class="s1">'Round'</span><span class="p">,</span> <span class="s2">"Away Team"</span><span class="p">,</span> <span class="s2">"Away Score"</span><span class="p">,</span> <span class="s2">"Home Score"</span><span class="p">]</span>
    <span class="n">colNames</span> <span class="o">=</span> <span class="p">{</span><span class="s2">"Away Team"</span><span class="p">:</span><span class="s2">"Team"</span><span class="p">,</span> <span class="s2">"Away Score"</span><span class="p">:</span><span class="s2">"Points By"</span><span class="p">,</span> <span class="s2">"Home Score"</span><span class="p">:</span><span class="s2">"Points Against"</span><span class="p">}</span>
    <span class="n">away_df</span> <span class="o">=</span> <span class="n">match_df</span><span class="p">[</span><span class="n">awayCols</span><span class="p">]</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="n">colNames</span><span class="p">)</span>
    <span class="n">away_df</span><span class="p">[</span><span class="s2">"Home/Away"</span><span class="p">]</span> <span class="o">=</span> <span class="s2">"Away"</span>
    <span class="n">away_df</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">]</span> <span class="o">=</span> <span class="n">match_df</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">]</span>

    <span class="c1"># Join home and away teams together and sort by date</span>
    <span class="n">teams_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">home_df</span><span class="p">,</span> <span class="n">away_df</span><span class="p">])</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span> <span class="o">=</span> <span class="s2">"Date"</span><span class="p">,</span> <span class="n">ignore_index</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

    <span class="c1"># Add a column which gives the performance score for the team's game</span>
    <span class="c1"># Two points for a win, one for a draw, and none for a loss</span>
    <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Performance'</span><span class="p">]</span> <span class="o">=</span> <span class="mi">2</span><span class="o">*</span><span class="p">(</span><span class="n">teams_df</span><span class="p">[</span><span class="s1">'Home/Away'</span><span class="p">]</span> <span class="o">==</span> <span class="n">teams_df</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">])</span> <span class="o">+</span> <span class="p">(</span><span class="n">teams_df</span><span class="p">[</span><span class="s1">'Home/Away'</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Draw"</span><span class="p">)</span>

    <span class="c1"># Calculate the statistics, starting with the ones that are based on the current season.</span>
    <span class="n">seasons</span> <span class="o">=</span> <span class="n">teams_df</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'Team'</span><span class="p">,</span> <span class="s1">'Season'</span><span class="p">])</span>
    <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Season Points By'</span><span class="p">]</span> <span class="o">=</span> <span class="n">seasons</span><span class="p">[</span><span class="s1">'Points By'</span><span class="p">]</span><span class="o">.</span><span class="n">cumsum</span><span class="p">()</span> <span class="o">-</span> <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Points By'</span><span class="p">]</span>
    <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Season Points Against'</span><span class="p">]</span> <span class="o">=</span> <span class="n">seasons</span><span class="p">[</span><span class="s1">'Points Against'</span><span class="p">]</span><span class="o">.</span><span class="n">cumsum</span><span class="p">()</span> <span class="o">-</span> <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Points Against'</span><span class="p">]</span>  
    <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Season Performance'</span><span class="p">]</span> <span class="o">=</span> <span class="n">seasons</span><span class="p">[</span><span class="s1">'Performance'</span><span class="p">]</span><span class="o">.</span><span class="n">cumsum</span><span class="p">()</span> <span class="o">-</span> <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Performance'</span><span class="p">]</span>

    <span class="c1"># Relative ranking of team by performance in season (higher rank means better performance).</span>
    <span class="n">roundGroups</span> <span class="o">=</span> <span class="n">teams_df</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'Season'</span><span class="p">,</span> <span class="s1">'Round'</span><span class="p">])</span>
    <span class="n">teams_df</span><span class="p">[</span><span class="s1">'Ranking'</span><span class="p">]</span> <span class="o">=</span> <span class="n">roundGroups</span><span class="p">[</span><span class="s1">'Season Performance'</span><span class="p">]</span><span class="o">.</span><span class="n">rank</span><span class="p">(</span><span class="s2">"dense"</span><span class="p">)</span>

    <span class="c1"># Now the stats that only depend on the team</span>
    <span class="n">teamGroups</span> <span class="o">=</span> <span class="n">teams_df</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'Team'</span><span class="p">])</span>

    <span class="c1"># Average points by, points against, and performance for a team in the last n=1...5 games</span>
    <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">6</span><span class="p">):</span>
        <span class="n">teams_df</span><span class="p">[(</span><span class="s1">'Points By Last '</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">n</span><span class="p">))]</span> <span class="o">=</span> <span class="n">teamGroups</span><span class="p">[</span><span class="s1">'Points By'</span><span class="p">]</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="o">.</span><span class="n">rolling</span><span class="p">(</span><span class="n">n</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">shift</span><span class="p">())</span>
        <span class="n">teams_df</span><span class="p">[(</span><span class="s1">'Points Against Last '</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">n</span><span class="p">))]</span> <span class="o">=</span> <span class="n">teamGroups</span><span class="p">[</span><span class="s1">'Points Against'</span><span class="p">]</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="o">.</span><span class="n">rolling</span><span class="p">(</span><span class="n">n</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">shift</span><span class="p">())</span>
        <span class="n">teams_df</span><span class="p">[(</span><span class="s1">'Performance Last '</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">n</span><span class="p">))]</span> <span class="o">=</span> <span class="n">teamGroups</span><span class="p">[</span><span class="s1">'Performance'</span><span class="p">]</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="o">.</span><span class="n">rolling</span><span class="p">(</span><span class="n">n</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">shift</span><span class="p">())</span>

    <span class="c1"># Put the data back together so that each row corresponds to a game with a home and away team</span>
    <span class="c1"># Start by separating home and away teams and adding 'Home' or 'Away' prefix to column names</span>
    <span class="n">teams_df</span> <span class="o">=</span> <span class="n">teams_df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Points Against'</span><span class="p">,</span> <span class="s1">'Performance'</span><span class="p">])</span>
    <span class="n">unchangedCols</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Season'</span><span class="p">,</span> <span class="s1">'Date'</span><span class="p">,</span> <span class="s1">'Round'</span><span class="p">,</span> <span class="s1">'Winner'</span><span class="p">,</span> <span class="s1">'Home/Away'</span><span class="p">]</span>
    <span class="n">oldColNames</span> <span class="o">=</span> <span class="p">[</span><span class="n">name</span> <span class="k">for</span> <span class="n">name</span> <span class="ow">in</span> <span class="n">teams_df</span><span class="o">.</span><span class="n">columns</span> <span class="k">if</span> <span class="n">name</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">unchangedCols</span><span class="p">]</span>

    <span class="n">homeStats</span> <span class="o">=</span> <span class="n">teams_df</span><span class="p">[</span><span class="n">teams_df</span><span class="p">[</span><span class="s1">'Home/Away'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'Home'</span><span class="p">]</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Home/Away'</span><span class="p">])</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
    <span class="n">homeStats</span> <span class="o">=</span> <span class="n">homeStats</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">oldColNames</span><span class="p">,</span> <span class="p">[</span><span class="s1">'Home '</span> <span class="o">+</span> <span class="n">name</span> <span class="k">for</span> <span class="n">name</span> <span class="ow">in</span> <span class="n">oldColNames</span><span class="p">])))</span>
    <span class="n">awayStats</span> <span class="o">=</span> <span class="n">teams_df</span><span class="p">[</span><span class="n">teams_df</span><span class="p">[</span><span class="s1">'Home/Away'</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'Away'</span><span class="p">]</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="n">unchangedCols</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
    <span class="n">awayStats</span> <span class="o">=</span> <span class="n">awayStats</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">oldColNames</span><span class="p">,</span> <span class="p">[</span><span class="s1">'Away '</span> <span class="o">+</span> <span class="n">name</span> <span class="k">for</span> <span class="n">name</span> <span class="ow">in</span> <span class="n">oldColNames</span><span class="p">])))</span>

    <span class="n">matchStats</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">homeStats</span><span class="p">,</span> <span class="n">awayStats</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
    
    <span class="k">return</span> <span class="n">matchStats</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [55]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Obtain and process the AFL match data</span>
<span class="n">match_df</span> <span class="o">=</span> <span class="n">getAFLData</span><span class="p">()</span>
<span class="n">afl_df</span> <span class="o">=</span> <span class="n">processMatchData</span><span class="p">(</span><span class="n">match_df</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [56]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Save the data frames</span>
<span class="n">match_df</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">'afl_matches.csv'</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">afl_df</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">'afl_stats.csv'</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>To get data from csv files instead of re-calculating:</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [61]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">match_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'afl_matches.csv'</span><span class="p">,</span> <span class="n">parse_dates</span><span class="o">=</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">])</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [64]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'afl_stats.csv'</span><span class="p">,</span> <span class="n">parse_dates</span><span class="o">=</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">])</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Some notes on these features:</p>
<ul>
<li>All of these features can be calculated before a game is played and therefore can be used to predict the outcome of a given match.</li>
<li>One could get much more granular with the features, for example by considering the number of specific goals and behinds, hte number of possessions, etc. It would be worth considering such features and doing a more detailed exploration of possible features to see whether they result in more accurate models. For now, we keep it simple.</li>
<li>To reduce the number of features, one could use the difference between the home and away team statistics. We did try this in a parallel analysis but found that it lead to poorer results, so we haven't included this in the discussion.</li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Data-exploration">Data exploration<a class="anchor-link" href="#Data-exploration">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [54]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_df</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[54]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(4463, 46)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [41]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[41]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Date</th>
<th>Season</th>
<th>Round</th>
<th>Home Team</th>
<th>Home Points By</th>
<th>Winner</th>
<th>Home Season Points By</th>
<th>Home Season Points Against</th>
<th>Home Season Performance</th>
<th>Home Ranking</th>
<th>...</th>
<th>Away Performance Last 2</th>
<th>Away Points By Last 3</th>
<th>Away Points Against Last 3</th>
<th>Away Performance Last 3</th>
<th>Away Points By Last 4</th>
<th>Away Points Against Last 4</th>
<th>Away Performance Last 4</th>
<th>Away Points By Last 5</th>
<th>Away Points Against Last 5</th>
<th>Away Performance Last 5</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>2000-03-08 18:40:00</td>
<td>2000</td>
<td>1</td>
<td>Richmond</td>
<td>94</td>
<td>Home</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1.0</td>
<td>...</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>1</th>
<td>2000-03-09 19:15:00</td>
<td>2000</td>
<td>1</td>
<td>Essendon</td>
<td>156</td>
<td>Home</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1.0</td>
<td>...</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>2</th>
<td>2000-03-10 18:40:00</td>
<td>2000</td>
<td>1</td>
<td>Kangaroos</td>
<td>111</td>
<td>Away</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1.0</td>
<td>...</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>3</th>
<td>2000-03-11 14:20:00</td>
<td>2000</td>
<td>1</td>
<td>Adelaide</td>
<td>108</td>
<td>Away</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1.0</td>
<td>...</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<th>4</th>
<td>2000-03-11 19:40:00</td>
<td>2000</td>
<td>1</td>
<td>Fremantle</td>
<td>107</td>
<td>Away</td>
<td>0</td>
<td>0</td>
<td>0</td>
<td>1.0</td>
<td>...</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
</tbody>
</table>
<p>5 rows × 46 columns</p>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [55]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 4463 entries, 0 to 4462
Data columns (total 46 columns):
 #   Column                      Non-Null Count  Dtype         
---  ------                      --------------  -----         
 0   Date                        4463 non-null   datetime64[ns]
 1   Season                      4463 non-null   int64         
 2   Round                       4463 non-null   int64         
 3   Home Team                   4463 non-null   object        
 4   Home Points By              4463 non-null   int64         
 5   Winner                      4463 non-null   object        
 6   Home Season Points By       4463 non-null   int64         
 7   Home Season Points Against  4463 non-null   int64         
 8   Home Season Performance     4463 non-null   int32         
 9   Home Ranking                4463 non-null   float64       
 10  Home Points By Last 1       4453 non-null   float64       
 11  Home Points Against Last 1  4453 non-null   float64       
 12  Home Performance Last 1     4453 non-null   float64       
 13  Home Points By Last 2       4453 non-null   float64       
 14  Home Points Against Last 2  4453 non-null   float64       
 15  Home Performance Last 2     4453 non-null   float64       
 16  Home Points By Last 3       4453 non-null   float64       
 17  Home Points Against Last 3  4453 non-null   float64       
 18  Home Performance Last 3     4453 non-null   float64       
 19  Home Points By Last 4       4453 non-null   float64       
 20  Home Points Against Last 4  4453 non-null   float64       
 21  Home Performance Last 4     4453 non-null   float64       
 22  Home Points By Last 5       4453 non-null   float64       
 23  Home Points Against Last 5  4453 non-null   float64       
 24  Home Performance Last 5     4453 non-null   float64       
 25  Away Team                   4463 non-null   object        
 26  Away Points By              4463 non-null   int64         
 27  Away Season Points By       4463 non-null   int64         
 28  Away Season Points Against  4463 non-null   int64         
 29  Away Season Performance     4463 non-null   int32         
 30  Away Ranking                4463 non-null   float64       
 31  Away Points By Last 1       4455 non-null   float64       
 32  Away Points Against Last 1  4455 non-null   float64       
 33  Away Performance Last 1     4455 non-null   float64       
 34  Away Points By Last 2       4455 non-null   float64       
 35  Away Points Against Last 2  4455 non-null   float64       
 36  Away Performance Last 2     4455 non-null   float64       
 37  Away Points By Last 3       4455 non-null   float64       
 38  Away Points Against Last 3  4455 non-null   float64       
 39  Away Performance Last 3     4455 non-null   float64       
 40  Away Points By Last 4       4455 non-null   float64       
 41  Away Points Against Last 4  4455 non-null   float64       
 42  Away Performance Last 4     4455 non-null   float64       
 43  Away Points By Last 5       4455 non-null   float64       
 44  Away Points Against Last 5  4455 non-null   float64       
 45  Away Performance Last 5     4455 non-null   float64       
dtypes: datetime64[ns](1), float64(32), int32(2), int64(8), object(3)
memory usage: 1.5+ MB
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>There are 8 missing values in each of the 'rolling average' statistics, because these can't be calculated until after a team has played thier first match.</p>
<p>There are two additional missing in the home rolling average statistics: this is because two new teams were added to the AFL.
Gold Coast Suns were added in 2011 and Greater Western Sydney was added in 2012.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [56]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[56]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Season</th>
<th>Round</th>
<th>Home Points By</th>
<th>Home Season Points By</th>
<th>Home Season Points Against</th>
<th>Home Season Performance</th>
<th>Home Ranking</th>
<th>Home Points By Last 1</th>
<th>Home Points Against Last 1</th>
<th>Home Performance Last 1</th>
<th>...</th>
<th>Away Performance Last 2</th>
<th>Away Points By Last 3</th>
<th>Away Points Against Last 3</th>
<th>Away Performance Last 3</th>
<th>Away Points By Last 4</th>
<th>Away Points Against Last 4</th>
<th>Away Performance Last 4</th>
<th>Away Points By Last 5</th>
<th>Away Points Against Last 5</th>
<th>Away Performance Last 5</th>
</tr>
</thead>
<tbody>
<tr>
<th>count</th>
<td>4463.000000</td>
<td>4463.000000</td>
<td>4463.000000</td>
<td>4463.000000</td>
<td>4463.000000</td>
<td>4463.000000</td>
<td>4463.000000</td>
<td>4453.000000</td>
<td>4453.000000</td>
<td>4453.000000</td>
<td>...</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
<td>4455.000000</td>
</tr>
<tr>
<th>mean</th>
<td>2011.233475</td>
<td>12.426619</td>
<td>93.222720</td>
<td>999.803719</td>
<td>978.481067</td>
<td>11.315259</td>
<td>4.016133</td>
<td>87.402425</td>
<td>91.265888</td>
<td>0.918033</td>
<td>...</td>
<td>1.018631</td>
<td>90.238683</td>
<td>88.911635</td>
<td>1.019005</td>
<td>89.995155</td>
<td>89.288739</td>
<td>1.005761</td>
<td>89.982103</td>
<td>89.348784</td>
<td>1.004280</td>
</tr>
<tr>
<th>std</th>
<td>6.601426</td>
<td>7.233967</td>
<td>28.158595</td>
<td>648.015951</td>
<td>606.278774</td>
<td>9.247668</td>
<td>2.520772</td>
<td>28.057759</td>
<td>28.348473</td>
<td>0.996747</td>
<td>...</td>
<td>0.740977</td>
<td>19.103399</td>
<td>19.720215</td>
<td>0.636606</td>
<td>17.550481</td>
<td>18.365747</td>
<td>0.574723</td>
<td>16.556606</td>
<td>17.483370</td>
<td>0.533337</td>
</tr>
<tr>
<th>min</th>
<td>2000.000000</td>
<td>1.000000</td>
<td>16.000000</td>
<td>0.000000</td>
<td>0.000000</td>
<td>0.000000</td>
<td>1.000000</td>
<td>13.000000</td>
<td>19.000000</td>
<td>0.000000</td>
<td>...</td>
<td>0.000000</td>
<td>36.333333</td>
<td>31.000000</td>
<td>0.000000</td>
<td>36.000000</td>
<td>36.500000</td>
<td>0.000000</td>
<td>37.000000</td>
<td>40.200000</td>
<td>0.000000</td>
</tr>
<tr>
<th>25%</th>
<td>2006.000000</td>
<td>6.000000</td>
<td>73.000000</td>
<td>458.500000</td>
<td>463.500000</td>
<td>4.000000</td>
<td>2.000000</td>
<td>67.000000</td>
<td>71.000000</td>
<td>0.000000</td>
<td>...</td>
<td>0.000000</td>
<td>77.333333</td>
<td>75.000000</td>
<td>0.666667</td>
<td>78.250000</td>
<td>76.500000</td>
<td>0.500000</td>
<td>79.000000</td>
<td>77.200000</td>
<td>0.800000</td>
</tr>
<tr>
<th>50%</th>
<td>2011.000000</td>
<td>12.000000</td>
<td>92.000000</td>
<td>955.000000</td>
<td>955.000000</td>
<td>10.000000</td>
<td>4.000000</td>
<td>85.000000</td>
<td>89.000000</td>
<td>0.000000</td>
<td>...</td>
<td>1.000000</td>
<td>89.666667</td>
<td>88.000000</td>
<td>1.333333</td>
<td>89.250000</td>
<td>88.250000</td>
<td>1.000000</td>
<td>89.600000</td>
<td>88.200000</td>
<td>1.200000</td>
</tr>
<tr>
<th>75%</th>
<td>2017.000000</td>
<td>18.000000</td>
<td>111.000000</td>
<td>1480.000000</td>
<td>1467.000000</td>
<td>18.000000</td>
<td>6.000000</td>
<td>105.000000</td>
<td>110.000000</td>
<td>2.000000</td>
<td>...</td>
<td>2.000000</td>
<td>102.333333</td>
<td>101.000000</td>
<td>1.333333</td>
<td>101.000000</td>
<td>100.500000</td>
<td>1.500000</td>
<td>100.800000</td>
<td>100.400000</td>
<td>1.200000</td>
</tr>
<tr>
<th>max</th>
<td>2022.000000</td>
<td>33.000000</td>
<td>233.000000</td>
<td>3139.000000</td>
<td>2681.000000</td>
<td>46.000000</td>
<td>13.000000</td>
<td>233.000000</td>
<td>198.000000</td>
<td>2.000000</td>
<td>...</td>
<td>2.000000</td>
<td>178.000000</td>
<td>171.000000</td>
<td>2.000000</td>
<td>166.750000</td>
<td>171.000000</td>
<td>2.000000</td>
<td>153.000000</td>
<td>171.000000</td>
<td>2.000000</td>
</tr>
</tbody>
</table>
<p>8 rows × 42 columns</p>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [60]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="n">afl_df</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">bins</span><span class="o">=</span><span class="mi">50</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">20</span><span class="p">,</span><span class="mi">15</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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uLi4wNPTE0OGDMHo0aPh7e0NDw8PjBgxAqGhoQgJCQEAhIeHo3bt2hgwYABmz56NxMRETJw4EVFRUXoHYIiIiKzBiRMncPPmTTz33HPKtMzMTBw8eBALFy7Ezp07TXJ3KWDcO0zrTtmp/D/nnae5zctrGWthS3d3GpM52sWS7jDl4AwRERERERFZhCVLlgAAWrdurTU9NjYWgwYNAgDMnTsXdnZ26NWrF1JTUxEREYHFixcrae3t7bF161YMHz4coaGhcHNzQ2RkJKZNm1Zc1SAiIjK6du3a4ZdfftGaNnjwYNSsWRNjx45FpUqVTHJ3KWDcO0xTM1Vay2ulz2VeXstYG1u6u9OYirNdLKn9OThDNq+g79bJnt7QZYiIiIiIqOhEJN80zs7OWLRoERYtWpRrmoCAAKt/7AkREVF2pUqVQt26dbWmubm5oUyZMsp03l1KZF04OENERERERERERERk5Xh3KZF14eAMERERERGZXEHvZiYiIiKivO3fv1/r75J2dymffkPWzs7cBSAiIiIiIiIiIiIiIipJeOcMEREREREVq5xXORIREREREZU0HJwhIiKbUHfKTsxu8vTfizO7mLs4RERUCDkHbS5NDzdTSYiIiIiIiEyLgzNkdHzeIxERERERERERERFR7vjOGSIiIiIiIiIiIiIiomLEwRkiIiIiIiIiIiIiIqJixMea2Tg+YoyIiIiIiIiIiIiIyLLwzhkiIiIiIiIiIiIiIqJixDtnLET2O1x4dwsRERERERERERFR4fBcK1kDDs4QEREREZFR5HykLhEREREREenHx5oREREREZFFqjtlp9a/REREREREtoKDM0RERERERERERERERMWIgzNERERERERERERERETFiO+cMQG+cIqIiIiIbBn7u0REREREREXDwRmiQuJJCSIiIiIiIiIiIiIqDD7WjIiIiIhKrJiYGDRu3BilSpWCj48PunfvjosXL2qlefLkCaKiolCmTBm4u7ujV69eSEpK0kpz7do1dO7cGa6urvDx8cE777yDjIyM4qyK2VQZt035EJVUjAMiIiIiKigOzhARERFRiXXgwAFERUXhyJEjiIuLQ3p6OsLDw/Hw4UMlzVtvvYXvvvsOGzZswIEDB/D333+jZ8+eyvzMzEx07twZaWlpOHz4MFatWoWVK1di0qRJ5qgSERERERERWQE+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rl1bb75FvYght4H3nMvmNs+Q6YYuk1t+hcnT0PLnzIODM7qKs10sqf05OENEREREREQW4fjx42jTpo3yt+Yq3cjISKxcuRLvvvsuHj58iGHDhiE5ORktWrTAjh074OzsrCyzdu1aREdHo127drCzs0OvXr0wf/78Yq8LEREZjne7GiYqKgrr1q3Dli1bUKpUKeUdMZ6ennBxcYGnpyeGDBmC0aNHw9vbGx4eHhgxYgRCQ0MREhICAAgPD0ft2rUxYMAAzJ49G4mJiZg4cSKioqL0DsAQkelwcIaIiIiIiIgsQuvWrSEiuc5XqVSYNm0apk2blmsab29vrFu3zhTFIyIiMqslS5YAeLq/zC42NhaDBg0CAMydO1e5OCE1NRURERFYvHixktbe3h5bt27F8OHDERoaCjc3N0RGRua5b6WiqTJuG9T2ovOOGyIOzhAREREREREREVGx4mMMCy6vCxg0nJ2dsWjRIixatCjXNAEBAbm+sJ6Iig8HZ4iIiIiIyObxcSlERERERGRJODhDRERERERERFaFA65ERERk7ezMXQAiIiIiInM5ePAgunbtCn9/f6hUKmzevFlrvohg0qRJKF++PFxcXNC+fXtcunRJK82dO3fQv39/eHh4wMvLC0OGDMGDBw+KsRZUUFXGbVM+RERERERE5sDBGSvGg0oiIiKionn48CHq16+f6zO5Z8+ejfnz52Pp0qU4evQo3NzcEBERgSdPnihp+vfvj3PnziEuLg5bt27FwYMHMWzYsOKqAhEREREREVkhPtaMiIiIiEqsTp06oVOnTnrniQjmzZuHiRMnolu3bgCAL774Ar6+vti8eTP69u2L8+fPY8eOHTh27BgaNWoEAFiwYAGef/55fPTRR/D39y+2uhAREREREZH14OBMPnhXChEREVHJdPnyZSQmJqJ9+/bKNE9PTzRt2hTx8fHo27cv4uPj4eXlpQzMAED79u1hZ2eHo0ePokePHnrXnZqaitTUVOXve/fuAQDS09ORnp5uohrlT20vZstbH7WdaP1rCuZsb2PR1MFcdbGFNiTrwONzIiIisiUcnCEiIiIi0iMxMREA4OvrqzXd19dXmZeYmAgfHx+t+Q4ODvD29lbS6BMTE4OpU6fqTN+1axdcXV2LWvRCm93EbFnnaXqjLJOte/v27SZbd3GLi4szS76PHj0yS75ERERERNaMgzNERERERMVs/PjxGD16tPL3vXv3UKlSJYSHh8PDw8Ns5ao7ZafZ8tZHbSeY3igL7x+3Q2qWyiR5nJ0SYZL1Fqf09HTExcWhQ4cOcHR0LPb8NXd+ERERERGR4Tg4Q0RERESkh5+fHwAgKSkJ5cuXV6YnJSWhQYMGSpqbN29qLZeRkYE7d+4oy+ujVquhVqt1pjs6Oprl5LpGaqZpBkCKKjVLZbKymbO9jc1c248ttSERERFRccn5uM4rszqbqSRkLnbmLgARERERkSUKDAyEn58f9uzZo0y7d+8ejh49itDQUABAaGgokpOTceLECSXN3r17kZWVhaZNmxZ7mYmIiIiIiMg68M4ZyhdfukhERES26sGDB/jtt9+Uvy9fvoxTp07B29sblStXxqhRozBjxgxUr14dgYGBeP/99+Hv74/u3bsDAGrVqoWOHTti6NChWLp0KdLT0xEdHY2+ffvC39/fTLUiIiIiIiIiS8fBGSIiIiIqsY4fP442bdoof2veAxMZGYmVK1fi3XffxcOHDzFs2DAkJyejRYsW2LFjB5ydnZVl1q5di+joaLRr1w52dnbo1asX5s+fX+x1ISIiIiIiIuvBwRkyirpTdmJ2E81LZC3zWeVEREREObVu3Roikut8lUqFadOmYdq0abmm8fb2xrp160xRPCIiIqISJ/sTXC5NDzdjSYiITIuDM0REREREREREREREFij7gOWVWZ3NWBIyNjtzF4CIiIiIiIiIiIiIiKgk4eAMERERERERERERERFRMeJjzYwk++1lRERERERkfXL26fnYCCLroIldtb1gdhMzF4aIiIjIQBycISIiIiKiEosXWRHZnrpTdiI1U8UBViIiIrJoHJwhm2PsA2xehUVERES2jIMTRGSreDccERERWTK+c4aIiIiIiIiIiIiIiKgYcXCGiIiIiIiIiIiIiIioGPGxZhaIj5YgIiIiIjK/7P1yPg6JiIjIvPioQiJtjAnrxztniIiIiIiIiIiIiIiIihEHZ2xQ3Sk7tf4lIiIiIiIiIiKyNjzHRVQ4VcZtUz5kufhYM7I4tvajYWv1ISIiIiIiskZ8VCERERFZEt45Q0REREREREREREREVIx45wwRERERERERERERkY3jXaSWhYMzRERERDaInW4iIiIiIiIiy8XBGSIiIiKiEobvxCOiko4XMRAREZG5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0KdPH1y8eBF2dk/H386dO4fmzZujQoUKGDduHNzc3PC///0P3bt3x9dff40ePXoUqp53795FUFCQ1vSVK1fC3d0do0ePhru7O/bu3YtJkybh3r17mDNnjlbau3fvomPHjujZsyf69OmDjRs3YuzYsahXrx46deqkN9/Hjx+jW7duOH78OHbv3q0EVW5+++039O7dG0OGDEFkZCQ+//xzDBo0CMHBwahTpw4A4Pr160oHZ/z48XBzc8Nnn30GtVpd4HYhXSUlJu7evYu7d++iWrVqAIDdu3ejU6dOqFq1KqZMmYLHjx9jwYIFaN68OX7++ed8Twrmt+22atUKI0eOxPz58zFhwgTUqlULwNOB05s3byI8PBzlypXDuHHj4OXlhStXruCbb74xqC6ZmZnKd5aeno7z589j8uTJqFatGpo3bw7gaUe6UqVKWLt2rU57rV27FkFBQUZ5cdunn36KF154Af3790daWhrWr1+PF198EVu3bkXnzp0BPP0+u3TpgmeffRbTpk2DWq3Gb7/9hh9//FFpk2nTpmHSpEkYNmwYWrZsCeDpTtbSMX6sL36OHj2K3377DbGxsXByckLPnj2xdu1apUOocfLkSXTs2BHly5fH1KlTkZmZiWnTpikHatktWbIEderUwQsvvAAHBwd89913eOONN5CVlYWoqKh8yzRr1izY2dnh7bffRkpKCmbPno3+/fvj6NGjAIC0tDREREQgNTUVI0aMgJ+fH65fv46tW7ciOTkZnp6eWL16NV577TU0adIEw4YNAwCdPkBhGFK3/L6TcuXKYcmSJRg+fDh69OiBnj17AgCeffbZIpfPUCU1VguaxxtvvIFy5cph0qRJePjwIVq1aoUKFSrggw8+wMiRI9G4cWP4+voCKPjvwIsvvojq1avjgw8+gIgYpQ3j4uLwxx9/YPDgwfDz88O5c+fw3//+F+fOncORI0d0Tkb16dMHgYGBiImJwc8//4zPPvsMPj4++PDDD5U0U6dOxZQpU9CsWTNMmzYNTk5OOHr0KPbu3Yvw8HAAwOrVqxEZGYmIiAh8+OGHePToEZYsWYIWLVrg5MmTRhlYLOn717yU1Hi25n0v+676iQiSkpKU497iwPixvvhh37VgLK3vmpiYiLJlyxZ4uZIaq+y7su9qcfvXIt97QwrNrYF5fbLfGnjq1CkBIK+99prWet5+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8OBBZWdnu/QHZtCgQQ7pi4iIUHJysiZMmKAvv/yywe+bnJysxMREbd68WdLl65KGhIRox44dSklJcVX0a3T06FFlZ2c71WiSpAMHDuhHP/qRrrrqKkVGRqpVq1YaMGCA3n33XfdG9P9Qftzvyy+/tJefyt9PSSotLdWuXbvs38+UlBSdPHlShYWF9jDvvfeeysvL1a9fvyrv37dvX4WEhGjx4sXuT4wLGGM0adIkrV69Wu+9956Sk5Md9vfq1UuhoaGaN2+efduhQ4dUVFTkkEeffPKJjh8/ri+++EIhISF6+OGHFR0drS5durg1/ufOnVN2drbT36OjR4/qxz/+sTp27KgWLVooNjZWffv21fLly2WMcfq4gVRWK9ZXvXr1kiRdccUV9rIaHx+voqIiWSwWlx7XarXqRz/6kU6cOKGFCxfqjTfeUPv27et8nTvKraf9+9//1jfffGNvI7givrb69Q9/+INT4Z0p++Hh4Q75XLHsHz16VJ9//rn27dvncPKdn59fbdn3dv1am7rKc1pamiIiIhzyory8XJs3b/ZIW6YxfKXu9ae2a2X1LVuNVV3bta7yWtHcuXMVEhLisTookOrDyip+vz788EMtWrRITz31lMLCwmr8bXQHd5SfinWpre26YMECv6pLa/P0009rzZo1kuquc7/44guFh4fr0qVLHklXfduula1YsUIhISFq3rx5vV7nb2W1cvu0tjaJp+q6YG671qUhbVtfqF/rw9P1a21ou7ofbVfnVS5bdbVbbfGr7rFz506PxLlaJoAsW7bMSDJ79uypdv/AgQNN165dPRwr15Bkhg4dat544w3z+uuvm1mzZpmEhAQTEhJiRo8ebbZu3WqOHDliPvjgA5OammpatWpljh8/Xu17Xbx40Xz77bemvLy83vFYtWqVkWS2bNnSyBR9Z+DAgaZNmzbmjTfeMG+88YZZunSpeeihh0xUVJRp166dOXv2bI2vPX36tPnoo4/MRx99ZCSZBQsWmI8++sj861//MsYY88wzz5jY2FjzzjvvmKVLlxpJJj4+3nz77bcui39N9uzZYySZZcuWORV+3bp1Jj093WRnZ5tXXnnFvPDCC+bWW281ksz//u//ujeyJnjLz/r16+v1XvUpP5W/n5mZmUaSeeutt4wxjt/Pffv2mTvuuMMkJyc7fD+HDRtmbrjhBrNr1y7z/vvvm2uvvdbcfffdVY71j3/8w0gyHTp0MDfffHO90tQYZWVlpqysrEGvnThxoomJiTFbt241x44dsz/OnTtnD9OkSRMTFRVl3nvvPfPhhx+alJQUk5KSYt9/8eJF061bN5OWlmbWrVtnJJmoqCgzffr0RqetLl999ZWRZJ588kmnwn/88cdm4MCB5vHHHzdLliwxL7/8svnBD35gJNUrvv5cVh966KFa6ytJpmnTpmb69Olm1qxZpk2bNiY8PLxBZbU2n376qZFkXn311Sr76lOvNLbcukJt8T19+rT55S9/aQoKCsyRI0fMpk2bzI033miuvfZac/78eZfFd8uWLUaSWbVqlVPhnSn7P/vZz0y7du2qLfu2+vV73/ueSUtLM3v37jUbNmwwV155ZbVlydv1a22cKc9t2rQxFovF5ObmmoMHD5oJEyaY2NhYU1xc7OHY1o+36t7K3njjDXt5r65MN0Rj2q71Ud+y1VjVtV2dKa/GGPPll1+ayMhIExUV5bE6yJ/rw5rY6klJpk+fPqZr166mefPm5pFHHjEJCQlGkrnyyitrbBdVxxvnfs7UpS1atDCSTFJSkomLi/NYXdqYtqszdW6zZs1MRkaGU3WuLX979uzZ6HQ5o75t14pOnz5tkpKSTFRUlImKiqrXa329rNbVPq2tTeLKuq42gdR2rYsn2ra+UL86yxv1a21ouzqHtqt3ylZd7VZb/H7xi1/Y88L2+OqrrzwS5+owOOMnJJmsrCyHbfv27TOSTGJiomndurWJiIgw3/ve98xdd91lPvvsM7fEw12DM9V9Lr/5zW+MJJOXl1fja20Fq/IjMzPTGGNMeXm5eeKJJ0xCQoIJDw83ksyLL77osrjXpjEVsM3FixfN9ddfbzp27Oi6iNUgWMtPWlqa245b0/czPT3dGOP4/bRYLGbIkCHm0KFDDu/xzTffmLvvvts0b97cREdHm/vvv9+cPn26yrFmzpxp4uPjzR//+EcTEhJijhw54rZ0uUp1eVO5zERFRZmOHTuaK664wkRGRpo777zTHDt2zOF9vvjiCzN8+HBjsViMJDNgwABjtVrdHv/GnOBW9P3vf99ERUWZixcvOhXen8vqXXfdVWt9Jcl069bN4fN+7733XFZWz5w5Y4wxZtu2bTU2GutTr1Qst7b3Nsb5cusKtcX33LlzJi0tzVx55ZUmPDzctG/f3jz44INVTowaG9/6NsKdKfvffvut+fnPf15t2bfVr88995wZPny4adasmWnVqpV56KGHnC77nqxfa+NseX755ZdNu3btTEREhOnbt6/ZuXOnh2Naf96qeyvLzs6utUw3RGParvXh7RNcY5wrr8Zc/n0fPHiwR+sgf64Pa2KrJ22TTSrWk7by07Zt21rbRa7U0HM/Z+rSW2+91YSGhpomTZoYSWbz5s0O7+HJutRZztS5kkxISIhTdW7z5s2NJPPUU095JP6Nabs++uijpmPHjmbs2LEBNzhTV/u0tjaJu+u6QGy71sUTbVtfqF+d5Y36tTa0Xd2PtqvzKpetutqtno6fs4J+cMZqtZrZs2ebq666ykRERJj27dub6dOnO4y6G2NM+/btzYgRI8yWLVtMr169TNOmTU23bt3sDdU//vGPplu3bsZisZgbb7zR/O1vf6ty/E8//dRkZGSYK664wlgsFtOrVy/zzjvvOJW26n4kjDGmVatW5tprr7U/37x5s7nllltMZGSkiYmJMT/4wQ/MwYMHq82nip23tvT99a9/NX369DEWi8UkJyeb5cuXV3ld5YctD/bs2WPS0tJMy5YtTdOmTU2HDh3M/fffX2faavqR+MMf/mAkmffee88YY+wddH/605+qhF2xYoWRZHbs2FHjcZwthM8995xJSUkxcXFxpmnTpubGG2+s9jV5eXnm5ptvNjExMSYqKspcd9119hm7NTUoGlIZf//73zcJCQn1fl19UX78s/zYXHPNNebnP/+5KSsrM7GxsWbu3LnVhrN9BhaLxVx11VVmyZIl5sknnzSSY3Xw2muvmdtuu81ceeWVJiIiwnTu3NksWrSoyvsNHDjQDBw40OH9JZm3337bPPXUU+Z73/uesVgsZvDgwebw4cMOr/3HP/5hRo8ebT9RsJ0MnTx50hhTfcVaW4PkyJEj9g7b2jibtto+E9uxKj8acrI7adIkExISUmUWck0oq84dw5ZPW7duNRMnTjRXXnmliY2Nta9gq/io+B125nfAVmYOHDhg7r77bhMbG2uf9drYPPz4449NZmamSU5ONhaLxSQkJJj777/ffP3119XG4fDhwyYzM9PExMSY6Ohoc99991U78+mNN94wffr0Mc2aNTOxsbHm1ltvNRs3bnQIs379envamzdvbm6//Xazf//+Gj6t71C/Nhzl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xsZKktauXSur1Vpn+Mo6dOhg/5z+8pe/6IUXXtCpU6c0fPhwffXVV/Zw48aNU1lZmf7whz/Yt7399tu6ePGifvzjH9f7uNVp1qyZ/f///ve/OnXqlG699Vb97W9/s2+3pfedd95ReXm5S45rM2XKFOXn52v58uUaPny4Ll26pAsXLrj0GLWh/PhX+bl48aLefvtt3XXXXQoJCZF0OU/j4+O1YsUKe7hLly5p06ZNGjVqlJKSkuzbr7nmGg0fPrzK+1YsB6dOndLXX3+tgQMH6p///KdOnTpVZ7zuv/9+RURE2J/b8saWHzExMZKkjRs36ty5c/VJcqM5k7bG/qbV5u6771Z+fr5Wrlype+65R5L07bff1vt9grGsNuQYDz74oMLCwuo8bkN+B372s59V+14NzUPJ8ft5/vx5ff311+rfv78kOdRDNcXh1ltv1TfffKPS0lJJ0po1a1ReXq6ZM2cqNNSx2Wf7zcjPz9fJkyd199132/P066+/VlhYmPr166ctW7ZUm876Cvb6tTbBWJ79ue6VaLtK0jfffKOZM2fqiSee0JVXXumS92wIyo9/lR/arvXnrbbrhQsXNHXqVP3sZz9Tly5dGv1+wVhWabvSdm0IX6lfaxOM5dmf616Jtqsk3XTTTfrDH/6gBx54QD/4wQ/02GOPaefOnQoJCdH06dNdcoyGaOK1I7tR37591bt37yrbr7jiCn399df25//6178UGhqqa665xiFcYmKiYmNj9a9//cthe8UfAum7Blrbtm2r3f7f//5XkvTZZ5/JGKMnnnhCTzzxRLVxPn78uL73ve/Vmq477rhDkyZNUkhIiFq0aKGuXbsqKirKnhZJ6tixY5XXde7cWRs3btTZs2ft4atTOX3S5TyzpaM2AwcOVEZGhmbNmqWFCxdq0KBBGjVqlO655x5ZLJY6Xx8VFaXU1FT782HDhumWW25R79699cwzz+jXv/61JKlTp07q06ePVqxYofHjx0uSVqxYof79+1f5HBtq7dq1euqpp7R3716VlZXZt9saApJ011136be//a1+8pOf6LHHHtOQIUM0evRo/fCHP6zSgKivTp06qVOnTpIu/yimpaVp5MiR2rVrl0Mc3IXy48jXy09eXp6++uor9e3bV5999pl9+2233abf/e53evbZZxUaGqrjx4/r22+/rbacVLftgw8+0JNP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cKB2796t5cuXa9SoUfVeTl2bnJwc3XLLLerevbsefPBBXXXVVSopKVFBQYH+/e9/6+OPP270MZ577jkNHz5cKSkpGj9+vL799lu9/PLLiomJUXZ2duMTocsFISwsTM8++6xOnToli8WiwYMHa+XKlVq0aJHuvPNOXX311Tp9+rReffVVRUdHO/UDderUKb355puSLt8k8tChQ1q8eLGaNWumxx57rEr4cePG2WdbzZkzp15p+OMf/6i///3vVbZnZmZqxIgRWrBggYYNG6Z77rlHx48fV05Ojq655hrt27fPHnb27Nnavn27RowYofbt2+v48eNatGiR2rRpo1tuuUXS5dkcsbGxWrJkiVq0aKGoqCj169evxuu8/vSnP1VpaakGDBig733veyouLtaKFSv097//Xb/+9a+9NoJbE8pP/bm6/KxYsUItW7bUTTfdVO3+H/zgB3r11Ve1bt06jR49WtnZ2crLy9PNN9+siRMn6tKlS/rNb36jbt26ae/evfbXpaWlKSIiQiNHjtRPf/pTnTlzRq+++qri4+Orbeg0xHvvvadJkybpRz/6ka677jpdvHhRb7zxhsLCwpSRkWEP16tXL23atEkLFixQUlKSkpOT7Tf/q8nmzZt1/vz5KttHjRrldNqWL19e52di69R9++23dd111ykuLk7dunVTt27dqo3X3Llz9cEHH2jYsGFq166dTpw4oT/+8Y/as2ePJk+e7LLrt1YWaGXVncfwxO9AbaKjozVgwADNnz9fVqtV3/ve95SXl6cjR440+D2vueYa/epXv9KcOXN06623avTo0bJYLNqzZ4+SkpI0b948RUdHa/Hixbr33nt14403asyYMbryyitVVFSkdevW6eabb3ZqGTv1q/sFWnn2x7rXJtjbrq1atdKoUaOqbLd1vlS3z9soP/VH2/U7wdZ2jYyMrLYcr1mzRrt373ZrGQ+0skrbtX6Cve3qj/VrbQKtPPtj3WsT7G1X6fJ9bJo1a6abbrpJ8fHxOnjwoF555RVFRkbqmWeeqVcaXcoEkGXLlhlJZs+ePdXuHzhwoOnatavDNqvVambNmmWSk5NNeHi4adu2rZk+fbo5f/68Q7j27dubESNGVHlPSSYrK8th25EjR4wk89xzzzls//zzz824ceNMYmKiCQ8PN9/73vfM97//ffOHP/yhzrRVd5zqbNq0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SGxsbKWXYevGjBlT6m6LcePGlRrWs2dP5c6148ePCwDJzMwUJycn5a6z/v376719XET/7y1y9znGderUUQ56CgsLJSgoSOvkiT6ag62SH5VKJXFxccpB5AMPPKB156ZGamqqAP9eNFBWI/feRwO98MILUr16deW7vvrg9u3b4ubmJnFxcRV+1IEmxj/77DNJT0+XHTt2yPLly6V9+/bi5eWl9RiWoqIiCQkJkaeffloZ9vPPPwsAWbp0aYXW66jsIR6KioqUu7dLxkS3bt206t/mzZtLz549S+3vd+7cWeqkkiHpNmS/HRMTI8HBwaXGaw5gNSeiNHF475XsV69eFQAyb968MstA3+N9AgIClJMya9euFUD7almRuydqfHx8tE7U6Du5bEj69J1cnjJlijg7O5fqTDUEcPcl2Jo23+bNm2XChAni7u4uAwYM0LpKU3NHX8lHscTHx2td0GUsjB/Gjy3Ez48//iiA9hXWmrqy5LBvv/1WAGhdpSxy97i7evXqei960ByrXL58WeLi4pRHHmvc204wtC1vzLYxY9VxYrUix3ea9q6uO611dc5UZD/QpUsXUavVpTox9ZXBpk2bdJ7T0XR86bsjLDc3Vy5fviwfffSRAJCjR49qpcHb27tU3ffoo49Kq1atlO9xcXGlOmvv9cILL4ivr69cunSpVLl6e3uXuiDW0djDPkbX8SUAefTRR8vsnDXGuRsRUeIiKSlJXFxcZO3ataXWVZXj1pEjR4qrq2up87CaTht2ztzlBAtr3749oqOjS32qV6+uNd3vv/8OJycn3H///VrDg4OD4efnh99//11reJ06dbS++/r6AgBq166tc/g///wDADh9+jREBJMmTUJAQIDWZ8qUKQCAS5culZuvvn37Ij09HTt37sShQ4fw999/491334WTk5OS1oYNG5aar3Hjxvj777+Rl5dX5vLvzR8AVK9eXclHWbp06YL4+HhMnToVNWvWRN++fbF8+XLk5+eXO++OHTtw+fJltG/fHqdPn8bp06dx9uxZPPzww/j4449RXFwM4G4Z3bp1q9TvBUDnsG+//RbR0dHw8vKCn58fAgIC8NprrwEArl27Vm667i0PzfajKY/w8HCMHTsWH3zwAWrWrInY2FikpaUZtOyqMiRvVflNKsLf3x/Dhw/HyZMn8eeff1ZoXkeM1cqsIzw8vNx1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X7lp1qyj5MfLy0uioqLKnL93794CQA4cOFDuOsh+4iE3N1fmzZsnsbGxEhoaKq6urlKtWjWJioqSpUuXSnFxsdb0169flwkTJsj9998vbm5uUrNmTXnwwQflnXfekTt37lQo3Ybut7Ozs2X48OFSs2ZNcXNzk2bNmpXad+trW4hIue0skbLr93stXLhQGjVqJK6urhIUFCSJiYnyzz//aE2TkJAgYWFhlUpfYWGhPP/88xIQECAqlUops08//VRiYmIkMDBQ3NzcpE6dOvKf//xHLl68WG6a790nODs7S2hoqIwaNUqys7N1znP48GEBIDExMeUuv6IYP4wfW4ifzz77TO+2pbF3714BIPPmzVOGzZ8/X8LCwkStVkv79u3l22+/lTZt2kjPnj2VaYqLi2XGjBnKdK1atZItW7aUyruuPBraljdG25ix6rixasjxnb72rkjZx72G7Af0tdX1lYG+vOk6tv/222+lQ4cO4uHhISEhIfLKK6/I9u3blfNs5aVBV5zevHlTXn/9deW8SXBwsDz22GNy5swZrenef/99adOmjXh4eEi1atWkWbNm8sorr8iFCxdKrccR2Ms+RqTs40tNXaGJUVOcu9F13mjz5s3i4uIiAwcOlKKioioft16+fFmeeuopqVatmvj6+sqwYcPk22+/FQCybt06A0rJ/qlEqtDVS1QJ/fr1w/Hjx43ybEQiIqLKmDdvHsaMGYNz585pvROMKqZ///74+eef+dxgG8d4IGP58ccf0bJlS6xatarUnTX2ivFDplBcXIyAgAAMGDBA63EwVHmMVSIyJe5jDLdp0yb0798f33zzDTp27Gjp5FicYz34nszu3ucUnjp1Cl9++SW6du1qmQQREZHDExEsW7YMXbp0YcO5Ci5evIitW7c6zAlYe8V4IGNaunQpvL29MWDAAEsnxSwYP2QMt2/fLvV4pFWrVuHq1as8bjYSxioRmRL3Mfrde164qKgICxYsgI+Pj1EfL27LbOadM2Sb6tWrh2HDhqFevXr4/fffsXjxYri5ueGVV16xdNKIiMjB5OXl4fPPP8eePXvw888/Y/PmzZZOkk06e/Ysvv32W3zwwQdwdXXFf/7zH0sniSqB8UDG9MUXXyjvWEtOTlZeGG6vGD9kTAcPHsSYMWPw+OOPo0aNGvj++++xbNkyNG3aFI8//rilk2fTGKtEZErcx5Tv+eefx61btxAVFYX8/Hxs2LABBw4cwIwZM+Dh4WHp5FkFPtaMTGr48OHYs2cPsrKyoFarERUVhRkzZrB3lIiIzO7cuXMIDw+Hn58fnnvuObz55puWTpJNWrFiBYYPH446derg3XffdcgXkdoDxgMZU926dZGdnY3Y2FisXr3arC+itgTGDxnTuXPn8MILL+Dw4cO4evUq/P390bt3b8ycOROBgYGWTp5NY6wSkSlxH1O+tWvX4t1338Xp06dx+/Zt3H///UhMTERycrKlk2Y12DlDRERERERERERERERkRnznDBERERERERERERERkRmxc4aIiIiIiIiIiIiIiMiMXCydAFMpLi7GhQsXUK1aNahUKksnh6hCRATXr19HSEgInJzsow+VMUm2jDFJZF0Yk0TWhTFJZF0Yk0TWhTFJZF2sKSbttnPmwoULqF27tqWTQVQlf/zxB0JDQy2dDKNgTJI9YEwSWRfGJJF1YUwSWRfGJJF1YUwSWRdriEm77ZypVq0agLuF7OPjY/TlFxQUYMeOHYiJiYGrq6vRl2/tHD3/gGnLIDc3F7Vr11a2Y3tQXkxym6oall/VlFd+jhiTdBdjq+LMUWaOGJP2vC0yb7apZN5u3brFmLQzzJ9tYz1pf7+psbG8Kqaq5eWIMWmPGDf/svWysKaYtNvOGc0tdT4+PibrnPH09ISPj49NboRV5ej5B8xTBvZ0a2h5McltqmpYflVjaPk5UkzSXYytijNnmTlSTNrztsi82SZdeWNM2g/mzz4wJkkfllfFGKu8HCkm7RHj5l/2UhbWEJP28aBDIiIiIiIiIiIiIiIiG8HOGSIiIiIiIiIiIiIiIjNi5wwREREREREREREREZEZsXPGwdR9davyISIqifsHsmfcvsleNE3Zzu2Y7FpqairatWuHatWqITAwEP369cPJkye1prl9+zaSkpJQo0YNeHt7Iz4+HtnZ2VrTnD9/HnFxcfD09ERgYCBefvllFBYWGj29jEki68d2IJFlMPaIysfOGSIiIiJyWLZ2IpjI3u3btw9JSUk4ePAg0tPTUVBQgJiYGOTl5SnTjBkzBl988QXWr1+Pffv24cKFCxgwYIAyvqioCHFxcbhz5w4OHDiAlStXYsWKFZg8ebIlskREREREpBM7Z4iIiIjIYfFEMJF12bZtG4YNG4YmTZqgRYsWWLFiBc6fP4/MzEwAwLVr17Bs2TLMnj0b3bp1Q5s2bbB8+XIcOHAABw8eBADs2LEDJ06cwEcffYSWLVuiV69emD59OtLS0nDnzh1LZo+IiIiISMHOGSIiIiJyWDwRTGTdrl27BgDw9/cHAGRmZqKgoADR0dHKNI0aNUKdOnWQkZEBAMjIyECzZs0QFBSkTBMbG4vc3FwcP37cjKknIiIiItLPxdIJICKiu0o+h/XczDgLpoRMafHixVi8eDHOnTsHAGjSpAkmT56MXr16Abj7+KRx48Zh3bp1yM/PR2xsLBYtWqR1gun8+fNITEzEnj174O3tjYSEBKSmpsLFhdU6UVVV9ERwhw4d9J4ITkxMxPHjx9GqVSvzZoLIThQXF2P06NHo2LEjmjZtCgDIysqCm5sb/Pz8tKYNCgpCVlaWMk3JeNSM14zTJT8/H/n5+cr33NxcAEBBQQEKCgpKTa8ZpnYSre/2QpMfe8uXhqPkj4iIiKwbz+IQERGZUWhoKGbOnIkGDRpARLBy5Ur07dsXP/zwA5o0aYIxY8Zg69atWL9+PXx9fZGcnIwBAwbg22+/BfDv45OCg4Nx4MABXLx4EUOHDoWrqytmzJhh4dwR2TaeCLYMez5J6ih5M1X+kpKScOzYMXzzzTcmWX5JqampmDp1aqnhO3bsgKenp975prctBgB8+eWXJkubJaWnp1s6CSZlr/m7efOmpZNAREREBmDnDBERkRn16dNH6/ubb76JxYsX4+DBgwgNDcWyZcuwdu1adOvWDQCwfPlyNG7cGAcPHkSHDh2Uxyft3LkTQUFBaNmyJaZPn47x48cjJSUFbm5ulsgWkV3giWDLsteTpID9580UJ4KTk5OxZcsW7N+/H6Ghocrw4OBg3LlzBzk5OVqdptnZ2QgODlamOXz4sNbysrOzlXG6TJgwAWPHjlW+5+bmonbt2oiJiYGPj0+p6QsKCpCeno5J3zkhv1iFYymxlc6rNdLkr0ePHnB1dbV0cozO3vOn6fAnIiIi68bOGSIiIgspKirC+vXrkZeXh6ioKD4+iciCeCLYcuz5JKmj5O3WrVtGW66I4Pnnn8fGjRuxd+9ehIeHa41v06YNXF1dsWvXLsTHxwMATp48ifPnzyMqKgoAEBUVhTfffBOXLl1CYGAggLudSD4+PoiIiNC5XrVaDbVaXWq4q6trmb9dfrEK+UUqu/t9NcrLv62z1/zZY56IiIjsETtniIiIzOznn39GVFQUbt++DW9vb2zcuBERERE4evSoSR6fBFT8EUr2Ru0syv8Vya89P5LIVMxRZsZcNk8EWw97PUkK2H/eCgsLjba8pKQkrF27Fps3b0a1atWUus3X1xceHh7w9fXFiBEjMHbsWPj7+8PHxwfPP/88oqKi0KFDBwBATEwMIiIiMGTIEMyaNQtZWVmYOHEikpKSdMYdEdmPpinbkV+k4js8iYjIJrBzhoiIyMwaNmyIo0eP4tq1a/j000+RkJCAffv2mXSdlX2Ekr2Y1f7f/yvzOCh7fiSRqZiyzIz5CCWeCCayLosXLwYAdO3aVWv48uXLMWzYMADAnDlz4OTkhPj4eOTn5yM2NhaLFi1SpnV2dsaWLVuQmJiIqKgoeHl5ISEhAdOmTTNXNoiIiIiIysXOGSIiIjNzc3PD/fffD+DuVflHjhzBvHnzMHDgQJM8Pgmo+COU7E3TlO3K/xV5HJQ9P5LIVMxRZsZ8lj5PBBNZFxEpdxp3d3ekpaUhLS1N7zRhYWF2+W4mIiIiIrIf7JwhIiKysOLiYuTn55vs8UlA5R+hZC/yi1TK/5XJr6OUkzGZssyMuVyeCCYiIiIiIiJLcLJ0Aoioavbv348+ffogJCQEKpUKmzZt0hovIpg8eTJq1aoFDw8PREdH49SpU1rTXL16FYMHD4aPjw/8/PwwYsQI3LhxQ2uan376CZ06dYK7uztq166NWbNmmTprRHZpwoQJ2L9/P86dO4eff/4ZEyZMwN69ezF48GCtxyft2bMHmZmZGD58uN7HJ/3444/Yvn07H59ERERERERERGRjeOeMnav76lZLJ4FMLC8vDy1atMAzzzyDAQMGlBo/a9YszJ8/HytXrkR4eDgmTZqE2NhYnDhxAu7u7gCAwYMH4+LFi0hPT0dBQQGGDx+OUaNGYe3atQDuPj4mJiYG0dHRWLJkCX7++Wc888wz8PPzw6hRo8yaXyJbd+nSJQwdOhQXL16Er68vmjdvju3bt6NHjx4A+PgkIiIiIiIiIiJHwM4ZIhvXq1cv9OrVS+c4EcHcuXMxceJE9O3bFwCwatUqBAUFYdOmTRg0aBB++eUXbNu2DUeOHEHbtm0BAAsWLEDv3r3xzjvvICQkBGvWrMGdO3fw4Ycfws3NDU2aNMHRo0cxe/Zsds4QVdCyZcvKHM/HJxERERGRNZo5cyYmTJiAF198EXPnzgUA3L59G+PGjcO6deu0LiwKCgpS5jt//jwSExOxZ88eeHt7IyEhAampqXBxsfwpqZIXtJ6bGWfBlBARkSPiY82olLqvbtX6kO06e/YssrKyEB0drQzz9fVFZGQkMjIyAAAZGRnw8/NTOmYAIDo6Gk5OTjh06JAyTefOneHm5qZMExsbi5MnT+Kff/4xU26IiIiIiIjIEo4cOYL33nsPzZs31xo+ZswYfPHFF1i/fj327duHCxcuaD3RoaioCHFxcbhz5w4OHDiAlStXYsWKFZg8ebK5s0BkF+rWrQuVSlXqk5SUBADo2rVrqXH//e9/tZZx/vx5xMXFwdPTE4GBgXj55ZdRWFhoiewQOTzLX6ZAFsMrROxfVlYWAGhdtaT5rhmXlZWlvFRcw8XFBf7+/lrThIeHl1qGZlz16tVLrTs/Px/5+fnK99zcXABAQUEBCgoKSk2vGaZrnKNQO//7UuqKloMxyq8q67d15ZWfo5UHEREREZHGjRs3MHjwYCxduhRvvPGGMvzatWtYtmwZ1q5di27dugEAli9fjsaNG+PgwYPo0KEDduzYgRMnTmDnzp0ICgpCy5YtMX36dIwfPx4pKSlaFwBaK547IWty5MgRFBUVKd+PHTuGHj164PHHH1eGjRw5Uuux156ensr/mg7T4OBgHDhwABcvXsTQoUPh6uqKGTNmmCcTRKRg54wd4t0uZA1SU1MxderUUsN37Nih1TC4V3p6uimTZdVmtf/3/8o+sqoq5WeM9ds6feV38+ZNM6eEiIiIiMg6JCUlIS4uDtHR0VqdM5mZmSgoKNB6UkOjRo1Qp04dZGRkoEOHDsjIyECzZs20LhiMjY1FYmIijh8/jlatWpk1L0S2LiAgQOv7zJkzUb9+fXTp0kUZ5unpieDgYJ3z20OHKZE9YecMkR3TVMbZ2dmoVauWMjw7OxstW7ZUprl06ZLWfIWFhbh69aoyf3BwMLKzs7Wm0XzXV+FPmDABY8eOVb7n5uaidu3aiImJgY+PT6npCwoKkJ6ejh49esDV1bWCObUPTVO2K/8fS4mt0LzGKL+qrN/WlVd+mju/yPrxykYiIiIi41m3bh2+//57HDlypNS4rKwsuLm5wc/PT2v4vU9q0PUkB804fSr7JAa1k2h9B8p+QoAhTw+wxycM8MkVFVPV8jJVOd+5cwcfffQRxo4dC5VKpQxfs2YNPvroIwQHB6NPnz6YNGmScpEsO0yJrAs7Z4jsWHh4OIKDg7Fr1y6lMyY3NxeHDh1CYmIiACAqKgo5OTnIzMxEmzZtAAC7d+9GcXExIiMjlWlef/11FBQUKCeu09PT0bBhQ52PNAMAtVoNtVpdarirq2uZnQfljbdn+UX/NqYqWwZVKT9jrN/W6Ss/Ry0PIiIiInJcf/zxB1588UWkp6fD3d3drOuu7JMYprctBqD9JICynhBgyNMD7PkJA4785IrKqGx5mepJDJs2bUJOTg6GDRumDHvqqacQFhaGkJAQ/PTTTxg/fjxOnjyJDRs2ADBfhylgfx2b7NT8l62XhTWlm50zdoKPMnNcN27cwOnTp5XvZ8+exdGjR+Hv7486depg9OjReOONN9CgQQOEh4dj0qRJCAkJQb9+/QAAjRs3Rs+ePTFy5EgsWbIEBQUFSE5OxqBBgxASEgLgbuU+depUjBgxAuPHj8exY8cwb948zJkzxxJZJiIiIiIiIhPLzMzEpUuX0Lp1a2VYUVER9u/fj4ULF2L79u24c+cOcnJytO6eyc7O1noKw+HDh7WWW95TGIDKP4lh0ndOyC9WaT0JoKwnBBjy9AB7fMIAn1xRMVUtL1M9iWHZsmXo1auXcu4GAEaNGqX836xZM9SqVQvdu3fHmTNnUL9+/UqvqzIdpvbasclOzX/ZallY06Pr2TlDZOO+++47PPzww8p3TQM2ISEBK1aswCuvvIK8vDyMGjUKOTk5eOihh7Bt2zatK5/WrFmD5ORkdO/eHU5OToiPj8f8+fOV8b6+vtixYweSkpLQpk0b1KxZE5MnT9aq9ImIiIiIiMh+dO/eHT///LPWsOHDh6NRo0YYP348ateuDVdXV+zatQvx8fEAgJMnT+L8+fOIiooCcPcpDG+++SYuXbqEwMBAAHdP5vn4+CAiIkLvuiv7JIb8YhXyi1Ra05T1hABDnh5Q1jS2/khdR35yRWVUtrxMUca///47du7cqdwRo4/miSinT59G/fr1zdZhCthfxyY7Nf9l62VhTY+uZ+cMlcvWGxv2rmvXrhARveNVKhWmTZuGadOm6Z3G398fa9euLXM9zZs3x9dff13pdBIREREREZHtqFatGpo2bao1zMvLCzVq1FCGjxgxAmPHjoW/vz98fHzw/PPPIyoqCh06dAAAxMTEICIiAkOGDMGsWbOQlZWFiRMnIikpSWfnCxEZZvny5QgMDERcXNnn6Y4ePQoAynuIzdlhaq+PTmen5r9stSysKc3snCEiIiKrxwsFiIiIiKzPnDlzlKcv5OfnIzY2FosWLVLGOzs7Y8uWLUhMTERUVBS8vLyQkJBQ5sWDRFS24uJiLF++HAkJCXBx+ffU7pkzZ7B27Vr07t0bNWrUwE8//YQxY8agc+fOaN68OQB2mBJZG3bOEBERERERERFRufbu3av13d3dHWlpaUhLS9M7T1hYmF29b4LI0nbu3Inz58/jmWee0Rru5uaGnTt3Yu7cucjLy0Pt2rURHx+PiRMnKtOww5TIurBzhoiIiBwK78IhIiIiIiJbFRMTo/Px9rVr18a+ffvKnZ8dpkTWg50zREREZJdKdsIQEREREREREVkTds4QEREREREREREZCe/UJiIiQzhZOgFERERERERERERERESOhHfOEAA++oWIiIiIiIiIiIgsh3edkaNh5wwRERE5rHsvTuABABERERERERGZg9Efa5aamop27dqhWrVqCAwMRL9+/XDy5EmtaW7fvo2kpCTUqFED3t7eiI+PR3Z2ttY058+fR1xcHDw9PREYGIiXX34ZhYWFxk4uERERERERERERERGRWRm9c2bfvn1ISkrCwYMHkZ6ejoKCAsTExCAvL0+ZZsyYMfjiiy+wfv167Nu3DxcuXMCAAQOU8UVFRYiLi8OdO3dw4MABrFy5EitWrMDkyZONnVwiIiIiIiIiIiIiIiKzMvpjzbZt26b1fcWKFQgMDERmZiY6d+6Ma9euYdmyZVi7di26desGAFi+fDkaN26MgwcPokOHDtixYwdOnDiBnTt3IigoCC1btsT06dMxfvx4pKSkwM3NzdjJJiIiIiIiIiIiIiIiMguj3zlzr2vXrgEA/P39AQCZmZkoKChAdHS0Mk2jRo1Qp04dZGRkAAAyMjLQrFkzBAUFKdPExsYiNzcXx48fN3WSiYiIyIrVfXWr8rGlZRMRERERERERaRj9zpmSiouLMXr0aHTs2BFNmzYFAGRlZcHNzQ1+fn5a0wYFBSErK0uZpmTHjGa8Zpwu+fn5yM/PV77n5uYCAAoKClBQUGCU/JSkWaYpll0Zamcxy3ruzbe15N8STFkGjlyuRERERES2pmSn/rmZcRZMCRERERHZCpN2ziQlJeHYsWP45ptvTLkaAEBqaiqmTp1aaviOHTvg6elpsvWmp6ebbNkVMau9edbz5Zdfan23lvxbkinK4ObNm0ZfJhGRPeIdLuSoeCKYiEriPoGIiIjI9piscyY5ORlbtmzB/v37ERoaqgwPDg7GnTt3kJOTo3X3THZ2NoKDg5VpDh8+rLW87OxsZZwuEyZMwNixY5Xvubm5qF27NmJiYuDj42OsbCkKCgqQnp6OHj16wNXV1ejLr6imKdvNuj61k2B622Kryb8lmHIb0Nz5RURERERE9oOdKERERESkYfTOGRHB888/j40bN2Lv3r0IDw/XGt+mTRu4urpi165diI+PBwCcPHkS58+fR1RUFAAgKioKb775Ji5duoTAwEAAd+9O8PHxQUREhM71qtVqqNXqUsNdXV1N2nlg6uUbKr9IZZH1Wkv+LckUZeDoZUpEREQE8EQ2kaU1TdmudazJOCQiIiIyHqN3ziQlJWHt2rXYvHkzqlWrprwjxtfXFx4eHvD19cWIESMwduxY+Pv7w8fHB88//zyioqLQoUMHAEBMTAwiIiIwZMgQzJo1C1lZWZg4cSKSkpJ0dsAQERERERERERERERHZCqN3zixevBgA0LVrV63hy5cvx7BhwwAAc+bMgZOTE+Lj45Gfn4/Y2FgsWrRImdbZ2RlbtmxBYmIioqKi4OXlhYSEBEybNs3YyaUq0lxJxSuoiIiIiGzfve9xYhuPiIiIiIjINEzyWLPyuLu7Iy0tDWlpaXqnCQsLK/XyeeKjHYhMifFFRCXVfXUr1M6CWe0tnRIiIiIiskc8BiUyP8YdWROjd84QEREREZHj4AEuERERERFRxTlZOgFERESOJDU1Fe3atUO1atUQGBiIfv364eTJk1rT3L59G0lJSahRowa8vb0RHx+P7OxsrWnOnz+PuLg4eHp6IjAwEC+//DIKCwvNmRUiIiIiIiIii6n76latD5Gt4Z0zNow7HSKyJ45y5fW+ffuQlJSEdu3aobCwEK+99hpiYmJw4sQJeHl5AQDGjBmDrVu3Yv369fD19UVycjIGDBiAb7/9FgBQVFSEuLg4BAcH48CBA7h48SKGDh0KV1dXzJgxw5LZcwiOsq2S42CbkoiIiIiIyPzYOUNERGRG27Zt0/q+YsUKBAYGIjMzE507d8a1a9ewbNkyrF27Ft26dQMALF++HI0bN8bBgwfRoUMH7NixAydOnMDOnTsRFBSEli1bYvr06Rg/fjxSUlLg5uZmiawRkZWrasciOyaJTIfxRUREROR42DlDRERkQdeuXQMA+Pv7AwAyMzNRUFCA6OhoZZpGjRqhTp06yMjIQIcOHZCRkYFmzZohKChImSY2NhaJiYk4fvw4WrVqZd5MEBHpUdETzobexaNvuffOz5PcRPqxQ4iIiIjIstg5Q0REZCHFxcUYPXo0OnbsiKZNmwIAsrKy4ObmBj8/P61pg4KCkJWVpUxTsmNGM14zTpf8/Hzk5+cr33NzcwEABQUFKCgoMEp+TEntLJZZr9Pd9ZYso5JpsYWyMzdNmZiybFjuREREREREZOvYOUNERGQhSUlJOHbsGL755huTrys1NRVTp04tNXzHjh3w9PQ0+fqralZ7y64/PT1d+b9kWr788ksLpMY2lCwzY7t586bJlk2G4XtqiOxX3Ve3Qu0sFap7eRcOERERUcWxc4aIiMgCkpOTsWXLFuzfvx+hoaHK8ODgYNy5cwc5OTlad89kZ2cjODhYmebw4cNay8vOzlbG6TJhwgSMHTtW+Z6bm4vatWsjJiYGPj4+xsqWyTRN2W6R9aqdBNPbFqNHjx5wdXUtlZZjKbEWSZc1KygoQHp6ulaZGZvmzi+6qzInRdm5QmS9+H4oIiIiIsfAzhkiIiIzEhE8//zz2LhxI/bu3Yvw8HCt8W3atIGrqyt27dqF+Ph4AMDJkydx/vx5REVFAQCioqLw5ptv4tKlSwgMDARw9y4FHx8fRERE6FyvWq2GWq0uNdzV1dVkJ9CNKb9IZdH1lyynkmmxhbKzFFNuWyx361WZd8acmh5jquToXSdPWJO5GLsjlNsxEZFjS0lJKfVEhIYNG+LXX38FANy+fRvjxo3DunXrkJ+fj9jYWCxatEjrsdjnz59HYmIi9uzZA29vbyQkJCA1NRUuLjxNTGRujDoiIiIzSkpKwtq1a7F582ZUq1ZNeUeMr68vPDw84OvrixEjRmDs2LHw9/eHj48Pnn/+eURFRaFDhw4AgJiYGERERGDIkCGYNWsWsrKyMHHiRCQlJensgKGqa5qy3eIdRERERCUZ0vFz7zTG7NDhHXhERJbRpEkT7Ny5U/leslNlzJgx2Lp1K9avXw9fX18kJydjwIAB+PbbbwEARUVFiIuLQ3BwMA4cOICLFy9i6NChcHV1xYwZM8yeFyJHx84ZIiIiM1q8eDEAoGvXrlrDly9fjmHDhgEA5syZAycnJ8THx2td7aTh7OyMLVu2IDExEVFRUfDy8kJCQgKmTZtmrmyYBU/6EFWcKU/EWlpl9gncj5CtM+WdN0REZJtcXFx0Ps762rVrWLZsGdauXYtu3boBuHuc2bhxYxw8eBAdOnTAjh07cOLECezcuRNBQUFo2bIlpk+fjvHjxyMlJQVubm7mzg6RQ2PnDBERkRmJSLnTuLu7Iy0tDWlpaXqnCQsL48voiYiIyCjM1WnDx7IREVXdqVOnEBISAnd3d0RFRSE1NRV16tRBZmYmCgoKEB0drUzbqFEj1KlTBxkZGejQoQMyMjLQrFkzrcecxcbGIjExEcePH0erVq0skSUih8XOGTKKshrzbHQTERERERE5nsq8h4rHj0RE+kVGRmLFihVo2LAhLl68iKlTp6JTp044duwYsrKy4ObmBj8/P615goKClMdpZ2VlaXXMaMZrxumTn5+P/Px85Xtubi4AoKCgAAUFBTrnUTv/e2GivmmqOk/J6Sszj6HpKjltReaxV7ZeFtaUbnbOEBERERERERkJHx1mPPb8qEYiosro1auX8n/z5s0RGRmJsLAw/O9//4OHh4fJ1puamoqpU6eWGr5jxw54enrqnGdW+3//N/SpDxWdp+T0lZmnMk+jSE9Pr/A89spWy+LmzZuWToKCnTNWjg17IiIiIiIisjf6jnV5DExkON51Rn5+fnjggQdw+vRp9OjRA3fu3EFOTo7W3TPZ2dnKO2qCg4Nx+PBhrWVkZ2cr4/SZMGECxo4dq3zPzc1F7dq1ERMTAx8fH53zNE3Zrvx/LCXWoPxUdJ6S01dmHkPTBdy92yI9PR09evSAq6urwfPZI1svC82dX9aAnTNERERERHaqqic5zXGStGnKdsxqrzlQVlV4fp7IJbIujEkiIvO5ceMGzpw5gyFDhqBNmzZwdXXFrl27EB8fDwA4efIkzp8/j6ioKABAVFQU3nzzTVy6dAmBgYEA7t794OPjg4iICL3rUavVUKvVpYa7urrqPTmfX6TSms4QFZ2n5PSVmacyHQtl5dnR2GpZWFOa2TlDREREREQmxxO2RERERFXz0ksvoU+fPggLC8OFCxcwZcoUODs748knn4Svry9GjBiBsWPHwt/fHz4+Pnj++ecRFRWFDh06AABiYmIQERGBIUOGYNasWcjKysLEiRORlJSks/OFiEyLnTNEREREREREREREVu7PP//Ek08+iStXriAgIAAPPfQQDh48iICAAADAnDlz4OTkhPj4eOTn5yM2NhaLFi1S5nd2dsaWLVuQmJiIqKgoeHl5ISEhAdOmTbNUlogcGjtniIiIiIiIiMzMFu8ms8U0E9kivkuG9Fm3bl2Z493d3ZGWloa0tDS904SFheHLL780dtLsWt1Xt0LtLJjV3tIpIXvjZOkEEBERERFZyv79+9GnTx+EhIRApVJh06ZNWuNFBJMnT0atWrXg4eGB6OhonDp1Smuaq1evYvDgwfDx8YGfnx9GjBiBGzdumDEXVFF1X92qfMi6MCapLIxdIsMwVoiIbAM7Z4iIiIjIYeXl5aFFixZ6ry6cNWsW5s+fjyVLluDQoUPw8vJCbGwsbt++rUwzePBgHD9+HOnp6diyZQv279+PUaNGmSsLRHaFMUlEREREjoKPNSOT4+24REREZK169eqFXr166RwnIpg7dy4mTpyIvn37AgBWrVqFoKAgbNq0CYMGDcIvv/yCbdu24ciRI2jbti0AYMGCBejduzfeeecdhISEmC0vVHX3XmHMtqv5MSaJiIiIyFGwc4aIiIiISIezZ88iKysL0dHRyjBfX19ERkYiIyMDgwYNQkZGBvz8/JSTwAAQHR0NJycnHDp0CP3797dE0onskiljMj8/H/n5+cr33NxcAEBBQQEKCgpKTa8ZpnYSo+TN2mjyZc35K/m7NE3Zrvx/LCXW4Hl1/bb2wF7zRUREZG/YOUNEREREpENWVhYAICgoSGt4UFCQMi4rKwuBgYFa411cXODv769MowtPBP/L0ieBS5a32ln0jqvKsu3xRGnJvJkrf6aMydTUVEydOrXU8B07dsDT01PvfNPbFhucfltkzfkr+TLrki9orshLrtPT042ZJKtx8+ZNSyeBiIiIDMDOGSIiIiIiM+OJ4NIslTd9J3jvHVcV9noCGLibN3s4ETxhwgSMHTtW+Z6bm4vatWsjJiYGPj4+paYvKChAeno6Jn3nhPxilTmTahZqJ8H0tsVWnb+Sd8hU5s6Z9PR09OjRA66uriZJnyVpOvyJiIjIurFzhsjOpaSklDr507BhQ/z6668AgNu3b2PcuHFYt24d8vPzERsbi0WLFmldkXj+/HkkJiZiz5498Pb2RkJCAlJTU+Hiwl0IERHZr+DgYABAdnY2atWqpQzPzs5Gy5YtlWkuXbqkNV9hYSGuXr2qzK8LTwT/y9IngfWd4C1rnCEnfwH7PgFcMm+3bt0yyzpNGZNqtRpqtbrUcFdX1zJ/u/xiFfKL7CsmS7Lm/DWYtKPEt3/TWJFYK+/3tVX2mCciIiJ7xDOrRA6gSZMm2Llzp/K9ZKfKmDFjsHXrVqxfvx6+vr5ITk7GgAED8O233wIAioqKEBcXh+DgYBw4cAAXL17E0KFD4erqihkzZpg9L0REROYSHh6O4OBg7Nq1Sznxm5ubi0OHDiExMREAEBUVhZycHGRmZqJNmzYAgN27d6O4uBiRkZF6l80TwaVZKm8ly/ve9esbV9ETn/Z6Ahi4m7fCwkKzrMuUMUlEuqWmpmLDhg349ddf4eHhgQcffBBvvfUWGjZsqEzDC/6IiEqr++pW5f9zM+MsmBKyZqwFrVDJ4CUyBhcXF51XCl67dg3Lli3D2rVr0a1bNwDA8uXL0bhxYxw8eBAdOnTAjh07cOLECezcuRNBQUFo2bIlpk+fjvHjxyMlJQVubm7mzg4REZHR3LhxA6dPn1a+nz17FkePHoW/vz/q1KmD0aNH44033kCDBg0QHh6OSZMmISQkBP369QMANG7cGD179sTIkSOxZMkSFBQUIDk5GYMGDUJISIiFckUVwba3dWFMElmXffv2ISkpCe3atUNhYSFee+01xMTE4MSJE/Dy8gLAC/6IiIgqi50zVoIHhWRKp06dQkhICNzd3REVFYXU1FTUqVMHmZmZKCgoQHR0tDJto0aNUKdOHWRkZKBDhw7IyMhAs2bNtK56io2NRWJiIo4fP45WrVrpXGdlX3RsyRfmlnwJsCXSUZX1G6P8bDn/VVVe+dnji5ytFetDMrfvvvsODz/8sPJd86ixhIQErFixAq+88gry8vIwatQo5OTk4KGHHsK2bdvg7u6uzLNmzRokJyeje/fucHJyQnx8PObPn2/2vBDZA8YkVRWvVDaubdu2aX1fsWIFAgMDkZmZic6dO/OCPyIioipg5wyRnYuMjMSKFSvQsGFDXLx4EVOnTkWnTp1w7NgxZGVlwc3NDX5+flrzBAUFISsrCwCQlZWl1TGjGa8Zp09lX3RsyRfmlnwJsLFeAGzu9Vel/Owh/1Wlr/zs4UXHRKRb165dISJ6x6tUKkybNg3Tpk3TO42/vz/Wrl1riuQRORzGJJF1u3btGoC7cQbAZBf8VfZiP7WTaH0Hyr4IzJALxCozv6EXnllqfmu4ONKWVLW8WM5EpA87Z4jsXK9evZT/mzdvjsjISISFheF///sfPDw8TLbeyr7o2JIvzK3Mi36tZf3GKD9bzn9VlVd+moNBonvde6cPr9Alsi+8m4+I6F/FxcUYPXo0OnbsiKZNmwKAyS74q+zFftPbFgPQvtirrIvADLlArDLzG3rhmaXnt+TFkbaosuXFi/2ISB92zpBZ8RZzy/Pz88MDDzyA06dPo0ePHrhz5w5ycnK0GtPZ2dnKO2qCg4Nx+PBhrWVkZ2cr4/Sp7IuOLfnC3Kq86Nda1l+V8rOH/FeVvvKz15c4ExEREREZKikpCceOHcM333xj8nVV9mK/Sd85Ib9YpXWxV1kXgRlygVhl5jf0wjNLzW8NF0fakqqWFy/2IyJ92DlD5GBu3LiBM2fOYMiQIWjTpg1cXV2xa9cuxMfHAwBOnjyJ8+fPIyoqCgAQFRWFN998E5cuXUJgYCCAu1eL+Pj4ICIiwmL5ICIiIiIiIvNITk7Gli1bsH//foSGhirDg4ODTXLBX2Uv9ssvViG/SKU1TVkXgRlygVhl5jf0wjNzz6+5YFbtLJjV3rIXR9qiypYXy5iI9HGydAKIyLReeukl7Nu3D+fOncOBAwfQv39/ODs748knn4Svry9GjBiBsWPHYs+ePcjMzMTw4cMRFRWFDh06AABiYmIQERGBIUOG4Mcff8T27dsxceJEJCUl6WwsExERERERkX0QESQnJ2Pjxo3YvXs3wsPDtcaXvOBPQ9cFfz///DMuXbqkTMML/oiIiEzQObN//3706dMHISEhUKlU2LRpk9Z4EcHkyZNRq1YteHh4IDo6GqdOndKa5urVqxg8eDB8fHzg5+eHESNG4MaNG8ZOKpFD+PPPP/Hkk0+iYcOGeOKJJ1CjRg0cPHgQAQEBAIA5c+bgkUceQXx8PDp37ozg4GBs2LBBmd/Z2RlbtmyBs7MzoqKi8PTTT2Po0KFlvoSViIiIiIiIbF9SUhI++ugjrF27FtWqVUNWVhaysrJw69YtAOAFf0RERFVg9Mea5eXloUWLFnjmmWcwYMCAUuNnzZqF+fPnY+XKlQgPD8ekSZMQGxuLEydOwN3dHQAwePBgXLx4Eenp6SgoKMDw4cMxatQorF271tjJJbJ769atK3O8u7s70tLSkJaWpneasLCwMl8iSERERERERPZn8eLFAICuXbtqDV++fDmGDRsG4O4Ff05OToiPj0d+fj5iY2OxaNEiZVrNBX+JiYmIioqCl5cXEhISeMEfEVEZ+N5ux2D0zplevXqhV69eOseJCObOnYuJEyeib9++AIBVq1YhKCgImzZtwqBBg/DLL79g27ZtOHLkCNq2bQsAWLBgAXr37o133nkHISEhxk4yERERkdGxMU1ERES2TkTKnYYX/BEREVWOWd85c/bsWWRlZSE6OloZ5uvri8jISGRkZAAAMjIy4Ofnp3TMAEB0dDScnJxw6NAhcyaXiIiIiIiIiIiIiIjI6Ix+50xZsrKyAABBQUFaw4OCgpRxWVlZCAwM1Brv4uICf39/ZRpd8vPzkZ+fr3zPzc0FABQUFKCgoMAo6S9Js0xjLVvtXP7VKNZE7SRafyvDFL+LORl7G9C1bCIie1fy7hIiIlvBO+OIiIiIiKiqzNo5Y0qpqamYOnVqqeE7duyAp6enydabnp5ulOXMam+UxZjd9LbFlZ7XXm5pNtY2UNLNmzeNvkwiIjI9djYROR521BARERERUWWYtXMmODgYAJCdnY1atWopw7Ozs9GyZUtlmkuXLmnNV1hYiKtXryrz6zJhwgSMHTtW+Z6bm4vatWsjJiYGPj4+RszFXQUFBUhPT0ePHj3g6upa5eU1TdluhFSZj9pJML1tMSZ954T8YlWVl3csJdYIqTIvY28DJWnu/CIi+7N//368/fbbyMzMxMWLF7Fx40b069dPGS8imDJlCpYuXYqcnBx07NgRixcvRoMGDZRprl69iueffx5ffPGF8vLVefPmwdvb2wI5IiIiIiIiIiKiijJr50x4eDiCg4Oxa9cupTMmNzcXhw4dQmJiIgAgKioKOTk5yMzMRJs2bQAAu3fvRnFxMSIjI/UuW61WQ61Wlxru6upq9BPnplh+flHVOzgsIb9YZZS0m/I3MjVTbGO2XB5EVLa8vDy0aNECzzzzDAYMGFBq/KxZszB//nysXLkS4eHhmDRpEmJjY3HixAm4u7sDAAYPHoyLFy8iPT0dBQUFGD58OEaNGoW1a9eaOztERERERERERFQJRu+cuXHjBk6fPq18P3v2LI4ePQp/f3/UqVMHo0ePxhtvvIEGDRooJ51CQkKUq4YbN26Mnj17YuTIkViyZAkKCgqQnJyMQYMGISQkxNjJJSIiMqtevXqhV69eOseJCObOnYuJEyeib9++AIBVq1YhKCgImzZtwqBBg/DLL79g27ZtOHLkCNq2bQsAWLBgAXr37o133nmHdSURERHR/3fv40b56EEiw/CRnURE5mH0zpnvvvsODz/8sPJd86ixhIQErFixAq+88gry8vIwatQo5OTk4KGHHsK2bduUq4EBYM2aNUhOTkb37t2Vx7XMnz/f2EklIiKyKmfPnkVWVhaio6OVYb6+voiMjERGRgYGDRqEjIwM+Pn5KR0zABAdHQ0nJyccOnQI/fv317ns/Px85OfnK981j08sKChAQUGBiXJUPrWzWGzdhlA7idbfyrJkGZubJq+mzLMjlSfZtqYp2zGr/d2/J998xNLJISIiIiIiK2L0zpmuXbtCRP8JDJVKhWnTpmHatGl6p/H393eIR7PwpcFEpTVN2Y78IhWvziGHlJWVBQAICgrSGh4UFKSMy8rKQmBgoNZ4FxcX+Pv7K9PokpqaiqlTp5YavmPHDnh6elY16ZU2q73FVl0h09sWV2n+L7/80kgpsR3p6ekmW/bNmzdNtmwiIiIiImuVmpqKDRs24Ndff4WHhwcefPBBvPXWW2jYsKEyTdeuXbFv3z6t+f7zn/9gyZIlyvfz588jMTERe/bsgbe3NxISEpCamgoXF7O+AYPI4THiiIiIHMCECROUu1mBu3fO1K5dGzExMfDx8bFYupqmbLfYug2hdhJMb1uMSd85Ib+48u9YO5YSa8RUWbeCggKkp6ejR48eJnuHmubOLyIioorQXCCpdhabuUCEiKikffv2ISkpCe3atUNhYSFee+01xMTE4MSJE/Dy8lKmGzlypNaF8SUvyCsqKkJcXByCg4Nx4MABXLx4EUOHDoWrqytmzJhh1vwQOTp2zhAREVmJ4OBgAEB2djZq1aqlDM/OzkbLli2VaS5duqQ1X2FhIa5evarMr4tarYZarS413NXV1WQn0PXRvnO08h0e5pRfrEJ+UeXTau4ytgam3LYcsTyJiIiIiLZt26b1fcWKFQgMDERmZiY6d+6sDPf09NR7fLhjxw6cOHECO3fuRFBQEFq2bInp06dj/PjxSElJgZubm0nzQET/YucMERGRlQgPD0dwcDB27dqldMbk5ubi0KFDSExMBABERUUhJycHmZmZaNOmDQBg9+7dKC4uRmRkpKWSTkREREREdu7ex/PzceSWd+3aNQB3XxFR0po1a/DRRx8hODgYffr0waRJk5S7ZzIyMtCsWTOtx2nHxsYiMTERx48fR6tWrUqtpzLvMC35flFD3xlZ0XnufYdpReepSLo07yE1VV6MPb8pmeM9o6ZkTelm5wwREZEZ3bhxA6dPn1a+nz17FkePHoW/vz/q1KmD0aNH44033kCDBg0QHh6OSZMmISQkBP369QMANG7cGD179sTIkSOxZMkSFBQUIDk5GYMGDUJISIiFckUVUfKglge0RERERERUGcXFxRg9ejQ6duyIpk2bKsOfeuophIWFISQkBD/99BPGjx+PkydPYsOGDQDuvsdU13tONeN0qcw7TEs+PtLQd3BWdJ57H1FZ0Xkqky5D361ZmfUYc35zMOV7Rk3Jmt5hys4ZIiIiM/ruu+/w8MMPK98174FJSEjAihUr8MorryAvLw+jRo1CTk4OHnroIWzbtg3u7u7KPGvWrEFycjK6d+8OJycnxMfHY/78+WbPCxERGY4ds0RERGRMSUlJOHbsGL755hut4aNGjVL+b9asGWrVqoXu3bvjzJkzqF+/fqXWVZl3mJZ8v6ih7+Cs6Dz3vsO0ovNUJF2a95Ea+m7NyqzHmPObkjneM2pK1vQOU3bOmNm9t4ASEZFj6dq1K0RE73iVSoVp06ZpvbzxXv7+/li7dq0pkkcmwvqfiIiIiIiMJTk5GVu2bMH+/fsRGhpa5rSax1+fPn0a9evXR3BwMA4fPqw1TXZ2NgDofU9NZd5hWvKdnYaewK/oPPe+F7Si81Q2XaZaT1XnN/fFQJZ4h60xWFOa2TlDRERERERkBPd2xKqdLZQQIjJI05TtyC9S8W42IrIZIoLnn38eGzduxN69exEeHl7uPEePHgUA1KpVC8Dd95i++eabuHTpEgIDAwHcfTyVj48PIiIiTJZ2IiqNnTNkFfiYByIiIiIiIiIi28TzOuaRlJSEtWvXYvPmzahWrZryjhhfX194eHjgzJkzWLt2LXr37o0aNWrgp59+wpgxY9C5c2c0b94cABATE4OIiAgMGTIEs2bNQlZWFiZOnIikpCSdd8cQkemwc4aIiByW5gBC7SylXiRIREREREREZE0WL14M4O7jsktavnw5hg0bBjc3N+zcuRNz585FXl4eateujfj4eEycOFGZ1tnZGVu2bEFiYiKioqLg5eWFhISEMh+tTUSmwc4ZIiIiIiIiIiIiIitX1vtLAaB27drYt29fucsJCwvDl19+aaxkEVElsXOGiIiIiIjIjPjoFyLrwpgkIiIiS3CydAKIiIiIiIiIiIiIiIgcCTtniIiIiIiIiIiIiIiIzIidM0RERERERERERERERGbEzhkiIiIiIiIiIiIiIiIzcrF0AoiIiIiIiIiIrEHdV7cq/5+bGWfBlBAREZG9Y+eMiZVs2JFhyiozNo6JiIiIyF7d2w5m25eIiBwFO0aJyBGxc4aIiIhMjhcr6MYTsURERERERESOiZ0zZFN4JQURERER2RN2XhMRkaPghUlERNrYOUNERERERERERERE5EDYYWp5TpZOABERERERERERERERkSNh5wwREREREREREREREZEZ8bFmZLP4/hkiIuvG9ygQEVUN27tERET/4iOYiMje8M4ZIiIiIiIiIiIiIiIiM+KdM0RERGQ0vFuGiIiI7AWv0iciIiJTYucMERERkZXgI4yIiIiIiIiIHAM7Z0yAVw0TERGROfCKXiIiIvPhRRREROTo6r66FWpnwaz2lk6JfWDnDBEREZEN4UUgRERERERERLaPnTNEREREVo4dMkSkbz/Aq/eJLIN30RAREVFVsXPGSHjSxLLKKn82lImIyBaxbUFERERERERkv9g5Q3aPVzQREREREREREdkvnvshIlvEzhkiIiIiO8GDUiIiIiIiIiLbwM4ZIiIiqjQ+eouIyLLYKUtkeYxDIiIiqgx2zpTj3pNO9za0mqZsR36RypxJoipgo5mIiBwF6zwiIiIiIiIi6+Vk6QSUJS0tDXXr1oW7uzsiIyNx+PBhSyeJ7EjdV7fq/JB+jEki68KYJLIujEmyNLZrtTEmiawLY5IsgfWifoxJMhfGoX5We+fMJ598grFjx2LJkiWIjIzE3LlzERsbi5MnTyIwMNCk6y5rQ9GMUzsLZrU3aTKIrIolY5KISrPWepKsE++iMT3Wk2TtHG0/wJgkS3G0WDMUY5KsnaPFLmOSyDpYbefM7NmzMXLkSAwfPhwAsGTJEmzduhUffvghXn31VQunjhyJvpOQp6bHmDkllsWYJLIu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hAMBiYiIiMwHO2dIdir7g+Pq4mgD5sT8cboWIiKydJwagoiIiIiIiIyBnTNEZo7TtViOsh2b7MgkIiIiIiIiIiKSL3bOEJk5TtdCREREREREREREJC/snCEyc5yuhYiIiB5lic+t4B2mROaFMU1ERESmjp0zRERERERERERERERmgoMYTAM7Z4iIzNyjo6NZKRMRERERERERERmXtbEzQEREREREREREREREZEl45wwRERERERERmSxO3UJERESmiJ0zRERERERERERERCR7j07dTmTKOK0ZERERERERERERERGRAfHOGZIF9noTERERERERERERkaVg5wwREREREVkUPp+CTEnI3DQoi62MnQ0iIiIi0jN2zhARERERWQhe5CUiIiIiIpIHds4QkVmy9KnyLL38RERERERERESWpKJrQbxrXL7YOUMmiycWIiIiIqottimJiIiIiMgY2DlDJoV3AxARERERERERERGRqWPnDBGZDXbeERERUW082pbgnTREpo0xTURERHJmbewMEBERERERERERERERWRLeOVMLnJ+aiMwJz2lERERERERERESGwc4ZIiILw04YIiIiIrJEbAcTEZkmTmOvP6wL5YWdM2SWQuamQVlsBYAnGiIiIiIiMh3qiyb2NgJLuxg5MyaIF/CIiIjIVLBzRk/YACQiIiIiY+PDr/WLIwvJUPj3JBEREZHlYecMEREREZGZ4gh8IiLt2PlKRCRvZWfFITJX7JwhIpPGUYZERERERFQb7KghIiJifWgM1sbOABERERERERERERERkSXhnTNERFROZXckcfQEEREREREREelbkzd3cjpesijsnCGzwPnUiWqG08IRERERGQfbYURERESWjZ0zVWCD2fRV9B1y9D8RERER6YpzcBMRERHVHttU8lHZdW9+T4bBzhkiMinsMDU+VtBERGTpWBdSTbEtS0RERERq7Jwhi8U/qomIiMgc8GIvEVHdKHt+5RTaRET6x3YsWTp2zhARERERmRj+IStPIXPTsLRL6b/KYisOACIiIiIik8cB7nXH2tgZqExiYiKaNGkCBwcHdO3aFT/88IOxs0RmqsmbO3V6WTpjxSS/A/nid2NcrCeJ5IUxaZkqqwtZTxoXY5JqgnFbdxiTRPLCmKSaYD2pX7K9c+bLL79EQkIC1q5di65du2LlypWIiorCpUuX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6KGHjJycHCM/P994//33jWuuucaQZPzyl780z+HuPD755JPGmjVr6n181c9V1Z958+a5LE3utmrVKiMkJMRYvny5sXv3biMtLc2IjIw0CgoK7E6aV7hY3cWFTZ482YiIiDA+/PBD4/Dhw+bP6dOn7U6a12hom5iUlGQkJSXZnOqG84d2srrGtJudO3c2zpw5Y57D2/Ls7Xy9PvpTPaT+eS76rk1D37Vp6Lu6hq+3l/XhT21qfdH2up8/1D1/rVvUn8bzmuBM//79jU6dOhmSjH379tmalrvuusto166dERwcbPzkJz8x7rrrLmP//v3m/h9++MH41a9+ZbRq1cpo0aKF0aZNGyMuLs547bXXjNdee81YsGCB0bt3b0OS8eijj7o0bTExMca4ceMa/L4PPvig1pv8qamphmEYRkVFhfH4448bMTExRkhIiDF48GBj7969Tuc4evSoGRwKDw83JkyYYJw8edIV2XKJC+Xx9OnTxtChQ422bdsaQUFBRseOHY1JkyYZkoz09HTzHO7OY1hYmFnm9SHJGDJkiPnZqvzZuXOny9JkhRdeeMHo0KGDERwcbPTt29fYsWOH3UnyGheru7iwugKcy5YtsztpXqOhbeLtt99uHD582MYUN44/tJPVNabdrH5z0tvy7O18vT76Uz2k/nk2+q6NR9+1aei7uoavt5f14U9tan3R9rqfP9Q9f61b1J/GcxiGYVxkco3t8vPzddlll+nNN9/UL37xC6Wnp2vmzJl2J6vebrjhBn3//ffauXOnue306dPq0qWLjh8/ruPHjysoKKjR5z937pwqKioUHBysgIAA/epXv9Lvf/97VyRdZ86cMc/rjxwOh9LT011WnhfTsmVL3XHHHVq+fHm9jrc6fQAAAAAAAACApvOKO+4rVqxQq1atNGLECN1xxx1asWKF0/7FixcrMDDQ6aFRv/vd7+RwOJSZmWluKy8v1yWXXKJHH33U3Pbcc8+pf//+at26tZo3b66EhAT97W9/czr/9ddfr169etWati5duiglJaXBeWrRooX69eunkpISfffdd5KkoqIiTZkyRe3bt1dISIh++tOf6plnnlFFRYX5vgMHDsjhcOi5557TwoULdfnllyskJERLliyRw+GQYRjKysqSw+GQw+Ew3/fPf/5Td955p6Kiosxrr1+/3ilNH374oRwOh1atWqXp06frJz/5iVq0aKHi4mLdd999atmypQ4ePKhbbrlFLVu21E9+8hNlZWVJkr7++mvddNNNCgsLU8eOHbVy5Uqncx87dkwPPfSQevTooZYtWyo8PFzDhw/X//7v/9aahr/+9a968skndemllyo0NFSDBw82HxJVVW5urm6++Wa1atVKYWFh6tmzpxYtWuR0zJ49e3THHXcoKipKoaGh6tOnj95+++0G/83q8tZbb2nEiBGKi4tTSEiILr/8cs2dO1fl5eVOx+3bt09jxoxRbGysQkNDdemll2rs2LE6ceKEpPOBlpKSEr3yyivm3+++++6rVxp++OEHnTlzxmV5AgAAAAAAAAC4TzO7E1AfK1as0OjRoxUcHKy7775bL774oj799FNde+21kqSBAweqoqJCH330kW655RZJ0rZt2xQQEKBt27aZ5/niiy906tQpDRo0yNy2aNEi3XrrrRo3bpzOnj2rVatW6c4779S6des0YsQISdL48eM1adIk7dy5U927dzff++mnn+r//u//NH369Ebl65///KcCAwMVGRmp06dP6/rrr9e3336rX/ziF+rQoYO2b9+uadOm6fDhw1q4cKHTe5ctW6YzZ84oLS1NISEhuuaaa/Taa69p/PjxGjJkiO69917z2MLCQvXv31+nT5/WAw88oNatW+uVV17Rrbfeqr/97W+6/fbbnc49d+5cBQcH66GHHlJpaamCg4MlnQ9uDR8+XIMGDdL8+fO1YsUKZWRkKCwsTI899pjGjRun0aNHa+nSpbr33nuVlJRkPqDwn//8p9auXas777xT8fHxKiws1B/+8Addf/312r17t+Li4pzS8PTTTysgIEAPPfSQTpw4ofnz52vcuHHKzc01j8nOztYtt9yidu3a6de//rViY2P1zTffaN26dfr1r38tSdq1a5euu+46/eQnP9HUqVMVFhamv/71rxo1apT+/ve/18h7YyxfvlwtW7ZUZmamWrZsqc2bN2vGjBkqLi7Ws88+K0k6e/asUlJSVFpaqvvvv1+xsbH69ttvtW7dOhUVFSkiIkKvvfaa/vu//1t9+/ZVWlqaJOnyyy+v1/WXLFkiwzDUtWtXTZ8+Xffcc0+T8wUAAAAAAAAAcBN7V1W7uM8++8yQZGRnZxuGcX5tvksvvdT49a9/bR5TXl5uhIeHG4888oh5TOvWrY0777zTCAwM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13Xw4EGnmTM//PCDFi9erMsvv1zt2rUzrxEYGCiHw2E+u0aSDhw4oLVr19aapvHjx+v48eP6xS9+oVOnTplLV7nCz372M+Xk5Oi9996rsa+oqEjnzp1r9LlvvvlmffLJJ+azdySppKREf/zjH9WpUyd169at0eeur8DAwBqzXlavXt3oZ75cc801io+P18KFC1VUVOS0r/I60dHRuuGGG/SHP/xBhw8frnGO7777rlHXrqoyOFc1b2fPntWSJUucjisuLq7xN+zRo4cCAgJUWlpqbgsLC6uRn7rUlv6TJ09q4cKFatOmjRISEuqbDQAAAAAAAACAhTx25szbb7+tkydP6tZbb611f79+/dS2bVutWLFCd911l6TzgZinn35aERER6tGjh6TzN+i7dOmivXv36r777nM6x4gRI7RgwQINGzZM99xzj44cOaKsrCz99Kc/1VdffVXjmldffbW6d++u1atXq2vXrrrmmmtclt+HH35Yb7/9tm655Rbdd999SkhIUElJib7++mv97W9/04EDBxo1w0SSpk6dqtdff13Dhw/XAw88oKioKL3yyivKz8/X3//+dwUEuD9Gd8stt2jOnDmaMGGC+vfvr6+//lorVqwwZ7c0VEBAgF588UWNHDlSvXv31oQJE9SuXTvt2bNHu3btMoNcWVlZGjBggHr06KFJkybpsssuU2FhoXJycvSf//xH//u//3vRa3322WfmzJaqbrjhBvXv31+tWrVSamqqHnjgATkcDr322ms1AlGbN29WRkaG7rzzTl1xxRU6d+6cXnvtNQUGBmrMmDHmcQkJCXr//fe1YMECxcXFKT4+XomJibWmKysrS2vXrtXIkSPVoUMHHT58WC+//LIOHjyo1157TcHBwQ0pUgAAAAAAAACARTw2OLNixQqFhoZqyJAhte4PCAjQiBEjtGLFCh09elStW7c2gzP9+/d3CjgMHDhQe/fudXrejCTddNNNeumll/T0009rypQpio+P1zPPPKMDBw7UGpyRpHvvvVePPPKIxo8f77rMSmrRooW2bNmip556SqtXr9arr76q8PBwXXHFFZo9e7YiIiIafe6YmBht375djz76qF544QWdOXNGPXv21DvvvKMRI0a4MBd1++1vf6uSkhKtXLlSb7zxhq655hqtX79eU6dObfQ5U1JS9MEHH2j27Nn63e9+p4qKCl1++eWaNGmSeUy3bt302Wefafbs2Vq+fLmOHj2q6OhoXX311ZoxY0a9rpObm6vc3Nwa2+fOnasBAwZo3bp1+s1vfqPp06erVatW+q//+i8NHjzY6Tk3vXr1UkpKit555x19++23atGihXr16qX/+Z//Ub9+/czjFixYoLS0NE2fPl0//PCDUlNT6wzOXHfdddq+fbv+/Oc/6+jRowoLC1Pfvn318ssv66abbqpvMQIAAAAAAAAALOYwGvKEdWjRokV68MEHdeDAAXXo0MHu5AAAAAAAAAAAAC9DcKYBDMNQr1691Lp1a33wwQd2JwcAAAAAAAAAAHghj13WzJOUlJTo7bff1gcffKCvv/5ab731lt1JAgAAAAAAAAAAXoqZM/Vw4MABxcfHKzIyUr/61a/05JNP2p0kAAAAAAAAAADgpQjOAAAAAAAAAAAAWCjA7gQAAAAAAAAAAAD4E4IzAAAAAAAAAAAAFmpmdwLcpaKiQocOHdIll1wih8Nhd3KABjEMQydPnlRcXJwCAoihAgAAAAAAAIAv8dngzKFDh9S+fXu7kwE0yb///W9deumldicDAAAAAAAAAOBCPhucueSSSySdv7kdHh5eY39ZWZk2btyooUOHKigoyOrkeT3Kr2kuVn7FxcVq3769+TkGAAAAAAAAAPgOnw3OVC5lFh4eXmdwpkWLFgoPDye40AiUX9PUt/xYkg8AAAAAAAAAfA8PswAAAAAAAAAAALAQwRkAAAAAAAAAAAALEZwBAAAAAAAAAACwkM8+cwaer9PU9ebvB54eYWNKAAAAAAAAAACwDjNnAAAAAAAAAAAALERwBgAAAAAAAAAAwEIEZwAAAAAAAAAAACxEcAYAAAAAAAAAAMBCBGcAAAAAAAAAAAAsRHAGAAAAAAAAAADAQgRnAAAAAAAAAAAALERwBgAAAAAAAAAAwEIEZwAAAAAAAAAAACxEcAYAAAAAAAAAAMBCzexOAOzTaep68/cDT4+wMSUAAAAAAAAAAPgPZs4AAAAAAAAAAABYiOAMAAAAAAAAAACAhQjOAAAAAAAAAAAAWIjgDAAAAAAAAAAAgIUIzgAAAAAAAAAAAFiowcGZrVu3auTIkYqLi5PD4dDatWud9huGoRkzZqhdu3Zq3ry5kpOTtW/fPqdjjh07pnHjxik8PFyRkZGaOHGiTp065XTMV199pYEDByo0NFTt27fX/PnzG547AAAAAAAAAAAAD9Pg4ExJSYl69eqlrKysWvfPnz9fixcv1tKlS5Wbm6uwsDClpKTozJkz5jHjxo3Trl27lJ2drXXr1mnr1q1KS0sz9xcXF2vo0KHq2LGj8vLy9Oyzz2rWrFn64x//2IgsAgAAAAAAAAAAeI5mDX3D8OHDNXz48Fr3GYahhQsXavr06brtttskSa+++qpiYmK0du1ajR07Vt988402bNigTz/9VH369JEkvfDCC7r55pv13HPPKS4uTitWrNDZs2f18ssvKzg4WFdddZW+/PJLLViwwCmIAwAAAAAAAAAA4G1c+syZ/Px8FRQUKDk52dwWERGhxMRE5eTkSJJycnIUGRlpBmYkKTk5WQEBAcrNzTWPGTRokIKDg81jUlJStHfvXh0/ftyVSQYAAAAAAAAAALBUg2fOXEhBQYEkKSYmxml7TEyMua+goEDR0dHOiWjWTFFRUU7HxMfH1zhH5b5WrVrVuHZpaalKS0vN18XFxZKksrIylZWV1Ti+cltt+/xFSKBh/t7QcnBF+TXl+t7uYuXnb+UBAAAAAAAAAP7EpcEZO82bN0+zZ8+usX3jxo1q0aJFne/Lzs52Z7I82vy+P/7+7rvvNuocTSk/V1zf29VVfqdPn7Y4JQAAAAAAAAAAq7g0OBMbGytJKiwsVLt27czthYWF6t27t3nMkSNHnN537tw5HTt2zHx/bGysCgsLnY6pfF15THXTpk1TZmam+bq4uFjt27fX0KFDFR4eXuP4srIyZWdna8iQIQoKCmpgTn1D91nvmb/vnJXSoPe6ovyacn1vd7Hyq5z5BQAAAAAAAADwPS4NzsTHxys2NlabNm0ygzHFxcXKzc3V5MmTJUlJSUkqKipSXl6eEhISJEmbN29WRUWFEhMTzWMee+wxlZWVmTeus7Oz1aVLl1qXNJOkkJAQhYSE1NgeFBR0weDBxfb7stJyh/l7Y8ugKeXniut7u7rKz1/LAwAAAAAAAAD8QUBD33Dq1Cl9+eWX+vLLLyVJ+fn5+vLLL3Xw4EE5HA5NmTJFTzzxhN5++219/fXXuvfeexUXF6dRo0ZJkrp27aphw4Zp0qRJ+uSTT/Txxx8rIyNDY8eOVVxcnCTpnnvuUXBwsCZOnKhdu3bpjTfe0KJFi5xmxgAAAAAAAAAAAHijBs+c+eyzz3TjjTearysDJqmpqVq+fLkeeeQRlZSUKC0tTUVFRRowYIA2bNig0NBQ8z0rVqxQRkaGBg8erICAAI0ZM0aLFy8290dERGjjxo1KT09XQkKC2rRpoxkzZigtLa0peQUAAAAAAAAAALBdg4MzN9xwgwzDqHO/w+HQnDlzNGfOnDqPiYqK0sqVKy94nZ49e2rbtm0NTR4AAAAAAAAAAIBHa/CyZgAAAAAAAAAAAGg8gjMAAAAAAAAAAAAWIjgDAAAAAAAAAABgIYIzAAAAAAAAAAAAFiI4AwAAAAAAAAAAYCGCMwAAAAAAAAAAABYiOAMAAAAAAAAAAGAhgjMAAAAAAAAAAAAWIjgDAAAAAAAAAABgIYIzAAAAAAAAAAAAFiI4AwAAAAAAAAAAYCGCMwAAAAAAAAAAABYiOAMAAAAAAAAAAGAhgjMAAAAAAAAAAAAWIjgDAAAAAAAAAABgIYIzAAAAAAAAAAAAFmpmdwIAu3Saut78/cDTI2xMCQAAAAAAAADAnzBzBgAAAAAAAAAAwEIEZwAAAAAAAAAAACxEcAYAAAAAAAAAAMBCBGcAAAAAAAAAAAAsRHAGAAAAAAAAAADAQgRnAAAAAAAAAAAALERwBgAAAAAAAAAAwEIEZwAAAAAAAAAAACzUzO4E+LNOU9ebvx94eoSNKQEAAAAAAAAAAFZh5gwAAAAAAAAAAICFCM4AAAAAAAAAAABYiOAMAAAAAAAAAACAhQjOAAAAAAAAAAAAWIjgDAAAAAAAAAAAgIUIzgAAAAAAAAAAAFiI4AwAAAAAAAAAAICFCM4AAAAAAAAAAABYiOAMAAAAAAAAAACAhQjOAAAAAAAAAAAAWIjgDAAAAAAAAAAAgIUIzgAAAAAAAAAAAFiI4AwAAAAAAAAAAICFCM4AAAAAAAAAAABYiOAMAAAAAAAAAACAhVwenJk1a5YcDofTz5VXXmnuP3PmjNLT09W6dWu1bNlSY8aMUWFhodM5Dh48qBEjRqhFixaKjo7Www8/rHPnzrk6qQAAAAAAAAAAAJZr5o6TXnXVVXr//fd/vEizHy/z4IMPav369Vq9erUiIiKUkZGh0aNH6+OPP5YklZeXa8SIEYqNjdX27dt1+PBh3XvvvQoKCtJTTz3ljuQCAAAAAAAAAABYxi3BmWbNmik2NrbG9hMnTuill17SypUrddNNN0mSli1bpq5du2rHjh3q16+fNm7cqN27d+v9999XTEyMevfurblz5+rRRx/VrFmzFBwc7I4kAwAAAAAAAAAAWMItz5zZt2+f4uLidNlll2ncuHE6ePCgJCkvL09lZWVKTk42j73yyivVoUMH5eTkSJJycnLUo0cPxcTEmMekpKSouLhYu3btckdyAQAAAAAAAAAALOPymTOJiYlavny5unTposOHD2v27NkaOHCgdu7cqYKCAgUHBysyMtLpPTExMSooKJAkFRQUOAVmKvdX7qtLaWmpSktLzdfFxcWSpLKyMpWVldU4vnJbbfusEhJomL/bkY6mXN8V5efN+W+qi5WfnZ9LAAAAAAAAAIB7OQzDMC5+WOMVFRWpY8eOWrBggZo3b64JEyY4BVEkqW/fvrrxxhv1zDPPKC0tTf/617/03nvvmftPnz6tsLAwvfvuuxo+fHit15k1a5Zmz55dY/vKlSvVokUL12YKcLPTp0/rnnvu0YkTJxQeHm53cgAAAAAAAAAALuSWZ85UFRkZqSuuuEL79+/XkCFDdPbsWRUVFTnNniksLDSfURMbG6tPPvnE6RyFhYXmvrpMmzZNmZmZ5uvi4mK1b99eQ4cOrfXmdllZmbKzszVkyBAFBQU1JYuN1n3WjwGonbNSvOr6rig/b85/U12s/CpnfgEAAAAAAAAAfI/bgzOnTp3SP/7xD40fP14JCQkKCgrSpk2bNGbMGEnS3r17dfDgQSUlJUmSkpKS9OSTT+rIkSOKjo6WJGVnZys8PFzdunWr8zohISEKCQmpsT0oKOiCwYOL7Xen0nKHUzq88fpNKT9fyH9T1VV+dqUHAAAAAAAAAOB+Lg/OPPTQQxo5cqQ6duyoQ4cOaebMmQoMDNTdd9+tiIgITZw4UZmZmYqKilJ4eLjuv/9+JSUlqV+/fpKkoUOHqlu3bho/frzmz5+vgoICTZ8+Xenp6bUGXwAAAAAAAAAAALyJy4Mz//nPf3T33Xfr6NGjatu2rQYMGKAdO3aobdu2kqTnn39eAQEBGjNmjEpLS5WSkqIlS5aY7w8MDNS6des0efJkJSUlKSwsTKmpqZozZ46rkwoAAAAAAAAAAGA5lwdnVq1adcH9oaGhysrKUlZWVp3HdOzYUe+++66rkwYAAAAAAAAAAGC7ALsTAAAAAAAAAAAA4E8IzgAAAAAAAAAAAFiI4AwAAAAAAAAAAICFCM4AAAAAAAAAAABYiOAMAAAAAAAAAACAhQjOAAAAAAAAAAAAWIjgDAAAAAAAAAAAgIUIzgAAAAAAAAAAAFiI4AwAAAAAAAAAAICFCM4AAAAAAAAAAABYyO+DM91nvadOU9fbnQwAAAAAAAAAAOAn/D44AwAAAAAAAAAAYCWCMwAAAAAAAAAAABYiOAMAAAAAAAAAAGAhgjMAAAAAAAAAAAAWamZ3AgB/0mnqeklSSKCh+X1tTgwAAAAAAAAAwBbMnAEAAAAAAAAAALAQwRkAAAAAAAAAAAALEZwBAAAAAAAAAACwEMEZAAAAAAAAAAAACxGcAQAAAAAAAAAAsBDBGQAAAAAAAAAAAAsRnAEAAAAAAAAAALAQwRkAAAAAAAAAAAALEZwBAAAAAAAAAACwEMEZAAAAAAAAAAAACxGcAQAAAAAAAAAAsBDBGQAAAAAAAAAAAAsRnAEAAAAAAAAAALAQwRkAAAAAAAAAAAALEZwBAAAAAAAAAACwEMEZAAAAAAAAAAAACxGcAQAAAAAAAAAAsBDBGQAAAAAAAAAAAAsRnAEAAAAAAAAAALAQwRkAAAAAAAAAAAALEZwBAAAAAAAAAACwEMEZAAAAAAAAAAAACxGcAQAAAAAAAAAAsBDBGQAAAAAAAAAAAAsRnAEAAAAAAAAAALCQRwdnsrKy1KlTJ4WGhioxMVGffPKJ3UkCAAAAAAAAAABoEo8NzrzxxhvKzMzUzJkz9fnnn6tXr15KSUnRkSNH7E4aAAAAAAAAAABAo3lscGbBggWaNGmSJkyYoG7dumnp0qVq0aKFXn75ZbuTBgAAAAAAAAAA0GjN7E5Abc6ePau8vDxNmzbN3BYQEKDk5GTl5OTU+p7S0lKVlpaar0+cOCFJOnbsmMrKymocX1ZWptOnT6tZWYDKKxw6evSoi3Nxcc3OlZi/e9v1K8vv6NGjCgoKsvz6rmDH9Suv2azC0OnTFXWW38mTJyVJhmFYki4AAAAAAAAAgHU8Mjjz/fffq7y8XDExMU7bY2JitGfPnlrfM2/ePM2ePbvG9vj4+Hpds83vGp5OV+L6/nf9e+pxzMmTJxUREeH2tAAAAAAAAAAArOORwZnGmDZtmjIzM83XFRUVOnbsmFq3bi2Hw1Hj+OLiYrVv317//ve/FR4ebmVSfQLl1zQXKz/DMHTy5EnFxcXZkDoAAAAAAAAAgDt5ZHCmTZs2CgwMVGFhodP2wsJCxcbG1vqekJAQhYSEOG2LjIy86LXCw8MJLjQB5dc0Fyo/ZswAAAAAAAAAgG8KsDsBtQkODlZCQoI2bdpkbquoqNCmTZuUlJRkY8oAAAAAAAAAAACaxiNnzkhSZmamUlNT1adPH/Xt21cLFy5USUmJJkyYYHfSAAAAAAAAAAAAGs1jgzN33XWXvvvuO82YMUMFBQXq3bu3NmzYoJiYGJecPyQkRDNnzqyxFBrqh/JrGsoPAAAAAAAAAPyXwzAMw+5EAAAAAAAAAAAA+AuPfOYMAAAAAAAAAACAryI4AwAAAAAAAAAAYCGCMwAAAAAAAAAAABYiOAMAAAAAAAAAAGAhvwzOZGVlqVOnTgoNDVViYqI++eQTu5PkNbZu3aqRI0cqLi5ODodDa9eutTtJXmXevHm69tprdckllyg6OlqjRo3S3r177U4WAAAAAAAAAMBCfheceeONN5SZmamZM2fq888/V69evZSSkqIjR47YnTSvUFJSol69eikrK8vupHilLVu2KD09XTt27FB2drbKyso0dOhQlZSU2J00AAAAAAAAAIBFHIZhGHYnwkqJiYm69tpr9fvf/16SVFFRofbt2+v+++/X1KlTbU6dd3E4HFqzZo1GjRpld1K81nfffafo6Ght2bJFgwYNsjs5AAAAAAAAAAAL+NXMmbNnzyovL0/JycnmtoCAACUnJysnJ8fGlMFfnThxQpIUFRVlc0oAAAAAAAAAAFbxq+DM999/r/LycsXExDhtj4mJUUFBgU2pgr+qqKjQlClTdN1116l79+52JwcAAAAAAAAAYJFmdicA8Ffp6enauXOnPvroI7uTAgAAAAAAAACwkF8FZ9q0aaPAwEAVFhY6bS8sLFRsbKxNqYI/ysjI0Lp167R161ZdeumldicHAAAAAAAAAGAhv1rWLDg4WAkJCdq0aZO5raKiQps2bVJSUpKNKYO/MAxDGRkZWrNmjTZv3qz4+Hi7kwQAAAAAAAAAsJhfzZyRpMzMTKWmpqpPnz7q27evFi5cqJKSEk2YMMHupHmFU6dOaf/+/ebr/Px8ffnll4qKilKHDh1sTJl3SE9P18qVK/XWW2/pkksuMZ91FBERoebNm9ucOgAAAAAAAACAFRyGYRh2J8Jqv//97/Xss8+qoKBAvXv31uLFi5WYmGh3srzChx9+qBtvvLHG9tTUVC1fvtz6BHkZh8NR6/Zly5bpvvvuszYxAAAAAAAAAABb+GVwBgAAAAAAAAAAwC5+9cwZAAAAAAAAAAAAuxGcAQAAAAAAAAAAsBDBGQAAAAAAAAAAAAsRnAEAAAAAAAAAALAQwRkAAAAAAAAAAAALEZwBAAAAAAAAAACwEMEZAAAAAAAAAAAACxGcAQAAAAAAAAAAsBDBGQAAAAAAAAAAAAsRnAEAAAAAAAAAALAQwRkAAAAAAAAAAAALEZwBAAAAAAAAAACw0P8DZVlyWF40x/8AAAAASUVORK5CYII="/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Most variables are normally distributed. The exceptions are the ranking and the season performance.</p>
<p>The seasonal points have higher values, because it's a cumulative sum and no average is taken.</p>
<p>Rankings are more likely to be lower, because it's a dense ranking. Earlier in the season most teams will have similar rankings; only later in the season do we have higher rankings.</p>
<p>In the Season graph we see the effect of COVID-19; less games were played in 2020.
You can also see the addition of new teams in 2011 and 2012.</p>
<p>There is the sharp drop in the 'Rounds' graph; this is when the finals rounds happen, where fewer games are played.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Create-training-and-test-set">Create training and test set<a class="anchor-link" href="#Create-training-and-test-set">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>We use matches played before 2019 as the training set.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [87]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Create a training and test set.</span>
<span class="c1"># Use games played before 2019 as the training set.</span>
<span class="n">train_set</span> <span class="o">=</span> <span class="n">afl_df</span><span class="p">[</span><span class="n">afl_df</span><span class="p">[</span><span class="s1">'Season'</span><span class="p">]</span> <span class="o">&lt;</span> <span class="mi">2019</span><span class="p">]</span>
<span class="n">test_set</span> <span class="o">=</span> <span class="n">afl_df</span><span class="p">[</span><span class="n">afl_df</span><span class="p">[</span><span class="s1">'Season'</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">2019</span><span class="p">]</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Data-preparation">Data preparation<a class="anchor-link" href="#Data-preparation">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [6]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Want out sklearn classes to return pandas dataframes, not numpy arrays</span>
<span class="kn">from</span> <span class="nn">sklearn</span> <span class="kn">import</span> <span class="n">set_config</span>
<span class="c1">#set_config(transform_output = "pandas")</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>We will create a data transformer to prepare our data.</p>
<p>To prepare the data, we simply remove the columns that we don't want to use in our training (such as the ones we can't know before a match is played).</p>
<p>There are not many NA values, so we simply drop them.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [82]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.base</span> <span class="kn">import</span> <span class="n">BaseEstimator</span><span class="p">,</span> <span class="n">TransformerMixin</span>

<span class="n">date_ix</span><span class="p">,</span> <span class="n">season_ix</span><span class="p">,</span> <span class="n">round_ix</span><span class="p">,</span> <span class="n">hometeam_ix</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span> 
<span class="n">homepoints_ix</span><span class="p">,</span> <span class="n">winner_ix</span><span class="p">,</span> <span class="n">awayteam_ix</span><span class="p">,</span> <span class="n">away_points_ix</span> <span class="o">=</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">25</span><span class="p">,</span> <span class="mi">26</span>
<span class="n">cols_to_drop</span> <span class="o">=</span> <span class="p">[</span><span class="n">season_ix</span><span class="p">,</span> <span class="n">date_ix</span><span class="p">,</span> <span class="n">round_ix</span><span class="p">,</span> <span class="n">hometeam_ix</span><span class="p">,</span> <span class="n">winner_ix</span><span class="p">,</span> <span class="n">awayteam_ix</span><span class="p">,</span> <span class="n">homepoints_ix</span><span class="p">,</span> <span class="n">away_points_ix</span><span class="p">]</span>

<span class="k">class</span> <span class="nc">AFLDataPrepper</span><span class="p">(</span><span class="n">BaseEstimator</span><span class="p">,</span> <span class="n">TransformerMixin</span><span class="p">):</span>
    <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">dropNA</span> <span class="o">=</span> <span class="kc">True</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">dropNA</span> <span class="o">=</span> <span class="n">dropNA</span>

    <span class="k">def</span> <span class="nf">fit</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="kc">None</span><span class="p">):</span>
        <span class="k">return</span> <span class="bp">self</span>

    <span class="k">def</span> <span class="nf">transform</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">):</span>

        <span class="c1"># Remove tied matches (this happens rarely)</span>
        <span class="n">draws</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">iloc</span><span class="p">[:,</span><span class="n">winner_ix</span><span class="p">]</span> <span class="o">==</span> <span class="s1">'Draw'</span>
        <span class="n">X</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">X</span><span class="p">[</span><span class="n">draws</span><span class="p">]</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>

        <span class="c1"># Only want to use features that we can know before the game is played</span>
        <span class="n">X</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">columns</span><span class="p">[</span><span class="n">cols_to_drop</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

        <span class="c1"># Remove rows with missing values</span>
        <span class="k">if</span> <span class="bp">self</span><span class="o">.</span><span class="n">dropNA</span><span class="p">:</span>
            <span class="n">X</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">dropna</span><span class="p">()</span>

        <span class="k">return</span> <span class="n">X</span>    
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [83]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.pipeline</span> <span class="kn">import</span> <span class="n">Pipeline</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">StandardScaler</span>

<span class="n">afl_pipeline</span> <span class="o">=</span> <span class="n">Pipeline</span><span class="p">([</span>
    <span class="p">(</span><span class="s1">'afl_prepper'</span><span class="p">,</span> <span class="n">AFLDataPrepper</span><span class="p">()),</span>
    <span class="p">(</span><span class="s1">'std_scaler'</span><span class="p">,</span> <span class="n">StandardScaler</span><span class="p">())</span>
<span class="p">])</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [88]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">get_labels</span><span class="p">(</span><span class="n">train_set</span><span class="p">,</span> <span class="n">drop_na</span> <span class="o">=</span> <span class="kc">True</span><span class="p">):</span>
    <span class="n">noDraws</span> <span class="o">=</span> <span class="n">train_set</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">train_set</span><span class="p">[</span><span class="n">train_set</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">]</span> <span class="o">==</span> <span class="s2">"Draw"</span><span class="p">]</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">drop_na</span><span class="p">:</span>
        <span class="k">return</span> <span class="n">noDraws</span><span class="o">.</span><span class="n">dropna</span><span class="p">()[</span><span class="s2">"Winner"</span><span class="p">]</span>
    <span class="k">return</span> <span class="n">noDraws</span><span class="p">[</span><span class="s2">"Winner"</span><span class="p">]</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [89]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Transform the data and get the labels</span>
<span class="n">afl_prepared</span> <span class="o">=</span> <span class="n">afl_pipeline</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">train_set</span><span class="o">.</span><span class="n">copy</span><span class="p">())</span>
<span class="n">train_labels</span> <span class="o">=</span> <span class="n">get_labels</span><span class="p">(</span><span class="n">train_set</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Selecting-and-training-a-model">Selecting and training a model<a class="anchor-link" href="#Selecting-and-training-a-model">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [68]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">cross_val_score</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>

<span class="k">def</span> <span class="nf">evaluate_model</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">train</span><span class="p">,</span> <span class="n">labels</span><span class="p">,</span> <span class="n">k</span><span class="o">=</span><span class="mi">3</span><span class="p">):</span>
    <span class="n">accuracy</span> <span class="o">=</span> <span class="n">cross_val_score</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">train</span><span class="p">,</span> <span class="n">labels</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="n">k</span><span class="p">,</span> <span class="n">scoring</span> <span class="o">=</span> <span class="s2">"accuracy"</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"Accuracy = </span><span class="si">{:0.2f}</span><span class="s2">%"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">accuracy</span><span class="p">)</span><span class="o">*</span><span class="mi">100</span><span class="p">))</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Random-Forest-Classifier">Random Forest Classifier<a class="anchor-link" href="#Random-Forest-Classifier">¶</a></h4>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [69]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">RandomForestClassifier</span>
<span class="n">afl_rf</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">()</span>
<span class="n">afl_rf</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[69]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<style>#sk-container-id-1 {color: black;background-color: white;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div class="sk-top-container" id="sk-container-id-1"><div class="sk-text-repr-fallback"><pre>RandomForestClassifier()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br/>On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden=""><div class="sk-item"><div class="sk-estimator sk-toggleable"><input checked="" class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-1">RandomForestClassifier</label><div class="sk-toggleable__content"><pre>RandomForestClassifier()</pre></div></div></div></div></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [70]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">evaluate_model</span><span class="p">(</span><span class="n">afl_rf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 63.05%
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [20]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Fine tune the parameters with randomised grid search.</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">RandomizedSearchCV</span>

<span class="n">param_grid</span> <span class="o">=</span> <span class="p">{</span>
    <span class="s1">'bootstrap'</span><span class="p">:</span> <span class="p">[</span><span class="kc">True</span><span class="p">,</span> <span class="kc">False</span><span class="p">],</span>
    <span class="s1">'max_depth'</span><span class="p">:</span> <span class="p">[</span><span class="mi">10</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">30</span><span class="p">],</span>
    <span class="s1">'min_samples_leaf'</span><span class="p">:</span> <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">4</span><span class="p">],</span>
    <span class="s1">'min_samples_split'</span><span class="p">:</span> <span class="p">[</span><span class="mi">2</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">10</span><span class="p">],</span>
    <span class="s1">'n_estimators'</span><span class="p">:</span> <span class="p">[</span><span class="mi">100</span><span class="p">,</span> <span class="mi">200</span><span class="p">,</span> <span class="mi">500</span><span class="p">]</span>
<span class="p">}</span>

<span class="n">rand_search_cv</span> <span class="o">=</span> <span class="n">RandomizedSearchCV</span><span class="p">(</span><span class="n">estimator</span><span class="o">=</span><span class="n">afl_rf</span><span class="p">,</span>
                                    <span class="n">param_distributions</span><span class="o">=</span><span class="n">param_grid</span><span class="p">,</span>
                                    <span class="n">cv</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span>
                                    <span class="n">n_iter</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span>
                                    <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>

<span class="n">rand_search_cv</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[20]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<style>#sk-container-id-2 {color: black;background-color: white;}#sk-container-id-2 pre{padding: 0;}#sk-container-id-2 div.sk-toggleable {background-color: white;}#sk-container-id-2 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-2 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-2 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-2 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-2 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-2 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-2 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-2 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-2 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-2 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-2 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-2 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-2 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-2 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-2 div.sk-item {position: relative;z-index: 1;}#sk-container-id-2 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-2 div.sk-item::before, #sk-container-id-2 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-2 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-2 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-2 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-2 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-2 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-2 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-2 div.sk-label-container {text-align: center;}#sk-container-id-2 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-2 div.sk-text-repr-fallback {display: none;}</style><div class="sk-top-container" id="sk-container-id-2"><div class="sk-text-repr-fallback"><pre>RandomizedSearchCV(cv=5, estimator=RandomForestClassifier(), n_iter=100,
                   param_distributions={'bootstrap': [True, False],
                                        'max_depth': [10, 20, 30],
                                        'min_samples_leaf': [1, 2, 4],
                                        'min_samples_split': [2, 5, 10],
                                        'n_estimators': [100, 200, 500]},
                   random_state=42)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br/>On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden=""><div class="sk-item sk-dashed-wrapped"><div class="sk-label-container"><div class="sk-label sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-2" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-2">RandomizedSearchCV</label><div class="sk-toggleable__content"><pre>RandomizedSearchCV(cv=5, estimator=RandomForestClassifier(), n_iter=100,
                   param_distributions={'bootstrap': [True, False],
                                        'max_depth': [10, 20, 30],
                                        'min_samples_leaf': [1, 2, 4],
                                        'min_samples_split': [2, 5, 10],
                                        'n_estimators': [100, 200, 500]},
                   random_state=42)</pre></div></div></div><div class="sk-parallel"><div class="sk-parallel-item"><div class="sk-item"><div class="sk-label-container"><div class="sk-label sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-3" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-3">estimator: RandomForestClassifier</label><div class="sk-toggleable__content"><pre>RandomForestClassifier()</pre></div></div></div><div class="sk-serial"><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-4" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-4">RandomForestClassifier</label><div class="sk-toggleable__content"><pre>RandomForestClassifier()</pre></div></div></div></div></div></div></div></div></div></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>This took about half an hour to do. Let's see the results:</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [21]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">rand_search_cv</span><span class="o">.</span><span class="n">best_params_</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[21]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>{'n_estimators': 500,
 'min_samples_split': 10,
 'min_samples_leaf': 2,
 'max_depth': 20,
 'bootstrap': True}</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">best_rf</span> <span class="o">=</span> <span class="n">rand_search_cv</span><span class="o">.</span><span class="n">best_estimator_</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [24]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">evaluate_model</span><span class="p">(</span><span class="n">best_rf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 65.09%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Some of the best parameters were the maximum values, so possible we'd improve the model by increasing these parameters. For this reason we will do a second search.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [21]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">param_grid2</span> <span class="o">=</span> <span class="p">{</span>
    <span class="s1">'bootstrap'</span><span class="p">:</span> <span class="p">[</span><span class="kc">True</span><span class="p">,</span> <span class="kc">False</span><span class="p">],</span>
    <span class="s1">'max_depth'</span><span class="p">:</span> <span class="p">[</span><span class="mi">15</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">25</span><span class="p">],</span>
    <span class="s1">'min_samples_leaf'</span><span class="p">:</span> <span class="p">[</span><span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">],</span>
    <span class="s1">'min_samples_split'</span><span class="p">:</span> <span class="p">[</span><span class="mi">10</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">30</span><span class="p">],</span>
    <span class="s1">'n_estimators'</span><span class="p">:</span> <span class="p">[</span><span class="mi">400</span><span class="p">,</span> <span class="mi">500</span><span class="p">,</span> <span class="mi">750</span><span class="p">,</span> <span class="mi">1000</span><span class="p">]</span>
<span class="p">}</span>

<span class="n">rand_search_cv2</span> <span class="o">=</span> <span class="n">RandomizedSearchCV</span><span class="p">(</span><span class="n">estimator</span><span class="o">=</span><span class="n">afl_rf</span><span class="p">,</span>
                                    <span class="n">param_distributions</span><span class="o">=</span><span class="n">param_grid2</span><span class="p">,</span>
                                    <span class="n">cv</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span>
                                    <span class="n">n_iter</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span>
                                    <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>

<span class="n">rand_search_cv2</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[21]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<style>#sk-container-id-2 {color: black;background-color: white;}#sk-container-id-2 pre{padding: 0;}#sk-container-id-2 div.sk-toggleable {background-color: white;}#sk-container-id-2 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-2 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-2 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-2 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-2 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-2 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-2 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-2 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-2 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-2 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-2 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-2 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-2 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-2 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-2 div.sk-item {position: relative;z-index: 1;}#sk-container-id-2 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-2 div.sk-item::before, #sk-container-id-2 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-2 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-2 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-2 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-2 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-2 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-2 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-2 div.sk-label-container {text-align: center;}#sk-container-id-2 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-2 div.sk-text-repr-fallback {display: none;}</style><div class="sk-top-container" id="sk-container-id-2"><div class="sk-text-repr-fallback"><pre>RandomizedSearchCV(cv=5, estimator=RandomForestClassifier(), n_iter=100,
                   param_distributions={'bootstrap': [True, False],
                                        'max_depth': [15, 20, 25],
                                        'min_samples_leaf': [2, 3],
                                        'min_samples_split': [10, 20, 30],
                                        'n_estimators': [400, 500, 750, 1000]},
                   random_state=42)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br/>On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden=""><div class="sk-item sk-dashed-wrapped"><div class="sk-label-container"><div class="sk-label sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-2" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-2">RandomizedSearchCV</label><div class="sk-toggleable__content"><pre>RandomizedSearchCV(cv=5, estimator=RandomForestClassifier(), n_iter=100,
                   param_distributions={'bootstrap': [True, False],
                                        'max_depth': [15, 20, 25],
                                        'min_samples_leaf': [2, 3],
                                        'min_samples_split': [10, 20, 30],
                                        'n_estimators': [400, 500, 750, 1000]},
                   random_state=42)</pre></div></div></div><div class="sk-parallel"><div class="sk-parallel-item"><div class="sk-item"><div class="sk-label-container"><div class="sk-label sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-3" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-3">estimator: RandomForestClassifier</label><div class="sk-toggleable__content"><pre>RandomForestClassifier()</pre></div></div></div><div class="sk-serial"><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-4" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-4">RandomForestClassifier</label><div class="sk-toggleable__content"><pre>RandomForestClassifier()</pre></div></div></div></div></div></div></div></div></div></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">rand_search_cv2</span><span class="o">.</span><span class="n">best_params_</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[22]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>{'n_estimators': 1000,
 'min_samples_split': 30,
 'min_samples_leaf': 3,
 'max_depth': 20,
 'bootstrap': True}</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [23]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">evaluate_model</span><span class="p">(</span><span class="n">rand_search_cv2</span><span class="o">.</span><span class="n">best_estimator_</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 65.17%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>n_estimators and min_samples_split are still at their max values, so we could do another search.</p>
<p>However, the previous search only resulted in a very modest increase in accuracy, so we'll leave the fine tuning here for now.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Logistic-Regression">Logistic Regression<a class="anchor-link" href="#Logistic-Regression">¶</a></h4>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LogisticRegression</span>

<span class="n">log_reg</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">max_iter</span><span class="o">=</span><span class="mi">500</span><span class="p">)</span>
<span class="n">log_reg</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[22]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<style>#sk-container-id-1 {color: black;background-color: white;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div class="sk-top-container" id="sk-container-id-1"><div class="sk-text-repr-fallback"><pre>LogisticRegression(max_iter=500)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br/>On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden=""><div class="sk-item"><div class="sk-estimator sk-toggleable"><input checked="" class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-1">LogisticRegression</label><div class="sk-toggleable__content"><pre>LogisticRegression(max_iter=500)</pre></div></div></div></div></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [72]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">evaluate_model</span><span class="p">(</span><span class="n">log_reg</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 64.25%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So, out of the box this seems to at least do as well as the random forest classifier.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Support-Vector-Machine">Support Vector Machine<a class="anchor-link" href="#Support-Vector-Machine">¶</a></h4>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [73]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="kn">import</span> <span class="n">LinearSVC</span>
<span class="n">linearSVC</span> <span class="o">=</span> <span class="n">LinearSVC</span><span class="p">(</span><span class="n">C</span><span class="o">=</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">loss</span><span class="o">=</span><span class="s1">'hinge'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [74]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">evaluate_model</span><span class="p">(</span><span class="n">linearSVC</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 64.22%
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [75]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Polynomial SVM</span>
<span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="kn">import</span> <span class="n">SVC</span>
<span class="n">poly_svm</span> <span class="o">=</span> <span class="n">SVC</span><span class="p">(</span><span class="n">kernel</span> <span class="o">=</span> <span class="s2">"poly"</span><span class="p">,</span> <span class="n">degree</span><span class="o">=</span><span class="mi">3</span><span class="p">,</span> <span class="n">C</span><span class="o">=</span><span class="mf">0.0001</span><span class="p">)</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">poly_svm</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 57.55%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So higher degree polynomials don't appear to do a better job.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Neural-networks">Neural networks<a class="anchor-link" href="#Neural-networks">¶</a></h4>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">tensorflow</span> <span class="k">as</span> <span class="nn">tf</span> 
<span class="kn">from</span> <span class="nn">tensorflow</span> <span class="kn">import</span> <span class="n">keras</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [23]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Neural networks need integer labels</span>
<span class="n">bin_labels</span> <span class="o">=</span> <span class="p">(</span><span class="n">train_labels</span> <span class="o">==</span> <span class="s2">"Home"</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="s1">'int'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [76]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">build_model</span><span class="p">(</span><span class="n">n_hidden</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">n_neurons</span><span class="o">=</span><span class="mi">30</span><span class="p">,</span> <span class="n">learning_rate</span><span class="o">=</span><span class="mf">3e-3</span><span class="p">):</span>
    <span class="n">model</span> <span class="o">=</span> <span class="n">keras</span><span class="o">.</span><span class="n">models</span><span class="o">.</span><span class="n">Sequential</span><span class="p">()</span>
    <span class="n">model</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">keras</span><span class="o">.</span><span class="n">layers</span><span class="o">.</span><span class="n">Input</span><span class="p">(</span><span class="n">shape</span><span class="o">=</span><span class="p">(</span><span class="mi">38</span><span class="p">,)))</span>
    <span class="k">for</span> <span class="n">layer</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_hidden</span><span class="p">):</span>
        <span class="n">model</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">keras</span><span class="o">.</span><span class="n">layers</span><span class="o">.</span><span class="n">Dense</span><span class="p">(</span><span class="n">n_neurons</span><span class="p">,</span> <span class="n">activation</span><span class="o">=</span><span class="s2">"relu"</span><span class="p">))</span>
    <span class="n">model</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">keras</span><span class="o">.</span><span class="n">layers</span><span class="o">.</span><span class="n">Dense</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">activation</span><span class="o">=</span><span class="s2">"sigmoid"</span><span class="p">))</span>
    <span class="n">optimizer</span> <span class="o">=</span> <span class="n">keras</span><span class="o">.</span><span class="n">optimizers</span><span class="o">.</span><span class="n">Adam</span><span class="p">(</span><span class="n">learning_rate</span><span class="p">)</span>
    <span class="n">model</span><span class="o">.</span><span class="n">compile</span><span class="p">(</span><span class="n">loss</span><span class="o">=</span><span class="n">keras</span><span class="o">.</span><span class="n">losses</span><span class="o">.</span><span class="n">binary_crossentropy</span><span class="p">,</span> <span class="n">optimizer</span><span class="o">=</span><span class="n">optimizer</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">model</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [89]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">scikeras.wrappers</span> <span class="kn">import</span> <span class="n">KerasClassifier</span>

<span class="n">keras_clf</span> <span class="o">=</span> <span class="n">KerasClassifier</span><span class="p">(</span>
    <span class="n">model</span><span class="o">=</span><span class="n">build_model</span><span class="p">,</span>
    <span class="n">n_hidden</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span>
    <span class="n">n_neurons</span><span class="o">=</span><span class="mi">30</span><span class="p">,</span>
    <span class="n">learning_rate</span> <span class="o">=</span> <span class="mf">3e-3</span>
<span class="p">)</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">keras_clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>77/77 [==============================] - 2s 2ms/step - loss: 0.6406
39/39 [==============================] - 0s 2ms/step
77/77 [==============================] - 1s 1ms/step - loss: 0.6461
39/39 [==============================] - 0s 1ms/step
77/77 [==============================] - 1s 1ms/step - loss: 0.6489
39/39 [==============================] - 0s 1ms/step
Accuracy = 64.39%
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [91]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">scipy.stats</span> <span class="kn">import</span> <span class="n">reciprocal</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">RandomizedSearchCV</span>

<span class="n">param_distribs</span> <span class="o">=</span> <span class="p">{</span>
    <span class="s2">"n_hidden"</span><span class="p">:</span> <span class="p">[</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">4</span><span class="p">],</span>
    <span class="s2">"n_neurons"</span><span class="p">:</span> <span class="p">[</span><span class="mi">10</span><span class="p">,</span><span class="mi">20</span><span class="p">,</span><span class="mi">30</span><span class="p">],</span>
    <span class="s2">"learning_rate"</span><span class="p">:</span> <span class="n">reciprocal</span><span class="p">(</span><span class="mf">3e-4</span><span class="p">,</span> <span class="mf">3e-2</span><span class="p">)</span>
<span class="p">}</span>
<span class="n">rnd_search_cv</span> <span class="o">=</span> <span class="n">RandomizedSearchCV</span><span class="p">(</span><span class="n">keras_clf</span><span class="p">,</span> <span class="n">param_distribs</span><span class="p">,</span> <span class="n">n_iter</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span>
<span class="n">rnd_search_cv</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">,</span> <span class="n">epochs</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span>
                  <span class="n">validation_split</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span>
                  <span class="n">verbose</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 2ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 2ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 2ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 2ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
39/39 [==============================] - 0s 1ms/step
</pre>
</div>
</div>
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[91]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<style>#sk-container-id-3 {color: black;background-color: white;}#sk-container-id-3 pre{padding: 0;}#sk-container-id-3 div.sk-toggleable {background-color: white;}#sk-container-id-3 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-3 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-3 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-3 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-3 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-3 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-3 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-3 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-3 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-3 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-3 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-3 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-3 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-3 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-3 div.sk-item {position: relative;z-index: 1;}#sk-container-id-3 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-3 div.sk-item::before, #sk-container-id-3 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-3 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-3 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-3 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-3 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-3 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-3 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-3 div.sk-label-container {text-align: center;}#sk-container-id-3 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-3 div.sk-text-repr-fallback {display: none;}</style><div class="sk-top-container" id="sk-container-id-3"><div class="sk-text-repr-fallback"><pre>RandomizedSearchCV(cv=3,
                   estimator=KerasClassifier(learning_rate=0.003, model=&lt;function build_model at 0x0000015BE74B8550&gt;, n_hidden=1, n_neurons=30),
                   param_distributions={'learning_rate': &lt;scipy.stats._distn_infrastructure.rv_continuous_frozen object at 0x0000015BF0D4C580&gt;,
                                        'n_hidden': [1, 2, 3, 4],
                                        'n_neurons': [10, 20, 30]})</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br/>On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden=""><div class="sk-item sk-dashed-wrapped"><div class="sk-label-container"><div class="sk-label sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-3" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-3">RandomizedSearchCV</label><div class="sk-toggleable__content"><pre>RandomizedSearchCV(cv=3,
                   estimator=KerasClassifier(learning_rate=0.003, model=&lt;function build_model at 0x0000015BE74B8550&gt;, n_hidden=1, n_neurons=30),
                   param_distributions={'learning_rate': &lt;scipy.stats._distn_infrastructure.rv_continuous_frozen object at 0x0000015BF0D4C580&gt;,
                                        'n_hidden': [1, 2, 3, 4],
                                        'n_neurons': [10, 20, 30]})</pre></div></div></div><div class="sk-parallel"><div class="sk-parallel-item"><div class="sk-item"><div class="sk-label-container"><div class="sk-label sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-4" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-4">estimator: KerasClassifier</label><div class="sk-toggleable__content"><pre>KerasClassifier(
	model=&lt;function build_model at 0x0000015BE74B8550&gt;
	build_fn=None
	warm_start=False
	random_state=None
	optimizer=rmsprop
	loss=None
	metrics=None
	batch_size=None
	validation_batch_size=None
	verbose=1
	callbacks=None
	validation_split=0.0
	shuffle=True
	run_eagerly=False
	epochs=1
	n_hidden=1
	n_neurons=30
	learning_rate=0.003
	class_weight=None
)</pre></div></div></div><div class="sk-serial"><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-5" type="checkbox"/><label class="sk-toggleable__label sk-toggleable__label-arrow" for="sk-estimator-id-5">KerasClassifier</label><div class="sk-toggleable__content"><pre>KerasClassifier(
	model=&lt;function build_model at 0x0000015BE74B8550&gt;
	build_fn=None
	warm_start=False
	random_state=None
	optimizer=rmsprop
	loss=None
	metrics=None
	batch_size=None
	validation_batch_size=None
	verbose=1
	callbacks=None
	validation_split=0.0
	shuffle=True
	run_eagerly=False
	epochs=1
	n_hidden=1
	n_neurons=30
	learning_rate=0.003
	class_weight=None
)</pre></div></div></div></div></div></div></div></div></div></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [92]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">rnd_search_cv</span><span class="o">.</span><span class="n">best_params_</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[92]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>{'learning_rate': 0.0017120646387156207, 'n_hidden': 1, 'n_neurons': 20}</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [93]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">evaluate_model</span><span class="p">(</span><span class="n">rnd_search_cv</span><span class="o">.</span><span class="n">best_estimator_</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>77/77 [==============================] - 1s 2ms/step - loss: 0.6603
39/39 [==============================] - 0s 3ms/step
77/77 [==============================] - 1s 2ms/step - loss: 0.6580
39/39 [==============================] - 0s 1ms/step
77/77 [==============================] - 1s 2ms/step - loss: 0.6478
39/39 [==============================] - 0s 1ms/step
Accuracy = 63.11%
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [94]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">evaluate_model</span><span class="p">(</span><span class="n">KerasClassifier</span><span class="p">(</span><span class="n">model</span><span class="o">=</span><span class="n">build_model</span><span class="p">,</span> <span class="n">n_hidden</span><span class="o">=</span><span class="mi">1</span><span class="p">),</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>77/77 [==============================] - 1s 2ms/step - loss: 0.6255
39/39 [==============================] - 0s 2ms/step
77/77 [==============================] - 1s 2ms/step - loss: 0.6747
39/39 [==============================] - 0s 2ms/step
77/77 [==============================] - 1s 2ms/step - loss: 0.6568
39/39 [==============================] - 0s 1ms/step
Accuracy = 64.58%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Ensemble-Methods">Ensemble Methods<a class="anchor-link" href="#Ensemble-Methods">¶</a></h3><p>So we have four models, each achieving an accuracy of about 65%.</p>
<p>Now we'll see if we can combine them to produce an even more accurate model.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [77]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">RandomForestClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LogisticRegression</span>
<span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="kn">import</span> <span class="n">LinearSVC</span>
<span class="kn">import</span> <span class="nn">tensorflow</span> <span class="k">as</span> <span class="nn">tf</span> 
<span class="kn">from</span> <span class="nn">tensorflow</span> <span class="kn">import</span> <span class="n">keras</span>
<span class="kn">from</span> <span class="nn">scikeras.wrappers</span> <span class="kn">import</span> <span class="n">KerasClassifier</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [78]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">rf_clf</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">()</span>
<span class="n">log_clf</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">max_iter</span><span class="o">=</span><span class="mi">500</span><span class="p">)</span>
<span class="n">svm_clf</span> <span class="o">=</span> <span class="n">LinearSVC</span><span class="p">(</span><span class="n">C</span><span class="o">=</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">loss</span><span class="o">=</span><span class="s1">'hinge'</span><span class="p">)</span>
<span class="n">keras_clf</span> <span class="o">=</span> <span class="n">KerasClassifier</span><span class="p">(</span>
    <span class="n">model</span><span class="o">=</span><span class="n">build_model</span><span class="p">,</span>
    <span class="n">n_hidden</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span>
    <span class="n">n_neurons</span><span class="o">=</span><span class="mi">30</span><span class="p">,</span>
    <span class="n">learning_rate</span> <span class="o">=</span> <span class="mf">7e-4</span>
<span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [79]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">bin_labels</span> <span class="o">=</span> <span class="p">(</span><span class="n">train_labels</span> <span class="o">==</span> <span class="s2">"Home"</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="s1">'int'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>To establish a baseline, let's evaluate our current models:</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [80]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">clf</span> <span class="ow">in</span> <span class="p">(</span><span class="n">rf_clf</span><span class="p">,</span> <span class="n">log_clf</span><span class="p">,</span> <span class="n">svm_clf</span><span class="p">,</span> <span class="n">keras_clf</span><span class="p">):</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">clf</span><span class="o">.</span><span class="vm">__class__</span><span class="o">.</span><span class="vm">__name__</span><span class="p">,</span> <span class="s2">":"</span><span class="p">)</span>
    <span class="n">evaluate_model</span><span class="p">(</span><span class="n">clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>RandomForestClassifier :
Accuracy = 63.38%
LogisticRegression :
Accuracy = 64.55%
LinearSVC :
Accuracy = 64.52%
KerasClassifier :
77/77 [==============================] - 2s 4ms/step - loss: 0.6799
39/39 [==============================] - 0s 3ms/step
77/77 [==============================] - 1s 3ms/step - loss: 0.6775
39/39 [==============================] - 0s 3ms/step
77/77 [==============================] - 1s 2ms/step - loss: 0.6904
39/39 [==============================] - 0s 2ms/step
Accuracy = 63.03%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So our state vector machine and logistic regresssion models are our best.
Let's see if we can improve them using some ensemble methods.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Voting-classifier">Voting classifier<a class="anchor-link" href="#Voting-classifier">¶</a></h4>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [81]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">VotingClassifier</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [82]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">voting_clf</span> <span class="o">=</span> <span class="n">VotingClassifier</span><span class="p">(</span>
    <span class="n">estimators</span><span class="o">=</span><span class="p">[(</span><span class="s1">'rf'</span><span class="p">,</span> <span class="n">rf_clf</span><span class="p">),</span> <span class="p">(</span><span class="s1">'lr'</span><span class="p">,</span> <span class="n">log_clf</span><span class="p">),</span> <span class="p">(</span><span class="s1">'svm'</span><span class="p">,</span> <span class="n">svm_clf</span><span class="p">),</span> <span class="p">(</span><span class="s1">'nn'</span><span class="p">,</span> <span class="n">keras_clf</span><span class="p">)],</span>
    <span class="n">voting</span><span class="o">=</span><span class="s1">'hard'</span>
<span class="p">)</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">voting_clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>77/77 [==============================] - 1s 2ms/step - loss: 0.7624
39/39 [==============================] - 0s 2ms/step
77/77 [==============================] - 1s 3ms/step - loss: 0.7113
39/39 [==============================] - 0s 2ms/step
77/77 [==============================] - 1s 2ms/step - loss: 0.7575
39/39 [==============================] - 0s 3ms/step
Accuracy = 64.17%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So the voting classifier doesn't give better results.
Try with soft voting:</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [83]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">voting_soft_clf</span> <span class="o">=</span> <span class="n">VotingClassifier</span><span class="p">(</span>
    <span class="n">estimators</span><span class="o">=</span><span class="p">[(</span><span class="s1">'rf'</span><span class="p">,</span> <span class="n">rf_clf</span><span class="p">),</span> <span class="p">(</span><span class="s1">'lr'</span><span class="p">,</span> <span class="n">log_clf</span><span class="p">),</span> <span class="p">(</span><span class="s1">'nn'</span><span class="p">,</span> <span class="n">keras_clf</span><span class="p">)],</span>
    <span class="n">voting</span><span class="o">=</span><span class="s1">'soft'</span>
<span class="p">)</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">voting_soft_clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>77/77 [==============================] - 1s 3ms/step - loss: 0.6931
39/39 [==============================] - 0s 2ms/step
77/77 [==============================] - 1s 2ms/step - loss: 0.6721
39/39 [==============================] - 0s 2ms/step
77/77 [==============================] - 1s 4ms/step - loss: 0.7699
39/39 [==============================] - 0s 3ms/step
Accuracy = 64.80%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Note that the LinearSVM classifier doesn't predict probabilities and can't be included in the soft voting model.
We see that using soft voting with all of the other classifiers gives us an accuracy that is almost as good as the SVM model.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Bagging">Bagging<a class="anchor-link" href="#Bagging">¶</a></h4>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Logistic regression is one of our best classifiers, so let's try an ensemble method to improve it.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [84]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">BaggingClassifier</span>

<span class="n">bag_log_clf</span> <span class="o">=</span> <span class="n">BaggingClassifier</span><span class="p">(</span>
    <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">max_iter</span><span class="o">=</span><span class="mi">500</span><span class="p">),</span> <span class="n">n_estimators</span><span class="o">=</span><span class="mi">500</span><span class="p">,</span>
    <span class="n">max_samples</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span> <span class="n">bootstrap</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">n_jobs</span><span class="o">=-</span><span class="mi">1</span>
<span class="p">)</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">bag_log_clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 64.66%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So bagging appears to slightly improve the logistic regression classifier, but a lot longer to train.</p>
<p>Let's try the SVM:</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [85]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">bag_svm_clf</span> <span class="o">=</span> <span class="n">BaggingClassifier</span><span class="p">(</span>
    <span class="n">LinearSVC</span><span class="p">(</span><span class="n">C</span><span class="o">=</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">loss</span><span class="o">=</span><span class="s1">'hinge'</span><span class="p">),</span> <span class="n">n_estimators</span><span class="o">=</span><span class="mi">500</span><span class="p">,</span>
    <span class="n">max_samples</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span> <span class="n">bootstrap</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">n_jobs</span><span class="o">=-</span><span class="mi">1</span>
<span class="p">)</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">bag_svm_clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 63.41%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So bagging doesn't improve the LinearSVC.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h4 id="Boosting">Boosting<a class="anchor-link" href="#Boosting">¶</a></h4>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [86]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="kn">import</span> <span class="n">AdaBoostClassifier</span>

<span class="n">ada_clf</span> <span class="o">=</span> <span class="n">AdaBoostClassifier</span><span class="p">(</span>
    <span class="n">log_clf</span><span class="p">,</span> <span class="n">n_estimators</span><span class="o">=</span><span class="mi">200</span><span class="p">,</span>
    <span class="n">algorithm</span><span class="o">=</span><span class="s2">"SAMME.R"</span><span class="p">,</span> <span class="n">learning_rate</span><span class="o">=</span><span class="mf">0.5</span>
<span class="p">)</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">ada_clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 64.47%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Not bad, but not much better than logistic regression by itself.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [87]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">xgboost</span>

<span class="n">xgb_clf</span> <span class="o">=</span> <span class="n">xgboost</span><span class="o">.</span><span class="n">XGBClassifier</span><span class="p">()</span>
<span class="n">evaluate_model</span><span class="p">(</span><span class="n">xgb_clf</span><span class="p">,</span> <span class="n">afl_prepared</span><span class="p">,</span> <span class="n">bin_labels</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy = 61.55%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So gradient boosting doesn't seem like a good prospect.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Evaluating-on-test-set">Evaluating on test set<a class="anchor-link" href="#Evaluating-on-test-set">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Our best performing models are the LinearSVC and logistic regression.
Let's see how they do on the test set.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [89]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">accuracy_score</span>

<span class="n">testX</span> <span class="o">=</span> <span class="n">afl_pipeline</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">test_set</span><span class="o">.</span><span class="n">copy</span><span class="p">())</span>
<span class="n">test_labels</span> <span class="o">=</span> <span class="n">get_labels</span><span class="p">(</span><span class="n">test_set</span><span class="o">.</span><span class="n">copy</span><span class="p">())</span>

<span class="n">log_clf</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">max_iter</span><span class="o">=</span><span class="mi">500</span><span class="p">)</span>
<span class="n">svm_clf</span> <span class="o">=</span> <span class="n">LinearSVC</span><span class="p">(</span><span class="n">C</span><span class="o">=</span><span class="mf">0.001</span><span class="p">,</span> <span class="n">loss</span><span class="o">=</span><span class="s1">'hinge'</span><span class="p">)</span>

<span class="k">for</span> <span class="n">clf</span> <span class="ow">in</span> <span class="p">(</span><span class="n">log_clf</span><span class="p">,</span> <span class="n">svm_clf</span><span class="p">):</span>
    <span class="n">clf</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">afl_prepared</span><span class="p">,</span> <span class="n">train_labels</span><span class="p">)</span>
    <span class="n">preds</span> <span class="o">=</span> <span class="n">clf</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">testX</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">clf</span><span class="o">.</span><span class="vm">__class__</span><span class="o">.</span><span class="vm">__name__</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"Accuracy = </span><span class="si">{:0.2f}</span><span class="s2">%"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">accuracy_score</span><span class="p">(</span><span class="n">test_labels</span><span class="p">,</span> <span class="n">preds</span><span class="p">)</span><span class="o">*</span><span class="mi">100</span><span class="p">))</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>LogisticRegression
Accuracy = 65.26%
LinearSVC
Accuracy = 63.47%
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So logistic regression does marginally better.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Launching-the-model">Launching the model<a class="anchor-link" href="#Launching-the-model">¶</a></h2><p>We want to be able to make actual predictions for future games, so we will create a class to do this.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [98]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">AFLPredictor</span><span class="p">:</span>
    <span class="k">def</span> <span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">transformer</span><span class="p">,</span> <span class="n">estimator</span><span class="p">,</span> <span class="n">match_df</span> <span class="o">=</span> <span class="kc">None</span><span class="p">,</span> <span class="n">afl_df</span> <span class="o">=</span> <span class="kc">None</span><span class="p">,</span> <span class="n">year</span><span class="o">=</span><span class="mi">2023</span> <span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">transformer</span> <span class="o">=</span> <span class="n">transformer</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">estimator</span> <span class="o">=</span> <span class="n">estimator</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">match_df</span> <span class="o">=</span> <span class="n">match_df</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">year</span> <span class="o">=</span> <span class="n">year</span>
    
    <span class="k">def</span> <span class="nf">getTeamStats</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">date</span><span class="p">,</span> <span class="nb">round</span><span class="p">,</span> <span class="n">homeTeam</span><span class="p">,</span> <span class="n">awayTeam</span><span class="p">):</span>

        <span class="c1"># Get only the matches we need to calculate stats for both tems</span>
        <span class="n">lastSeason</span> <span class="o">=</span> <span class="p">(</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Season'</span><span class="p">]</span> <span class="o">==</span> <span class="bp">self</span><span class="o">.</span><span class="n">year</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Round'</span><span class="p">]</span> <span class="o">&gt;</span> <span class="mi">18</span><span class="p">)</span>
        <span class="n">thisSeason</span> <span class="o">=</span> <span class="n">match_df</span><span class="p">[</span><span class="s1">'Season'</span><span class="p">]</span> <span class="o">==</span> <span class="bp">self</span><span class="o">.</span><span class="n">year</span>
        <span class="n">home</span> <span class="o">=</span> <span class="p">(</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Home Team'</span><span class="p">]</span> <span class="o">==</span> <span class="n">homeTeam</span><span class="p">)</span> <span class="o">|</span> <span class="p">(</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Away Team'</span><span class="p">]</span> <span class="o">==</span> <span class="n">homeTeam</span><span class="p">)</span>
        <span class="n">away</span> <span class="o">=</span> <span class="p">(</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Home Team'</span><span class="p">]</span> <span class="o">==</span> <span class="n">awayTeam</span><span class="p">)</span> <span class="o">|</span> <span class="p">(</span><span class="n">match_df</span><span class="p">[</span><span class="s1">'Away Team'</span><span class="p">]</span> <span class="o">==</span> <span class="n">awayTeam</span><span class="p">)</span>
        <span class="n">matches</span> <span class="o">=</span> <span class="n">match_df</span><span class="p">[(</span><span class="n">lastSeason</span> <span class="o">|</span> <span class="n">thisSeason</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">home</span> <span class="o">|</span> <span class="n">away</span><span class="p">)]</span>

        <span class="c1"># Add a dummy column that will be filled with our</span>
        <span class="n">dummy</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s1">'Date'</span><span class="p">:[</span><span class="n">date</span><span class="p">],</span> 
                             <span class="s1">'Round'</span><span class="p">:[</span><span class="nb">round</span><span class="p">],</span> 
                             <span class="s1">'Home Team'</span><span class="p">:</span> <span class="p">[</span><span class="n">homeTeam</span><span class="p">],</span> 
                             <span class="s1">'Away Team'</span><span class="p">:</span> <span class="p">[</span><span class="n">awayTeam</span><span class="p">],</span> 
                             <span class="s1">'Home Score'</span><span class="p">:[</span><span class="mi">0</span><span class="p">],</span> 
                             <span class="s1">'Away Score'</span><span class="p">:[</span><span class="mi">0</span><span class="p">]})</span>
        <span class="n">stats</span> <span class="o">=</span> <span class="n">processMatchData</span><span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">matches</span><span class="p">,</span> <span class="n">dummy</span><span class="p">]))</span>
          
        <span class="k">return</span> <span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">transformer</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="n">stats</span><span class="p">))[</span><span class="o">-</span><span class="mi">1</span><span class="p">,:]</span>

    <span class="k">def</span> <span class="nf">predict</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">date</span><span class="p">,</span> <span class="nb">round</span><span class="p">,</span> <span class="n">homeTeam</span><span class="p">,</span> <span class="n">awayTeam</span><span class="p">,</span> <span class="n">probs</span><span class="o">=</span><span class="kc">False</span><span class="p">):</span>
        <span class="n">stats</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">getTeamStats</span><span class="p">(</span><span class="n">date</span><span class="p">,</span> <span class="nb">round</span><span class="p">,</span> <span class="n">homeTeam</span><span class="p">,</span> <span class="n">awayTeam</span><span class="p">)</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="o">-</span><span class="mi">1</span><span class="p">)</span>
        <span class="k">if</span> <span class="n">probs</span><span class="p">:</span>
            <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">estimator</span><span class="o">.</span><span class="n">predict_proba</span><span class="p">(</span><span class="n">stats</span><span class="p">)</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">estimator</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">stats</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Let's do a full walkthrough.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [93]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">match_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'afl_matches.csv'</span><span class="p">,</span> <span class="n">parse_dates</span><span class="o">=</span><span class="p">[</span><span class="s1">'Date'</span><span class="p">]),</span> <span class="n">getAFLData</span><span class="p">(</span><span class="mi">2023</span><span class="p">,</span> <span class="mi">2023</span><span class="p">)])</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [94]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_stats</span> <span class="o">=</span> <span class="n">processMatchData</span><span class="p">(</span><span class="n">match_df</span><span class="p">)</span>
<span class="n">afl_prepared</span> <span class="o">=</span> <span class="n">afl_pipeline</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">afl_stats</span><span class="p">)</span>
<span class="n">labels</span> <span class="o">=</span> <span class="n">get_labels</span><span class="p">(</span><span class="n">afl_stats</span><span class="p">)</span>

<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="kn">import</span> <span class="n">LogisticRegression</span>
<span class="n">log_clf</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">max_iter</span><span class="o">=</span><span class="mi">500</span><span class="p">)</span>
<span class="n">log_clf</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">afl_prepared</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>

<span class="n">afl_predictor</span> <span class="o">=</span> <span class="n">AFLPredictor</span><span class="p">(</span><span class="n">afl_pipeline</span><span class="p">,</span> <span class="n">log_clf</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [95]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_predictor</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-22'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'Geelong'</span><span class="p">,</span> <span class="s1">'Essendon'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[95]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>array(['Home'], dtype=object)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [96]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">afl_predictor</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-22'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'Geelong'</span><span class="p">,</span> <span class="s1">'Essendon'</span><span class="p">,</span> <span class="n">probs</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[96]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>array([[0.33341533, 0.66658467]])</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>So our model is 67% sure that the home team (Geelong) will win.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [109]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">round14</span> <span class="o">=</span> <span class="p">[</span>
    <span class="p">[</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-15'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'Port Adelaide'</span><span class="p">,</span> <span class="s1">'Geelong'</span><span class="p">],</span>
    <span class="p">[</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-16'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'Brisbane Lions'</span><span class="p">,</span> <span class="s1">'Sydney'</span><span class="p">],</span>
    <span class="p">[</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-17'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'Greater Western Sydney'</span><span class="p">,</span> <span class="s1">'Fremantle'</span><span class="p">],</span>
    <span class="p">[</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-17'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'Richmond'</span><span class="p">,</span> <span class="s1">'St Kilda'</span><span class="p">],</span>
    <span class="p">[</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-18'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'Carlton'</span><span class="p">,</span> <span class="s1">'Gold Coast'</span><span class="p">],</span>
    <span class="p">[</span><span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">'2023-06-18'</span><span class="p">),</span> <span class="mi">14</span><span class="p">,</span> <span class="s1">'North Melbourne'</span><span class="p">,</span> <span class="s1">'Western Bulldogs'</span><span class="p">]</span>
<span class="p">]</span>
<span class="k">for</span> <span class="n">match</span> <span class="ow">in</span> <span class="n">round14</span><span class="p">:</span>
    <span class="n">prediction</span> <span class="o">=</span> <span class="n">afl_predictor</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">match</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">match</span><span class="p">[</span><span class="mi">1</span><span class="p">],</span> <span class="n">match</span><span class="p">[</span><span class="mi">2</span><span class="p">],</span> <span class="n">match</span><span class="p">[</span><span class="mi">3</span><span class="p">],</span> <span class="n">probs</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">match</span><span class="p">[</span><span class="mi">2</span><span class="p">]</span> <span class="o">+</span> <span class="s2">": </span><span class="si">{:.2f}</span><span class="s2">%"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">prediction</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span><span class="mi">1</span><span class="p">]</span><span class="o">*</span><span class="mi">100</span><span class="p">)</span> <span class="o">+</span> <span class="s2">", "</span> <span class="o">+</span> <span class="n">match</span><span class="p">[</span><span class="mi">3</span><span class="p">]</span> <span class="o">+</span> <span class="s2">": </span><span class="si">{:.2f}</span><span class="s2">%"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">prediction</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span><span class="mi">0</span><span class="p">]</span><span class="o">*</span><span class="mi">100</span><span class="p">))</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Port Adelaide: 44.89%, Geelong: 55.11%
Brisbane Lions: 35.42%, Sydney: 64.58%
Greater Western Sydney: 39.05%, Fremantle: 60.95%
Richmond: 46.85%, St Kilda: 53.15%
Carlton: 52.57%, Gold Coast: 47.43%
North Melbourne: 81.49%, Western Bulldogs: 18.51%
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [108]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">match</span> <span class="ow">in</span> <span class="n">round14</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">afl_predictor</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">match</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">match</span><span class="p">[</span><span class="mi">1</span><span class="p">],</span> <span class="n">match</span><span class="p">[</span><span class="mi">2</span><span class="p">],</span> <span class="n">match</span><span class="p">[</span><span class="mi">3</span><span class="p">]))</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>['Away']
['Away']
['Away']
['Away']
['Home']
['Home']
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Conclusion">Conclusion<a class="anchor-link" href="#Conclusion">¶</a></h2><p>The models that performed the best were logistic regression and a linear SVM, both achieving about 65% accuracy on the test set.</p>
<p>Of the four main models tested, neural networks performed the worst.
However, such models required a significant amount of tuning to perform well and the training dataset isn't particularly large.
It is possible that with proper tuning one could achieve better performance with deep learning.</p>
</div>
</div>
</div>
</div>
</main>
</body>
</html>
