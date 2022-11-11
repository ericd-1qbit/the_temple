

## Our approach
### CIFAR 10

transforms.Compose(
            [
                transforms.Resize(image_size),
                transforms.RandomHorizontalFlip()
                if augment_horizontal_flip
                else nn.Identity(),
                transforms.CenterCrop(image_size),
                transforms.ToTensor(),
                transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5)),
            ]
        )

Resize to 32x32
// If size is an int, smaller edge of the image will be matched to this number.
Crops the given image at the center.
    If the image is torch Tensor, it is expected
    to have [..., H, W] shape, where ... means an arbitrary number of leading dimensions.
    If image size is smaller than output size along any edge, image is padded with 0 and then center cropped.

    Args:
        size (sequence or int): Desired output size of the crop. If size is an
            int instead of sequence like (h, w), a square crop (size, size) is
            made. If provided a sequence of length 1, it will be interpreted as (size[0], size[0]).

## Score-based repo
https://github.com/yang-song/score_sde_pytorch/blob/ef5cb679a4897a40d20e94d8d0e2124c3a48fb8c/datasets.py#L71


### CIFAR-10
def resize_op(img):
img = tf.image.convert_image_dtype(img, tf.float32)
return tf.image.resize(img, [config.data.image_size, config.data.image_size], antialias=True)


config.training.batch_size = 128
  data.dataset = 'CIFAR10'
  data.image_size = 32
  data.random_flip = True
  data.centered = False
  data.uniform_dequantization = False
  data.num_channels = 3


### CELEBA
https://drive.google.com/drive/folders/0B7EVK8r0v71pWEZsZE9oNnFzTm8?resourcekey=0-5BR16BdXnb8hVj6CNHKzLg

    def resize_op(img):
      img = tf.image.convert_image_dtype(img, tf.float32)
      img = central_crop(img, 140)
      
	      def central_crop(image, size):
			  """Crop the center of an image to the given size."""
			  top = (image.shape[0] - size) // 2
			  left = (image.shape[1] - size) // 2
			  return tf.image.crop_to_bounding_box(image, top, left, size, size)

      img = resize_small(img, config.data.image_size)
      return img


config.training.batch_size = 128
  data.dataset = 'CELEBA'
  data.image_size = 64
  data.random_flip = True
  data.uniform_dequantization = False
  data.centered = False
  data.num_channels = 3


### LSUN


    if config.data.image_size == 128:
      def resize_op(img):
        img = tf.image.convert_image_dtype(img, tf.float32)
        img = resize_small(img, config.data.image_size)
        img = central_crop(img, config.data.image_size)
        return img

    else:
      def resize_op(img):
        img = crop_resize(img, config.data.image_size)
        img = tf.image.convert_image_dtype(img, tf.float32)
        return img

config.training.batch_size = 64
  data.dataset = 'LSUN'
  data.image_size = 256
  data.random_flip = True
  data.uniform_dequantization = False
  data.centered = False
  data.num_channels = 3





```
def crop_resize(image, resolution):
  """Crop and resize an image to the given resolution."""
  crop = tf.minimum(tf.shape(image)[0], tf.shape(image)[1])
  h, w = tf.shape(image)[0], tf.shape(image)[1]
  image = image[(h - crop) // 2:(h + crop) // 2,
          (w - crop) // 2:(w + crop) // 2]
  image = tf.image.resize(
    image,
    size=(resolution, resolution),
    antialias=True,
    method=tf.image.ResizeMethod.BICUBIC)
  return tf.cast(image, tf.uint8)


def resize_small(image, resolution):
  """Shrink an image to the given resolution."""
  h, w = image.shape[0], image.shape[1]
  ratio = resolution / min(h, w)
  h = tf.round(h * ratio, tf.int32)
  w = tf.round(w * ratio, tf.int32)
  return tf.image.resize(image, [h, w], antialias=True)
```

