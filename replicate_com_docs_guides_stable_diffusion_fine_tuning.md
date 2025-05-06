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

You can fine-tune Stable Diffusion on your own images to create a new version of the model that is better at generating images of a person, object, or style.

For example, we’ve fine-tuned SDXL on:

- [Apple Emojis](https://replicate.com/fofr/sdxl-emoji)
- [the Barbie movie](https://replicate.com/fofr/sdxl-barbie)
- [Tron: Legacy](https://replicate.com/fofr/sdxl-tron)
- [Apple Vision Pro](https://replicate.com/fofr/sdxl-vision-pro)

## [Anchor for types-of-fine-tune](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#types-of-fine-tune) Types of fine-tune

There are multiple ways to fine-tune Stable Diffusion, such as:

- Dreambooth
- LoRAs (Low-Rank Adaptation)
- Textual inversion

Each of these techniques need just a few images of the subject or style you are training. You can use the same images for all of these techniques. 5 to 10 images is usually enough.

### [Anchor for dreambooth](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#dreambooth) Dreambooth

Dreambooth is a full model fine-tune that produces checkpoints that can be used as independent models. These checkpoints are typically 2GB or larger.

Read our blog post for a guide on [using Replicate for training Stable Diffusion with Dreambooth](https://replicate.com/blog/dreambooth-api).

Google Research [announced Dreambooth in August 2022](https://dreambooth.github.io/) ( [read the paper](https://arxiv.org/pdf/2208.12242.pdf)).

### [Anchor for loras-low-rank-adaptation](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#loras-low-rank-adaptation) LoRAs (Low-Rank Adaptation)

LoRAs are faster to tune and more lightweight than Dreambooth. As small as 1-6MB, they are easy to share and download.

LoRAs are a general technique that accelerate the fine-tuning of models by training smaller matrices. These then get loaded into an unchanged base model to apply their affect. In [February 2023 Simo Ryu published](https://github.com/cloneofsimo/lora) a way to fine-tune diffusion models like Stable Diffusion using LoRAs.

You can also use a `lora_scale` to change the strength of a LoRA.

### [Anchor for textual-inversion](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#textual-inversion) Textual inversion

Textual inversion does not modify any model weights. Instead it focuses on the text embedding space. It trains a new token concept (using a given word) that can be used with existing Stable Diffusion weights ( [read the paper](https://arxiv.org/pdf/2208.01618.pdf)).

## [Anchor for fine-tuning-sdxl-using-replicate](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#fine-tuning-sdxl-using-replicate) Fine-tuning SDXL using Replicate

You can fine-tune SDXL using Replicate – these fine-tunes combine LoRAs and textual inversion to create high quality results.

There are two ways to fine-tune SDXL on Replicate:

1. Use the [Replicate website](https://replicate.com/stability-ai/sdxl/train) to start a training, you can change the most important training parameters
2. Use the [Replicate API](https://replicate.com/blog/fine-tune-sdxl) to train with the full range of training parameters

Whichever approach you choose, you’ll need to prepare your training data.

### [Anchor for prepare-your-training-images](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#prepare-your-training-images) Prepare your training images

When running a training you need to provide a zip file containing your training images. Keep the following guidelines in mind when preparing your training images.

Images should contain only the subject itself, without background noise or other objects. They need to be in JPEG or PNG format. Dimensions, file size and filenames don't matter.

You can use as few as 5 images, but 10-20 images is better. The more images you use, the better the fine-tune will be. Small images will be automatically upscaled. All images will be cropped to square during the training process.

Put your images in a folder and zip it up. The directory structure of the zip file doesn't matter:

Copy

```
zip -r data.zip data
```

### [Anchor for watch-the-api-fine-tuning-guide-on-youtube](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#watch-the-api-fine-tuning-guide-on-youtube) Watch the API fine-tuning guide on YouTube

Fine-tune SDXL with Replicate - YouTube

fofrai

2.96K subscribers

[Fine-tune SDXL with Replicate](https://www.youtube.com/watch?v=xsa-_ZE9S7I)

fofrai

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

[Watch on](https://www.youtube.com/watch?v=xsa-_ZE9S7I)

0:00

0:00 / 25:44•Live

•

[Watch on YouTube](https://www.youtube.com/watch?v=xsa-_ZE9S7I "Watch on YouTube")

[🍿 Watch the fine-tuning guide on YouTube](https://www.youtube.com/watch?v=xsa-_ZE9S7I)

### [Anchor for use-the-replicate-cli-to-start-a-training](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#use-the-replicate-cli-to-start-a-training) Use the Replicate CLI to start a training

This guide uses the Replicate CLI to start the training, but if you want to use something else you can use [a client library](https://replicate.com/docs/reference/client-libraries) or [call the HTTP API directly](https://replicate.com/docs/reference/http#trainings.create).

Let’s start by installing the [Replicate CLI](https://github.com/replicate/cli):

Copy

```
brew tap replicate/tap
brew install replicate
```

Grab your API token from replicate.com/account and set the REPLICATE\_API\_TOKEN environment variable.

Copy

```
export REPLICATE_API_TOKEN=...
```

You need to create a model on Replicate – it will be the destination for your trained SDXL version:

Copy

```
# You can also go to https://replicate.com/create
replicate model create yourname/model --hardware gpu-a40-small
```

Now you can start your training:

Copy

```
replicate train stability-ai/sdxl \
 --destination yourname/model \
 --web \
 input_images=@data.zip
```

The `input_images` parameter is required. You can pass in a URL to your uploaded zip file, or use the `@` prefix to upload one from your local filesystem.

See the [training inputs on the SDXL model](https://replicate.com/stability-ai/sdxl/train) for a full list of training options.

Visit [replicate.com/trainings](https://replicate.com/trainings) to follow the progress of your training job.

### [Anchor for run-the-model](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#run-the-model) Run the model

When the model has finished training you can run it using replicate.com/my-name/my-model, or via the API:

Copy

```
output = replicate.run(
    "my-name/my-model:abcde1234...",
    input={"prompt": "a photo of TOK riding a rainbow unicorn"},
)

# Save the generated image
with open('output.png', 'wb') as f:
    f.write(output[0].read())
```

The trained concept is named `TOK` by default, but you can change that by setting `token_string` and `caption_prefix` inputs during the training process.

### [Anchor for how-we-prepare-data-for-training](https://replicate.com/docs/guides/stable-diffusion/fine-tuning\#how-we-prepare-data-for-training) How we prepare data for training

Before fine-tuning starts, the input images are preprocessed using multiple models:

- [SwinIR](https://replicate.com/jingyunliang/swinir) upscales the input images to a higher resolution.
- [BLIP](https://replicate.com/salesforce/blip) generates text captions for each input image.
- [CLIPSeg](https://github.com/timojl/clipseg) removes regions of the images that are not interesting or helpful for training.

For most users, the captions that BLIP generates for training work well. However, you can provide your own captions by adding a `caption.csv` file to your zip file of input images. Each image needs a caption. [Here's an example csv](https://github.com/replicate/cog-sdxl/blob/main/example_datasets/monster/caption.csv).

[Next:Using ControlNet with Stable Diffusion](https://replicate.com/docs/guides/stable-diffusion/controlnet)