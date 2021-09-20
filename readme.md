# Laravel Nova Field - Array Images with resize
A laravel nova field that will let you save your uploaded images path to your database in array format.

### This package is using this package to resize the images https://github.com/Intervention/image

# Installation
add package to your composer.json
```
"require": {
        ...
        "halimtuhu/array-images": "v1.2",
        ...
    },
```
and this repo as repository in same file
```
"repositories": [
        {
            "type": "path",
            "url": "./nova"
        },
        {
            "type": "vcs",
            "url": "https://github.com/hnassr/array-images"
        }
    ]
```

# Usage
Create array images just call `Halimtuhu\ArrayImages\ArrayImages` class and use `make` static method to create a field.
```
...
use Halimtuhu\ArrayImages\ArrayImages;
...
public function fields(Request $request)
    {
        return [
            ...
            ArrayImages::make('Images', 'images')->resize(800, null, true), // width, height, aspectRatio
            ...
        ];
    }
...
```
That will create a field with name `Images`. Stored data will look like this.
```
[{
    "url": "http://laranov.halimtuhu.test/storage/wB04AbprHGxHw4I3sizXmuw9L4LBcG0wv0QEacAo.jpeg",
    "name": "wB04AbprHGxHw4I3sizXmuw9L4LBcG0wv0QEacAo.jpeg"
}, {
    "url": "http://laranov.halimtuhu.test/storage/eOuxUCjHGNokkHdOXYB7gGObxCvf7m30ridFpBpy.jpeg",
    "name": "eOuxUCjHGNokkHdOXYB7gGObxCvf7m30ridFpBpy.jpeg"
}, {
    "url": "http://laranov.halimtuhu.test/storage/nLkZp4vfpATEp56NStJfeAtKoHvmN2hapfxoNrEN.jpeg",
    "name": "nLkZp4vfpATEp56NStJfeAtKoHvmN2hapfxoNrEN.jpeg"
}]
```

# Available Methods
### Disk
Specify disk target for uploaded images.
```
ArrayImages::make('Images', 'images')
    ->disk('public'),
```
If not specified then the default disk will be used.

### Path
Specify target path for uploaded images.
```
ArrayImages::make('Images', 'images)
    ->disk('public')
    ->path('images'),
```
If not specified then default path on selected disk will be used.


# Notes
- make sure you have specified correct `APP_URL` on your application
- make sure you have specified default `FILESYSTEM_DRIVER` on your application
