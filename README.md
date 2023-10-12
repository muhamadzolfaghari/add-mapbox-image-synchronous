# add-mapbox-image-synchronous
Add Mapbox map by synchronous method

Adding images while using symbol layers to illustrate images as a marker image could face challenges specifically when adding images for various categories.
Adding images should be done before adding any layer, furthermore that stages are divided into "addImage" and "loadImage" and "loadImage" is non-block or is not immediately run after the previous code which takes time to fully load, which makes code readability reduced.

As mentioned, adding an image is used in two methods of the maboxgl.Map class.

Through the class Promise, there is a facility to run map.loadImage synchronously.


```js
async function addMapImage(
  imageName: string,
  imageUrl: string,
  map: mapboxgl.Map,
) {
  return await new Promise<void>((resolve, reject) => {
    map.loadImage(imageName, imageUrl, (error, result) => {
      if (error) {
        reject(error);
      }

      map.addImage(imageName, result as ImageBitmap);
      resolve();
    });
  });
}


function addMapFeatures(map: mapboxgl.Map) {
    for (const image of images) {
        await addMapImage(image.name, image.url, map)
    }

    for (const layer of layers) {
        map.addLayer(layer)
    }

    for (const sourceId in sources) {
        map.addSource(sourceId, sources[sourceId])
    }
}
```


#mapbox #image #map #map #typescirpt
