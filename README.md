# convert-to-webp
Convert any image format to webp

```php
/* 
* Send images and return a zip with converted images in Webp.
* $images = ["image.jpg", "image.png", ...];
*/
function imagesToWebp(array $images, string $downloaded_zip_path) {
  $zip = tmpfile();
  $post = [];

  foreach($images as $index => $image) {
      $post["images[$index]"] =  curl_file_create($image);
  }

  $ch = curl_init('https://deermobile.com/api/v1/convert/webp');
  curl_setopt($ch, CURLOPT_POSTFIELDS, $post);
  curl_setopt($ch, CURLOPT_FILE, $zip);
  curl_exec($ch);
  curl_close($ch);

  return file_put_contents($downloaded_zip_path, $zip);
}
```
