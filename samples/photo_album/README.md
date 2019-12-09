# Cloudinary Node Photo Album Projects #

## About ##

This is the Cloudinary sample "photo album" project
This is for testing purpose and for Developer Software Engineer assignment only.


## Assignment ##

### Exercise 1: ###

Install the Cloudinary sample 'photo album' project and see that it's working, in Java, PHP, or any other preferred development framework

- I will install this on Node.js

1. Clone from Github [Node.js SDK](https://github.com/cloudinary/cloudinary_npm).
2. Set up my own [Github repo](https://github.com/JackyLN/my_cloudinary_node).
3. Add in `.env` file with `CLOUDINARY_URL` from my Cloudinary Dashboard.
4. Run the `photo_album` sample project

```
cd samples/photo_album
npm install
node server
```

5. Add jQuery and blueimp

```
npm install jquery blueimp-file-upload
``` 

6. Access the site from http://localhost:9000/

### Exercise 2: ###

Modify the sample project's image upload form to: 
- Automatically limit image size to 500x500 pixels on upload. 
- Tag uploaded images (doesn't matter which tag).

1. Modify `/photo_album/controllers/photo_controller.js`
2. Update Upload function:

Add tag `modify_width_height_500` and set `width: 500, height: 500, crop: "limit"`

```
cloudinary.uploader.upload(imageFile,
    { tags: ['express_sample', 'modify_width_height_500'], width: 500, height: 500, crop: "limit"})
    .then(function (image) {
      console.log('** file uploaded to Cloudinary service');
      console.dir(image);
      photo.image = image;
      // Save photo with image metadata
      return photo.save();
    })
    .then(function () {
      console.log('** photo saved');
    })
    .finally(function () {
      res.render('photos/create_through_server', { photo: photo, upload: photo.image });
    });
}
```

3. Test image json returned:

```
{ public_id: 'djdgp7wbsstsq6teys28',
  version: 1575878358,
  signature: '6dda4118708ea62daf8d99482c630593be055478',
  width: 500,
  height: 500,
  format: 'jpg',
  resource_type: 'image',
  created_at: '2019-12-09T07:59:18Z',
  tags: [ 'express_sample', 'modify_width_height_500' ],
  bytes: 40974,
  type: 'upload',
  etag: 'c7b64832295f4a17b1b6dc92b751ca36',
  placeholder: false,
  url:
   'http://res.cloudinary.com/jackycloudinary/image/upload/v1575878358/djdgp7wbsstsq6teys28.jpg',
  secure_url:
   'https://res.cloudinary.com/jackycloudinary/image/upload/v1575878358/djdgp7wbsstsq6teys28.jpg',
  original_filename: '99813-14dvttx.86y7' }
  ```

### Exercise 3: ###

Modify the sample project's gallery to display 2 additional thumbnails per image: 
- One with the Cloudinary logo as an overlay (watermark). 
- Second with the image saturation increased to 50%.

1. Upload cloudinary logo image to my own asset (download from sample asset)

  The file is: https://res.cloudinary.com/jackycloudinary/image/upload/v1575885541/cloudinary_icon_vvz0jf.png

2. Modify `/photo_album/views/photos/index.ejs` 
3. Add two more type of transformation:

```
<% var transformations = [
  ...
  { crop : "scale", height : 150, width : 150 , transformation : {
    overlay: "cloudinary_icon_vvz0jf", gravity: "south_east", x: 5, y: 5, width: 200, opacity: 60, effect: "brightness:200"} },
  { crop : "scale", height : 150, width : 150 , effect: "saturation:50"}
] %>  
```

### Final ###

1. Tested.
2. Those jquery and blueimp-file-upload help to fix the issue on taking care of all different upload methods of the app, server side, signed direct/client-side uploads and unsigned direct/client-side uploads.