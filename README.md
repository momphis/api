# Introducing the [gifs.com](https://gifs.com) API [![](https://img.shields.io/badge/API-online-brightgreen.svg)](https://gifs.com)

<img align="right" src="https://storage.googleapis.com/cdn.gifs.com/genie-github-animation.gif?v=4">

*Everyone wishes for something...*
>"...I wish I could make gifs from vines or instagram videos."

>"...I wish I could convert my gifs to optimized HTML5 videos, .webm's, or .mp4s."

>"...I wish the transcoding was the fastest in the world."

*Your wishes have been granted.*

The [gifs.com](https://gifs.com) API makes it dead simple to convert and transcode a vast array of media into our HTML5 optimized gifs.com player, a compressed .gif, .webm and .mp4.

#### Can I see an example?

[Example request](http://api.gifs.com/media/import?source=https://zippy.gfycat.com/LimpingEveryHairstreak.webm&title=ClapClapClap) - try switching out the `source` with a vine link!

Send us any `.gif`, `.mp4`, `.webm`, `giphy`, `imgur`, `gfycat`, `streamable`, `instagram`, `twitter`, `facebook`, or `vine` links and we transcode your media lightning fast and serve it up in our awesome gifs player :zap:.

[Documentation](https://github.com/gifs/api/tree/master/DOCUMENTATION.md) |
[Examples](https://github.com/gifs/api/tree/master/examples) |
[Snippets](https://github.com/gifs/api/tree/master/SNIPPETS.md) |
[Get in Touch](mailto:rory@gifs.com) |
[FAQs](https://github.com/gifs/api#faqs) 


## Media Routes

The media routes allows anyone to add short media from various sources including external URLs and uploading from disk. There is a `150mb` size and `30s` time limit for all media being added.

### Import Endpoint `POST https://api.gifs.com/media/import`

We support importing the following file mime types: `image/gif`, `video/mp4`, `video/webm` and you can also link directly to a `giphy`, `imgur`, `gfycat`, `streamable`, `instagram`, `twitter`, `facebook`, or `vine` web page and we'll automagically find the best quality file to import.

Send a `POST` request with the following schema as `content-type: application/json`:

| Parameter       | Type         | Required?  | Description                          |
| -------------   |--------------|------------|--------------------------------------|
| source          | string       | required   | The source URL of the media to add   |
| title           | string       | optional   | The title of the media               |
| tags            | []string     | optional   | The tags relating the the media      |
| nsfw            | boolean      | optional   | If the media is not safe for work    |
| attribution     | object       | optional   | Any attribution you want displayed   |

Attribution object schema is:

| Parameter       | Type         | Required?  | Description                                 |
| -------------   |--------------|------------|---------------------------------------------|
| site            | string       | required   | twitter, reddit, instagram, or a custom URL |
| user            | string       | optional   | The username for social media sites         |
| url             | string       | optional   | The url if site != social media             |

#### Example Request

```HTTP
POST /media/import HTTP/1.1
Host: api.gifs.com
Token: beta-access-token-monty
Content-Type: application/json
Accept: application/json
Accept-Charset: utf-8
{
 "source": "http://i.imgur.com/WUYpq61.gif",
 "title": "Cat does a front flip",
 "tags": ["cat", "flipping", "cat flip", "amazing cats"],
 "attribution": {
   "site": "twitter",
   "user": "gifsCom"
 }
}
```

#### Example Response

```HTTP
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8
{
 "success":{
    "page": "https://gifs.com/gif/wpk4Lw",
    "files": {
        "gif": "https://j.gifs.com/wpk4Lw.gif",
        "jpg": "https://j.gifs.com/wpk4Lw.jpg",
        "mp4": "https://j.gifs.com/wpk4Lw.mp4",
        "webm": "https://j.gifs.com/wpk4Lw.webm"
    },
    "oembed": "https://gifs.com/oembed/wpk4Lw",
    "embed": "<iframe src='https://gifs.com/embed/wpk4Lw' frameborder='0' scrolling='no' width='309' height='291' style='-webkit-backface-visibility: hidden;-webkit-transform: scale(1);' ></iframe>",
    "meta": {
        "duration": "2.61s",
        "frames": "26",
        "height": "291",
        "width": "309"
    }
 }
}
```

### Upload Endpoint `POST https://api.gifs.com/media/upload`

You can upload `image/gif`, `video/mp4`, and `video/webm` media by sending a `POST` `multipart/form-data` request with the following form fields:

| Parameter         | Type      | Required?  | Description                                 |
| ------------------|-----------|------------|---------------------------------------------|
| file              | file      | required   | The file being uploaded                     |
| title             | string    | optional   | The title of the media                      |
| tags              | []string  | optional   | The tags relating the the media             |
| nsfw              | boolean   | optional   | If the media is not safe for work           |
| attribution_site  | string    | optional   | twitter, reddit, instagram, or a custom URL |
| attribution_user  | string    | optional   | The username for social media sites         |
| attribution_url   | string    | optional   | The url if site != social media             |

#### Example Request

```shell
curl \
  -F "file=@/media/gifs/awesome.gif" \
  -F "title=The most awesome gif eva" \
  -F "tags=awesome, cool, fun, gnarly" \
  https://api.gifs.com/media/upload
```

#### Example Response

```HTTP
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8
{
 "success":{
    "page": "https://gifs.com/gif/2k9BMv",
    "files": {
        "gif": "https://j.gifs.com/2k9BMv.gif",
        "jpg": "https://j.gifs.com/2k9BMv.jpg",
        "mp4": "https://j.gifs.com/2k9BMv.mp4",
        "webm": "https://j.gifs.com/2k9BMv.webm"
    },
    "oembed": "https://gifs.com/oembed/2k9BMv",
    "embed": "<iframe src='https://gifs.com/embed/2k9BMv' frameborder='0' scrolling='no' width='640' height='360' style='-webkit-backface-visibility: hidden;-webkit-transform: scale(1);' ></iframe>",
    "meta": {
        "duration": "4.104s",
        "frames": "123",
        "height": "360",
        "width": "640"
    }
 }
}
```
# FAQs

#### I just made something cool with the gifs API, can you feature it?

Feel free to send a pull request! If it's awesome, we'll merge it into our [examples](https://github.com/gifs/api/tree/master/examples).

#### What are you adding next?

The gifs API is the foundation for all gifs projects. Up next is:

Captioning and effects! :fire:

#### Can I help or contribute, or pretty please see a sneak peak?

Oh - yes! We'd love to get some feedback. Please feel free to [get in touch with us](mailto:rory@gifs.com).
