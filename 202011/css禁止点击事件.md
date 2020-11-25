将禁用的按钮灰掉的效果

```javascript
.disabled {
    pointer-events: none;
    cursor: default;
    opacity: 0.6;
}
```

选中的按钮
```javascript
.disabled.is-active {
    pointer-events: auto;
    cursor: pointer;
    opacity: 1;
}
```
