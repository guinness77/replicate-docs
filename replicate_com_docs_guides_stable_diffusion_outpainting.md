Docs

Search documentation`⌘K`

Get started

Collapse sidebar

[Run a model from Node.js](https://replicate.com/docs/get-started/nodejs) [Run a model from Google Colab](https://replicate.com/docs/get-started/google-colab) [Run a model from Python](https://replicate.com/docs/get-started/python) [Fine-tune an image model](https://replicate.com/docs/get-started/fine-tune-with-flux)

Guides

[Build a website with Next.js](https://replicate.com/docs/guides/nextjs) [Build a Discord bot with Python](https://replicate.com/docs/guides/discord-bot) [Build an app with SwiftUI](https://replicate.com/docs/guides/swiftui) [Cache images with Cloudflare](https://replicate.com/docs/guides/cloudflare-image-cache) [Use realtime speech with OpenAI](https://replicate.com/docs/guides/openai-realtime) [Push your own model](https://replicate.com/docs/guides/push-a-model) [Push a Diffusers model](https://replicate.com/docs/guides/push-a-diffusers-model) [Push a Transformers model](https://replicate.com/docs/guides/push-a-transformers-model) [Handle webhooks with Val Town](https://replicate.com/docs/guides/build-a-webhook-notifier-with-val-town) [Deploy a custom model](https://replicate.com/docs/guides/deploy-a-custom-model) [Push a model using GitHub Actions](https://replicate.com/docs/guides/push-a-model-using-github-actions) [Set up a CI/CD pipeline](https://replicate.com/docs/guides/continuous-model-deployment) [Get a GPU on Brev](https://replicate.com/docs/guides/get-a-gpu-on-brev) [Get a GPU on Lambda Labs](https://replicate.com/docs/guides/get-a-gpu-on-lambda-labs) [Working with LoRAs](https://replicate.com/docs/guides/working-with-loras)

ComfyUI

Hypermedia

Instant ID

Language models

Llava

Model best practices

Photomaker

Stable Diffusion

[Make art with Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion) [How to use Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/how-to-use) [Image to image (img2img) with Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/image-to-image) [Inpainting with Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/inpainting) [Outpainting with Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/outpainting) [Fine-tuning Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/fine-tuning) [Using ControlNet with Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/controlnet) [Fast Stable Diffusion: Turbo and latent consistency models (LCMs)](https://replicate.com/docs/guides/stable-diffusion/turbo-and-latent-consistency) [A to Z of Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/glossary)

Upscaling images

Whisper

Topics

Models

Predictions

Deployments

Webhooks

Organizations

Billing

Site policy

Reference

[How does Replicate work?](https://replicate.com/docs/reference/how-does-replicate-work) [Client libraries](https://replicate.com/docs/reference/client-libraries) [HTTP API](https://replicate.com/docs/reference/http) [OpenAPI schema](https://replicate.com/docs/reference/openapi) [Open source](https://replicate.com/docs/reference/open-source)

Outpainting is the process of using an image generation model like Stable Diffusion to extend beyond the canvas of an existing image. Outpainting is very similar to [inpainting](https://replicate.com/docs/guides/stable-diffusion/inpainting), but instead of generating a region _within_ an existing image, the model generates a region _outside_ of it.

Here's an example of an outpainted image:

| Input | Output |
| --- | --- |
| ![source image](https://replicate.com/frontend-assets/indigo-input-Bqw0dPC-.jpg) | ![output image](https://replicate.com/frontend-assets/indigo-output-B861-YY0.jpg) |

In this guide, we'll walk you through the process of creating your own outpainted images from scratch using Stable Diffusion SDXL.

## [Anchor for the-outpainting-process](https://replicate.com/docs/guides/stable-diffusion/outpainting\#the-outpainting-process) The outpainting process

At a high level, outpainting works like this:

1. Choose an existing image you'd like to outpaint.
2. Create a **source image** that places your original image within a larger canvas.
3. Create a black and white **mask image**.
4. Use your source image, your mask image, and a **text prompt** as inputs to Stable Diffusion to generate a new image.

An introduction to inpainting and outpainting with Stable Diffusion - YouTube

Replicate

3.28K subscribers

[An introduction to inpainting and outpainting with Stable Diffusion](https://www.youtube.com/watch?v=YWSBGP6FR-s)

Replicate

Search

Watch later

Share

Copy link

Info

Shopping

Tap to unmute

If playback doesn't begin shortly, try restarting your device.

More videos

## More videos

You're signed out

Videos you watch may be added to the TV's watch history and influence TV recommendations. To avoid this, cancel and sign in to YouTube on your computer.

CancelConfirm

Share

Include playlist

An error occurred while retrieving sharing information. Please try again later.

[Watch on](https://www.youtube.com/watch?v=YWSBGP6FR-s)

0:00

0:00 / 7:01•Live

•

[Watch on YouTube](https://www.youtube.com/watch?v=YWSBGP6FR-s "Watch on YouTube")

[🍿 Watch our inpainting and outpainting guide on YouTube](https://www.youtube.com/embed/YWSBGP6FR-s)

## [Anchor for step-1-find-an-existing-image](https://replicate.com/docs/guides/stable-diffusion/outpainting\#step-1-find-an-existing-image) Step 1: Find an existing image

The first step is to find an image you'd like to outpaint. This can be any image you want, like a photograph, a painting, or an image generated by an AI model like Stable Diffusion.

Here's an example of an image to outpaint, an AI-generated armchair in the shape of an avocado:

![source image](https://replicate.com/frontend-assets/avocado-armchair-original-DI9BstXE.jpg)

The image here has square dimensions, but your image can have any aspect ratio.

## [Anchor for step-2-create-a-source-image](https://replicate.com/docs/guides/stable-diffusion/outpainting\#step-2-create-a-source-image) Step 2: Create a source image

Once you've found an image you want to outpaint, you need to place it within a larger canvas so the image model will have space to paint around it. You can do this with traditional raster image editing software like Photoshop or GIMP, but since you won't actually be doing any manual bitmap-based editing of the image, you can also use web-based vector drawing tools like [Figma](https://www.figma.com/) or [Canva](https://www.canva.com/) to achieve the same result.

Create a new square image, and place your original image within it. 1024x1024 is ideal if you're using the [SDXL version of Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/outpainting#the-models), as you will in this guide. For more info about image sizing and dimensions, see the docs on [width and height](https://replicate.com/docs/guides/stable-diffusion/how-to-use#width-and-height).

In the example image below, there's a checkboard pattern to indicate the "transparent" parts of the canvas that will be outpainted, but the checkboard is not actually neccessary. You can choose any color you like for the surrounding canvas, but it's a good idea to choose a color that's similar to the color of the image you're outpainting. This will help the model generate a more seamless transition between the original image and the outpainted region.

It should look something like this:

![source image](https://replicate.com/frontend-assets/avocado-armchair-with-canvas-BAJaLMq5.jpg)

☝️ Here the original image is centered in the middle of the canvas, but you can place it anywhere you like depending on which part of the canvas you'd like to outpaint. These are also perfectly valid arrangements:

![source image](https://replicate.com/frontend-assets/avocado-armchair-alternate-canvases-VBRx2n8Q.jpg)

Save this image as a JPG or PNG file. Give it a name like `outpainting-source.jpg` or `outpainting-source.png` so you can easily identify it later.

## [Anchor for step-3-create-a-mask-image](https://replicate.com/docs/guides/stable-diffusion/outpainting\#step-3-create-a-mask-image) Step 3: Create a mask image

Next, you'll generate a mask image. This is a black and white image that tells the model which parts of the image to preserve, and which parts to generate new content for. Again you can use any image editing tool you like do to do this, as long as it can save JPG or PNG files.

Use the same dimensions for your mask image as you did for your source image: 1024x1024 square. The mask image should be black and white, with the black areas representing the parts of the image you want preserve, and the white areas representing the parts of the image you want to generate new content for.

If you can't easily remember which parts should be black and which should be white, try asking ChatGPT to [create a mnemonic for you](https://chat.openai.com/share/d49703ef-185b-4d17-91fb-34a2bbde8695). Here's one:

> Keep the Night, Replace the Light

For our centered avocado armchair, the mask image should look something like this:

![source image](<Base64-Image-Removed>)

☝️ **Important!** Be sure to draw your mask slightly smaller than the source image. This will help the model generate a more seamless visual transition between the original image and the outpainted region. It will also prevent an unwanted visible line from being drawn between the original image and the outpainted region.

Save this image as a JPG or PNG file. Give it a name like `outpainting-mask.jpg` or `outpainting-mask.png` so you can easily identify it later.

## [Anchor for step-4-generate-the-outpainted-image](https://replicate.com/docs/guides/stable-diffusion/outpainting\#step-4-generate-the-outpainted-image) Step 4: Generate the outpainted image

Now that you've generated your source image and mask image, you're ready to generate the outpainted image. There are many models that support outpainting, but in this guide you'll use the [SDXL version of Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/outpainting#the-models) to generate your outpainted image.

The inputs you'll provide to stable diffusion are:

- `prompt`: A short string of text describing the image you'd like to generate. To see what your avocado armchair would look like if it were in a larger room, use a prompt like "an armchair in a room full of plants".
- `image`: The source image you created in step 2.
- `mask`: The mask image you created in step 3.

### [Anchor for use-replicates-web-interface](https://replicate.com/docs/guides/stable-diffusion/outpainting\#use-replicates-web-interface) Use Replicate's web interface

To generate your outpainted image using Replicate's web interface, follow [this link](https://replicate.com/stability-ai/sdxl/versions/610dddf033f10431b1b55f24510b6009fcba23017ee551a1b9afbc4eec79e29c?prediction=faz67o3bvxmrr5ydw7yhustwfq), replacing the `image`, `mask`, and `prompt` inputs with your own values. The web UI makes it easy to drag and drop your image and mask files right into the browser window.

### [Anchor for use-replicates-api](https://replicate.com/docs/guides/stable-diffusion/outpainting\#use-replicates-api) Use Replicate's API

To generate your outpainted image using Replicate's API, you can use [whatever programming language you prefer](https://replicate.com/docs/reference/client-libraries), but in this guide we'll use Python.

Start by [setting up the Python client](https://replicate.com/docs/get-started/python), then run this code:

Copy

```
import replicate
output = replicate.run(
  "stability-ai/sdxl:39ed52f2a78e934b3ba6e2a89f5b1c712de7dfea535525255b1aa35c5565e08b",
  input={
    "prompt": "an armchair in a room full of plants",
    "image": open("path/to/outpainting-source.jpg", "rb"),
    "mask": open("path/to/outpainting-mask.jpg", "rb")
  }
)

# Save the outpainted image
with open('outpainted.png', 'wb') as f:
    f.write(output[0].read())
```

The resulting image should look something like this:

![source image](https://replicate.com/frontend-assets/avocado-armchair-outpainted-Yv6wIRJH.jpg)

Now that you've generated your first outpainted image, it's time to iterate. Refine the prompt, adjust the mask, and try again. This is where the API really shines, because you can easily write code to run the model multiple times with different inputs to see what works best.

Happy outpainting! 🥑

[Next:Fine-tuning Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/fine-tuning)