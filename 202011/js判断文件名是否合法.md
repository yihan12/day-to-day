文件类型可查询MIME参考手册.

### 获取文件后缀名

```javascript
/**
 * @description 获取文件后缀名
 * @param {String} fileName 文件全名，包含后缀名的那种
 */
export function getFileExt(fileName) {
    let splits = fileName.split('.');
    return _.last(splits);
}
```

### 检查文件类型

```javascript
/**
 * @description 检查文件类型，是否是合法的，这里的validMIMEList仅写了部分，如果需要支持更多，请查询MIME参考手册，增加更多的MIME类型进来
 * @param {Object} file 文件对象
 * @param {String} exts 文件合法类型，格式：doc|docx|png
 */
export function checkFileType(file, exts) {
    let validMIMEList = [
        // doc
        'application/msword',
        // xls
        'application/vnd.ms-excel',
        // docx
        'application/vnd.openxmlformats-officedocument.wordprocessingml.document',
        // xlsx
        'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
        // pdf
        'application/pdf',
        // rar
        'application/x-rar-compressed',
        // zip
        'application/zip'
    ];
    let validExts = exts.split('|');
    let fileExt = getFileExt(file.name);
    if (_.includes(validMIMEList, file.type) || _.includes(validExts, fileExt)) {
            return true;
    } else {
            return false;
    }
}
```
