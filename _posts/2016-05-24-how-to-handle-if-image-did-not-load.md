---
layout: post
title: "TIL: How to handle if image didn’t load"
description: Sometimes you can have a problem with images, especially when urls for them is generated in the code.
summary: Sometimes you can have a problem with images, especially when urls for them is generated in the code.
tags: til javascript
date: 2016-05-24
---

Sometimes you can have a problem with images, especially when urls for them is
generated in the code. Like for Gravatar service. User has an email, but she
doesn’t use Gravatar service. You don’t want to make an additional call to
check if image is there or handle that on the server. You only want to make
one call and if the image doesn’t exist or it can’t be loaded, a placeholder
image should be displayed or the empty image should be hidden altogether.

Html tag `<img/>` has two event methods onLoad and onError, which could be used
for this case.

[JS Bin - example](https://jsbin.com/bopalu/edit?html,js,console)

```html
<img
  onerror="onError(event.currentTarget.currentSrc)"
  src="http://image.isnt.there/img.png"
/>

<img
  onload="onLoad(event.currentTarget.currentSrc)"
  src="https://en.gravatar.com/userimage/9268958/419f96d0498ad49530ad44c268085142.png"
/>
```

```javascript
function onLoad(src) {
  console.log("Image was loaded " + src);
}

function onError(src) {
  console.log("Image doesn't load " + src);
}
```

Yes, I know Gravatar provides default image if image for an email doesn’t exist.
But sometimes that isn’t enough.

[Gravatar - Image Requests](https://en.gravatar.com/site/implement/images/)
