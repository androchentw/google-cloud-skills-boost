# GSP037: Detect Labels, Faces, and Landmarks in Images with the Cloud Vision API

* [GSP037: Detect Labels, Faces, and Landmarks in Images with the Cloud Vision API](https://www.cloudskillsboost.google/games/4713/labs/30673)
* Create a Cloud Vision API request and calling the API with curl
* Use the label, face, and landmark detection methods of the API

## Task 1. Create an API key

```sh
export API_KEY=<YOUR_API_KEY>
```

## Task 2. Upload an image to a Cloud Storage bucket

`<GCP_PROJECT>-bucket`: `qwiklabs-gcp-00-6fbdcb9cfe93-bucket`

Edit Object ACL

* Entity: Public
* Name: allUsers
* Access: Reader

## Task 3. Create your request

```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri": "gs://qwiklabs-gcp-00-6fbdcb9cfe93-bucket/donuts.png"
          }
        },
        "features": [
          {
            "type": "LABEL_DETECTION",
            "maxResults": 10
          }
        ]
      }
  ]
}
```

## Task 4. Label detection

```sh
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
```

### response

* `description` with the name of the item.
* `score`, a number from 0 - 1 indicating how confident it is that the description matches what's in the image.
* `mid` value that maps to the item's mid in Google's Knowledge Graph. You can use the mid when calling the Knowledge Graph API to get more information on the item.

```json
{
  "responses": [
    {
      "labelAnnotations": [
        {
          "mid": "/m/02wbm",
          "description": "Food",
          "score": 0.986098,
          "topicality": 0.986098
        },
        {
          "mid": "/m/01wydv",
          "description": "Beignet",
          "score": 0.9145899,
          "topicality": 0.9145899
        },
        {
          "mid": "/m/07xgrh",
          "description": "Ingredient",
          "score": 0.8922239,
          "topicality": 0.8922239
        },
        {
          "mid": "/m/01dk8s",
          "description": "Powdered sugar",
          "score": 0.855484,
          "topicality": 0.855484
        },
        {
          "mid": "/m/0p57p",
          "description": "Recipe",
          "score": 0.84780663,
          "topicality": 0.84780663
        },
        {
          "mid": "/m/01ykh",
          "description": "Cuisine",
          "score": 0.83784735,
          "topicality": 0.83784735
        },
        {
          "mid": "/m/06gd3r",
          "description": "Angel wings",
          "score": 0.8157256,
          "topicality": 0.8157256
        },
        {
          "mid": "/m/02q08p0",
          "description": "Dish",
          "score": 0.80321497,
          "topicality": 0.80321497
        },
        {
          "mid": "/m/052lwg6",
          "description": "Baked goods",
          "score": 0.79568243,
          "topicality": 0.79568243
        },
        {
          "mid": "/m/06x4c",
          "description": "Sugar",
          "score": 0.7846247,
          "topicality": 0.7846247
        }
      ]
    }
  ]
}
```

## Task 5. Web detection

* Edit request.json `requests.features.type`: `LABEL_DETECTION` => `WEB_DETECTION`

```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri": "gs://qwiklabs-gcp-00-6fbdcb9cfe93-bucket/donuts.png"
          }
        },
        "features": [
          {
            "type": "WEB_DETECTION",
            "maxResults": 10
          }
        ]
      }
  ]
}
```

```sh
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
```

### response

* check `webEntities`, `fullMatchingImages`, `partialMatchingImages`, `pagesWithMatchingImages`, `visuallySimilarImages`

```json
{
  "responses": [
    {
      "webDetection": {
        "webEntities": [
          {
            "entityId": "/m/01wydv",
            "score": 0.7406846,
            "description": "Beignet"
          },
          {
            "entityId": "/m/01dk8s",
            "score": 0.63719505,
            "description": "Icing Sugar"
          },
          {
            "entityId": "/m/02wvn_6",
            "score": 0.4973904,
            "description": "Ricciarelli"
          },
          {
            "entityId": "/m/0jy4k",
            "score": 0.4087,
            "description": "Doughnut"
          },
          {
            "entityId": "/g/11fmgrs4qm",
            "score": 0.3724,
            "description": "Vision AI"
          },
          {
            "entityId": "/m/0105pbj4",
            "score": 0.3506,
            "description": "Google Cloud Platform"
          },
          {
            "entityId": "/m/045c7b",
            "score": 0.3289,
            "description": "Google"
          },
          {
            "entityId": "/t/24bjj59_jbj9f",
            "score": 0.3289
          },
          {
            "entityId": "/m/02y_9m3",
            "score": 0.302,
            "description": "Cloud computing"
          },
          {
            "entityId": "/m/01mtb",
            "score": 0.3002,
            "description": "Cooking"
          }
        ],
        "fullMatchingImages": [
          {
            "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
          },
          {
            "url": "https://miro.medium.com/v2/resize:fit:1400/1*JSX2yNORAAOxdGoU17c4_A.png"
          }
        ],
        "pagesWithMatchingImages": [
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?locale=it&parent=catalog",
            "pageTitle": "Detect Labels, Faces, and Landmarks in Images with the Cloud ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          },
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?locale=de&parent=catalog",
            "pageTitle": "Detect Labels, Faces, and Landmarks in Images with the Cloud ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          },
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?locale=fr_CA&parent=catalog",
            "pageTitle": "Detect Labels, Faces, and Landmarks in Images with the Cloud ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          },
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?locale=uk&parent=catalog",
            "pageTitle": "Detect Labels, Faces, and Landmarks in Images with the Cloud ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          },
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?locale=pt_PT&parent=catalog",
            "pageTitle": "Detect Labels, Faces, and Landmarks in Images with the Cloud ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          },
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?locale=zh_TW&parent=catalog",
            "pageTitle": "Detect Labels, Faces, and Landmarks in Images with the Cloud ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          },
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?parent=catalog",
            "pageTitle": "Detect Labels, Faces, and Landmarks in Images with the Cloud ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          },
          {
            "url": "https://github.com/ratokeshi/Cloud-Shell-GSP037-Detect-Labels-Faces-and-Landmarks-in-Images-with-the-Cloud-Vision-API/blob/master/tutorial.md",
            "pageTitle": "GSP037 -- Tutorial: Detect Labels, Faces, and Landmarks in Images ...",
            "fullMatchingImages": [
              {
                "url": "https://camo.githubusercontent.com/de4a92596dd95e3a6e3486783113543c0b0ad077242450b605fdc8d5b3a5a4b4/68747470733a2f2f63646e2e7177696b6c6162732e636f6d2f5634506d455549377958644b7079744c4e5271775625324279474871796d2532426668646b745669386e6a34705073253344"
              }
            ]
          },
          {
            "url": "https://github.com/CCH0124/qwiklab/blob/master/Machine%20Learning%20APIs/2020-09-03-cloud-vision-api.md",
            "pageTitle": "2020-09-03-cloud-vision-api.md - GitHub",
            "fullMatchingImages": [
              {
                "url": "https://developers.google.com/codelabs/cloud-vision-intro/img/b05d9534e547f5ee.jpeg"
              }
            ]
          },
          {
            "url": "https://www.cloudskillsboost.google/focuses/1841?locale=es&parent=catalog",
            "pageTitle": "Detecte etiquetas, rostros y puntos de referencia en las imágenes ...",
            "fullMatchingImages": [
              {
                "url": "https://cdn.qwiklabs.com/V4PmEUI7yXdKpytLNRqwV%2ByGHqym%2BfhdktVi8nj4pPs%3D"
              }
            ]
          }
        ],
        "visuallySimilarImages": [
          {
            "url": "https://cdn.qwiklabs.com/w%2BfLMzkJxWN1WummHFhBLmkw5eFFSMFfQUiN6bwAwFA%3D"
          },
          {
            "url": "https://cdn.qwiklabs.com/vgWkDHchgJbOs4QsNHnrTHKs5%2Fo1rkQWFxMCLtHmrPo%3D"
          },
          {
            "url": "https://images.sbs.com.au/dims4/default/f352d99/2147483647/strip/true/crop/1200x675+0+113/resize/1280x720!/quality/90/?url=http%3A%2F%2Fsbs-au-brightspot.s3.amazonaws.com%2Fdrupal%2Ffood%2Fpublic%2Fgettyimages-638180210.jpg"
          },
          {
            "url": "https://www.catburglardoughco.co.uk/cdn/shop/files/C68A5692-5039-4486-BEA4-B64A758B558F.jpg?v=1699803372&width=533"
          },
          {
            "url": "https://img-aws.ehowcdn.com/700x/www.onlyinyourstate.com/wp-content/uploads/2023/03/21427379_1677301105647409_3898802876737590812_o.jpg"
          },
          {
            "url": "https://d1wa2w8kzcjjxv.cloudfront.net/2015/05/powdered-sugar.jpg"
          },
          {
            "url": "https://standardbakingco.com/wp-content/uploads/2023/09/cinnamon-walnut-rugelach-product.jpg"
          },
          {
            "url": "https://cf.bstatic.com/xdata/images/hotel/max1024x768/135380629.jpg?k=07558db0f6c134220f9c7924f88536f1d2d2e6b794286200167ab8ca381db24a&o=&hp=1"
          },
          {
            "url": "https://i.ytimg.com/vi/kCUwgLOAsd0/maxresdefault.jpg"
          }
        ],
        "bestGuessLabels": [
          {
            "label": "powdered sugar"
          }
        ]
      }
    }
  ]
}
```

## Task 6. Face detection

```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri": "gs://qwiklabs-gcp-00-6fbdcb9cfe93-bucket/selfie.png"
          }
        },
        "features": [
          {
            "type": "FACE_DETECTION"
          },
          {
            "type": "LANDMARK_DETECTION"
          }
        ]
      }
  ]
}
```

```sh
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
```

### response

* `boundingPoly` gives you the x,y coordinates around the face in the image.
* `fdBoundingPoly` is a smaller box than boundingPoly, focusing on the skin part of the face.
* `landmarks` is an array of objects for each facial feature, some you may not have even known about. This tells us the type of landmark, along with the 3D position of that feature (x,y,z coordinates) where the z coordinate is the depth. The remaining values give you more details on the face, including the likelihood of joy, sorrow, anger, and surprise.

```json
{
      "faceAnnotations": [
        {
          "boundingPoly": {
            "vertices": [
              {
                "x": 669,
                "y": 324
              },
              ...
            ]
          },
          "fdBoundingPoly": {
            ...
          },
          "landmarks": [
            {
              "type": "LEFT_EYE",
              "position": {
                "x": 692.05646,
                "y": 372.95868,
                "z": -0.00025268539
              }
            },
            ...
          ],
          "rollAngle": 0.21619819,
          "panAngle": -23.027969,
          "tiltAngle": -1.5531756,
          "detectionConfidence": 0.72354823,
          "landmarkingConfidence": 0.20047489,
          "joyLikelihood": "LIKELY",
          "sorrowLikelihood": "VERY_UNLIKELY",
          "angerLikelihood": "VERY_UNLIKELY",
          "surpriseLikelihood": "VERY_UNLIKELY",
          "underExposedLikelihood": "VERY_UNLIKELY",
          "blurredLikelihood": "VERY_UNLIKELY",
          "headwearLikelihood": "VERY_LIKELY"
        }
        ...
     }
}
```

## Task 7. Landmark annotation

```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri": "gs://qwiklabs-gcp-00-6fbdcb9cfe93-bucket/city.png"
          }
        },
        "features": [
          {
            "type": "LANDMARK_DETECTION",
            "maxResults": 10
          }
        ]
      }
  ]
}
```

```sh
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
```

### response

`landmarkAnnotations`

* the `mid` of the landmark
* it's name (`description`)
* a confidence `score`
* The `boundingPoly` shows the region in the image where the landmark was identified.
* The `locations` key tells us the latitude longitude coordinates of the picture.

```json
      "landmarkAnnotations": [
        {
          "mid": "/m/0hm_7",
          "description": "Red Square",
          "score": 0.8557956,
          "boundingPoly": {
            "vertices": [
              {},
              {
                "x": 503
              },
              {
                "x": 503,
                "y": 650
              },
              {
                "y": 650
              }
            ]
          },
          "locations": [
            {
              "latLng": {
                "latitude": 55.753930299999993,
                "longitude": 37.620794999999994
              }
...
```

## Task 8. Object localization

```json
{
  "requests": [
    {
      "image": {
        "source": {
          "imageUri": "https://cloud.google.com/vision/docs/images/bicycle_example.png"
        }
      },
      "features": [
        {
          "maxResults": 10,
          "type": "OBJECT_LOCALIZATION"
        }
      ]
    }
  ]
}
```

```sh
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
```

### Response

`localizedObjectAnnotations`

```json
{
  "responses": [
    {
      "localizedObjectAnnotations": [
        {
          "mid": "/m/01bqk0",
          "name": "Bicycle wheel",
          "score": 0.89648587,
          "boundingPoly": {
            "normalizedVertices": [
              {
                "x": 0.32076266,
                "y": 0.78941387
              },
              {
                "x": 0.43812272,
                "y": 0.78941387
              },
              {
                "x": 0.43812272,
                "y": 0.97331065
              },
              {
                "x": 0.32076266,
                "y": 0.97331065
              }
            ]
          }
        },
        {
          "mid": "/m/0199g",
          "name": "Bicycle",
          "score": 0.886761,
          "boundingPoly": {
            "normalizedVertices": [
              {
                "x": 0.312,
                "y": 0.6616471
              },
              {
                "x": 0.638353,
                "y": 0.6616471
              },
              {
                "x": 0.638353,
                "y": 0.9705882
              },
              {
                "x": 0.312,
                "y": 0.9705882
              }
            ]
          }
        },
...
```

### Task 9. Explore other Vision API methods

[Method: images.annotate documentation](https://cloud.google.com/vision/reference/rest/v1/images/annotate#Feature)

* **Logo detection**: Identify common logos and their location in an image.
* **Safe search detection**: Determine whether or not an image contains explicit content. This is useful for any application with user-generated content. You can filter images based on four factors: adult, medical, violent, and spoof content.
* **Text detection**: Run OCR to extract text from images. This method can even identify the language of text present in an image.
