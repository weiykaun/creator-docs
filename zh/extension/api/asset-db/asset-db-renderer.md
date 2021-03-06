<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

# AssetDB

AssetDB singleton class in renderer process, you can access the instance with `Editor.assetdb`.

## remote

The remote AssetDB instance of main process, same as `Editor.remote.assetdb`.

## library

The library path.

# explore

Reveal given url in native file system.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

# exploreLib

Reveal given url's library file in native file system.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

# queryPathByUrl

Get native file path by url.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function.
    - `cb.path` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

# queryUuidByUrl

Get uuid by url.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function.
    - `cb.path` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

# queryPathByUuid

Get native file path by uuid.

**Parameters**

- `uuid` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function.
    - `cb.path` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

# queryUrlByUuid

Get asset url by uuid.

**Parameters**

- `uuid` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function.
    - `cb.url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 

# queryInfoByUuid

Get asset info by uuid.

**Parameters**

- `uuid` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function
    - `cb.info` **[object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** 

**Examples**

```js
Editor.assetdb.queryInfoByUuid(uuid, function (err, info) {
    // info.path
    // info.url
    // info.type
});
```

# queryMetaInfoByUuid

Get meta info by uuid.

**Parameters**

- `uuid` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function.
    - `cb.info` **[object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** 

**Examples**

```js
Editor.assetdb.queryMetaInfoByUuid(uuid, function (err, info) {
    // info.assetPath
    // info.metaPath
    // info.assetMtime
    // info.metaMtime
    // info.json
});
```

# deepQuery

Query all assets from asset-db.

**Parameters**

- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function
    - `cb.results` **[array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** 

**Examples**

```js
Editor.assetdb.deepQuery(function (err, results) {
    results.forEach(function (result) {
        // result.name
        // result.extname
        // result.uuid
        // result.type
        // result.children - the array of children result
    });
});
```

# queryAssets

Query assets by url pattern and asset-type.

**Parameters**

- `pattern` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The url pattern.
- `assetTypes` **([string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array))** The asset type(s).

    You can use the `Editor.assettype2name[cc.js.getClassName(asset)]` API to get the corresponding resource type. The `asset` in the API is the resource type you want to query, such as `cc.SpriteFrame`, `cc.Texture2D`.

- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callback function.
    - `cb.results` **[array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** 

**Examples**

```js
Editor.assetdb.queryAssets('db://assets/**\/*', 'texture', function (err, results) {
    results.forEach(function (result) {
        // result.url
        // result.path
        // result.uuid
        // result.type
    });
});
```

# import

Import files outside asset-db to specific url folder. The import result will be sent through ipc message `asset-db:assets-created`.

**Parameters**

- `rawfiles` **[array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** Rawfile path list.
- `destUrl` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The url of dest folder.
- `showProgress` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** Show progress or not.
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** The callbak function.

**Examples**

```js
Editor.assetdb.import([
    '/file/to/import/01.png',
    '/file/to/import/02.png',
    '/file/to/import/03.png',
], 'db://assets/foobar');
```

# create

Create asset in specific url by sending string data to it. The created result will be sent through by ipc message `asset-db:assets-created`.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `data` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** 

**Examples**

```js
Editor.assetdb.create('db://assets/foo/bar/foobar.js', 'var foobar = 0;');
```

# move

Move asset from src to dest. The moved result will be sent through by ipc message `asset-db:assets-moved`.

**Parameters**

- `srcUrl` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `destUrl` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `showMessageBox`  

**Examples**

```js
Editor.assetdb.move('db://assets/foo/bar/foobar.js', 'db://assets/foo/bar/foobar02.js');
```

# delete

Delete assets by url list. The deleted results will be sent through by ipc message `asset-db:assets-deleted`.

**Parameters**

- `urls` **[array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** 

**Examples**

```js
Editor.assetdb.delete([
    'db://assets/foo/bar/foobar.js',
    'db://assets/foo/bar/foobar02.js',
]);
```

# saveExists

Save specific asset by sending string data. The saved results will be sent through by ipc message `asset-db:asset-changed`.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `data` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** the callback function.

**Examples**

```js
Editor.assetdb.saveExists('db://assets/foo/bar/foobar.js', 'var foobar = 0;');
```

# createOrSave

Create or save assets by sending string data. If the url is already existed, it will be changed with new data. The behavior is same with method saveExists. Otherwise, a new asset will be created. The behavior is same with method create.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `data` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** the callback function.

**Examples**

```js
Editor.assetdb.createOrSave('db://assets/foo/bar/foobar.js', 'var foobar = 0;');
```

# saveMeta

Save specific meta by sending meta's json string. The saved results will be sent through by ipc message `asset-db:asset-changed`.

**Parameters**

- `uuid` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `metaJson` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** the callback function.

**Examples**

```js
Editor.assetdb.saveMeta(meta.uuid, JSON.stringify(meta, null, 2));
```

# refresh

Refresh the assets in url, and return the results.

**Parameters**

- `url` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** 
- `[cb]` **[function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** 

**Examples**

```js
Editor.assetdb.refresh('db://assets/foo/bar/', function (err, results) {
    // assets that imported during init
    results.forEach(function (result) {
        if (result.command === 'delete') {
            // result.uuid
            // result.url
            // result.path
            // result.type
        } else if (result.command === 'change' || result.command === 'create') {
            // result.uuid
            // result.parentUuid
            // result.url
            // result.path
            // result.type
        } else if (result.command === 'uuid-change') {
            // result.oldUuid
            // result.uuid
            // result.parentUuid
            // result.url
            // result.path
            // result.type
        }
    });
});
```

# Editor

# assetdb

The AssetDB instance
