Docs

Search documentation`⌘K`

Get started

Collapse sidebar

[Run a model from Node.js](https://replicate.com/docs/get-started/nodejs) [Run a model from Google Colab](https://replicate.com/docs/get-started/google-colab) [Run a model from Python](https://replicate.com/docs/get-started/python) [Fine-tune an image model](https://replicate.com/docs/get-started/fine-tune-with-flux)

Guides

[Build a website with Next.js](https://replicate.com/docs/guides/nextjs) [Build a Discord bot with Python](https://replicate.com/docs/guides/discord-bot) [Build an app with SwiftUI](https://replicate.com/docs/guides/swiftui) [Cache images with Cloudflare](https://replicate.com/docs/guides/cloudflare-image-cache) [Use realtime speech with OpenAI](https://replicate.com/docs/guides/openai-realtime) [Push your own model](https://replicate.com/docs/guides/push-a-model) [Push a Diffusers model](https://replicate.com/docs/guides/push-a-diffusers-model) [Push a Transformers model](https://replicate.com/docs/guides/push-a-transformers-model) [Handle webhooks with Val Town](https://replicate.com/docs/guides/build-a-webhook-notifier-with-val-town) [Deploy a custom model](https://replicate.com/docs/guides/deploy-a-custom-model) [Push a model using GitHub Actions](https://replicate.com/docs/guides/push-a-model-using-github-actions) [Set up a CI/CD pipeline](https://replicate.com/docs/guides/continuous-model-deployment) [Get a GPU on Brev](https://replicate.com/docs/guides/get-a-gpu-on-brev) [Get a GPU on Lambda Labs](https://replicate.com/docs/guides/get-a-gpu-on-lambda-labs) [Working with LoRAs](https://replicate.com/docs/guides/working-with-loras)

ComfyUI

Hypermedia

[Build AI apps fast with hypermedia](https://replicate.com/docs/guides/hypermedia) [What is hypermedia, and why use it for AI apps?](https://replicate.com/docs/guides/hypermedia/what-is-hypermedia) [Building a face swapping app with Val Town, HTMX, and Replicate](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app)

Instant ID

Language models

Llava

Model best practices

Photomaker

Stable Diffusion

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

Warning

This guide is no longer supported, and includes references to deprecated models. Check out the [docs homepage](https://replicate.com/docs) for more up-to-date guides and examples.

Now that we've learned about the tools and concepts, let's build a hypermedia AI app. We'll use Val Town to create a serverless function, HTMX to add hypermedia controls to the page, and Replicate to call AI models.

### [Anchor for the-concept](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#the-concept) The concept

Face-swapping models are increasingly popular. And why not? It's fun to insert your face into a painting or movie screenshot. But wouldn't it be cool if you could do it with generated images, so you could star in any movie you can imagine?

Let's make a face swap app that lets you insert your face into a generated image. We'll use the popular [lucataco/faceswap](https://replicate.com/lucataco/faceswap) to switch the faces, and the photorealistic model [adirik/realvisxl-v3.0-turbo](https://replicate.com/adirik/realvisxl-v3.0-turbo) to generate the imaginary scenes.

### [Anchor for preparing-your-development-environment](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#preparing-your-development-environment) Preparing your development environment

This part is surprisingly easy. You don't need to install anything. You can follow along in the browser.

Sign up for a free account on [Val Town](https://val.town/). You'll also need an account on [Replicate](https://replicate.com/).

The only other preparation is to get a [Replicate API token](https://replicate.com/account/api-tokens) and set it as `REPLICATE_API_TOKEN` in your Val Town [Environment Variables](https://www.val.town/settings/environment-variables). This will let you call Replicate models from your val.

Watch out: this will also let anyone else call Replicate models from your val. Val Town protects the security of your environment variable, but it doesn't secure your HTTP endpoint or do any authentication. We won't do that for this demo app, but keep it in mind when building your own tool.

### [Anchor for start-with-a-val](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#start-with-a-val) Start with a val

Conveniently, Val Town has an HTMX template we can use:

deepfates/HTMX\_template \| Val Town

[![deepfates avatar](https://img.clerk.com/eyJ0eXBlIjoiZGVmYXVsdCIsImlpZCI6Imluc18yTm10cGhQUklwU0tqZHNiOHNnNGd2ZjJURFUiLCJyaWQiOiJ1c2VyXzJZMVVQeXNVejF3OEFlUmFsT0tQUDVsbmxxcCIsImluaXRpYWxzIjoiRCJ9)](https://www.val.town/u/deepfates "deepfates’s profile page")

deepfates

[HTMX\_template](https://www.val.town/v/deepfates/HTMX_template)

HTTP

999

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

/\\*\\* @jsxImportSource https://esm.sh/preact \*/

import{render}from"npm:preact-render-to-string";

exportdefaultasyncfunction(req:Request){

if(req.method==="POST"){

constname=(awaitreq.formData()).get("name");

returnnewResponse(render(<>Hello {name\|\|"World"}!</>));

}

returnnewResponse(

render(<html>

<head>

<title>Title</title>

<style>{"html { font-family: sans-serif; }"}</style>

<style>@import url('https://fonts.googleapis.com/css2?family=Inter&display=swap');</style><divclass="newsletter-form-container"><formclass="newsletter-form"action="https://app.loops.so/api/newsletter-form/clbv5du7z04g2ju08qcznl56v"method="POST"style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 100%;"><inputclass="newsletter-form-input"name="newsletter-form-input"type="email"placeholder="you@best-email.com"required=""style="font-family: Inter, sans-serif; color: rgb(0, 0, 0); font-size: 14px; margin: 0px 0px 10px; width: 100%; max-width: 300px; min-width: 100px; background: rgb(255, 255, 255); border: 1px solid rgb(209, 213, 219); box-sizing: border-box; box-shadow: rgba(0, 0, 0, 0.05) 0px 1px 2px; border-radius: 6px; padding: 8px 12px;"><buttontype="submit"class="newsletter-form-button"style="background: rgb(41, 176, 68); font-size: 14px; color: rgb(255, 255, 255); font-family: Inter, sans-serif; display: flex; width: 100%; max-width: 300px; white-space: normal; height: 38px; align-items: center; justify-content: center; flex-direction: row; padding: 9px 17px; box-shadow: rgba(0, 0, 0, 0.05) 0px 1px 2px; border-radius: 6px; text-align: center; font-style: normal; font-weight: 500; line-height: 20px; border: none; cursor: pointer;">Subscribe to Replicate Intelligence</button><buttontype="button"class="newsletter-loading-button"style="background: rgb(41, 176, 68); font-size: 14px; color: rgb(255, 255, 255); font-family: Inter, sans-serif; display: none; width: 100%; max-width: 300px; white-space: normal; height: 38px; align-items: center; justify-content: center; flex-direction: row; padding: 9px 17px; box-shadow: rgba(0, 0, 0, 0.05) 0px 1px 2px; border-radius: 6px; text-align: center; font-style: normal; font-weight: 500; line-height: 20px; border: none; cursor: pointer;">Please wait...</button></form><divclass="newsletter-success"style="display: none; align-items: center; justify-content: center; width: 100%;"><pclass="newsletter-success-message"style="font-family: Inter, sans-serif; color: rgb(0, 0, 0); font-size: 14px;">You're subscribed! 🚀</p></div><divclass="newsletter-error"style="display: none; align-items: center; justify-content: center; width: 100%;"><pclass="newsletter-error-message"style="font-family: Inter, sans-serif; color: rgb(185, 28, 28); font-size: 14px;">Oops! Something went wrong, please try again</p></div>

<scriptsrc="https://unpkg.com/htmx.org@1.9.9"></script>

<script>

function submitHandler(event) {

event.preventDefault();

var container = event.target.parentNode;

var form = container.querySelector(".newsletter-form");

var formInput = container.querySelector(".newsletter-form-input");

var success = container.querySelector(".newsletter-success");

var errorContainer = container.querySelector(".newsletter-error");

var errorMessage = container.querySelector(".newsletter-error-message");

var backButton = container.querySelector(".newsletter-back-button");

var submitButton = container.querySelector(".newsletter-form-button");

var loadingButton = container.querySelector(".newsletter-loading-button");

const rateLimit = () => {

errorContainer.style.display="flex";

errorMessage.innerText = "Too many signups, please try again in a little while";

submitButton.style.display = "none";

formInput.style.display = "none";

backButton.style.display = "block";

}

Preview

This is an embedded val, so you can run it here. It's just a hello world example right now, but it does have a live endpoint. You can click "Browser preview" in the bottom panel of the val (or "Open HTTP endpoint" in the top bar) and observe the dynamic behavior enabled by HTMX. Send a request, get a response and update a separate part of the DOM. All with just a 3kb library and two attributes:

Copy

```
hx-target="#answer" hx-post="/"
```

And all without a full page reload. It's... oddly refreshing.

#### [Anchor for understanding-htmx-attributes](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#understanding-htmx-attributes) Understanding HTMX attributes

HTMX adds a few attributes to HTML tags so you can add hypermedia controls to your page. The ones to know here are:

- **hx-get**: fetch a resource
- **hx-post**: send a request
- **hx-trigger**: specify the event that triggers a request
- **hx-swap**: define how to update the page after a request
- **hx-target**: specify the element to update after a request

You can read more about the attributes in the [HTMX documentation](https://htmx.org/reference/#attributes).

### [Anchor for integrate-replicate](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#integrate-replicate) Integrate Replicate

Before we wire up the hypermedia controls, let's add the Replicate client to our val to call the models. We'll use the `replicate` package from npm. This code will run on the Val Town platform, so we don't need to install anything locally.

We also add the function calls that we use to call the models, with parameters set for a nice image. First we send a text prompt to the image generation model, and then send the generated image to the face swap model, and finally return the result.

deepfates/hypermedia\_guide\_01 \| Val Town

[![deepfates avatar](https://img.clerk.com/eyJ0eXBlIjoiZGVmYXVsdCIsImlpZCI6Imluc18yTm10cGhQUklwU0tqZHNiOHNnNGd2ZjJURFUiLCJyaWQiOiJ1c2VyXzJZMVVQeXNVejF3OEFlUmFsT0tQUDVsbmxxcCIsImluaXRpYWxzIjoiRCJ9)](https://www.val.town/u/deepfates "deepfates’s profile page")

deepfates

[hypermedia\_guide\_01](https://www.val.town/v/deepfates/hypermedia_guide_01)

HTTP

99

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

/\\*\\* @jsxImportSource https://esm.sh/preact \*/

import{encode}from"https://deno.land/std@0.107.0/encoding/base64.ts";

import{render}from"npm:preact-render-to-string";

importReplicatefrom"npm:replicate";

constreplicate=newReplicate({

auth:Deno.env.get("REPLICATE\_DEMO\_API\_TOKEN"),

});

exportdefaultasyncfunction(req:Request){

if(req.method==="POST"){

constformData=awaitreq.formData();

constimage=formData.get("image");

consttextPrompt=formData.get("textPrompt");

// Run generative model

constgeneratedImage=awaitreplicate.run(

"adirik/realvisxl-v3.0-turbo:6e941e7fe46955afc031f35e84312a792d546b0f434f9008d457eb9deb24575c",

{

input:{

prompt:textPrompt+", cinematic movie still 35mm, film grain",

num\_inference\_steps:20,

guidance\_scale:5,

height:768,

width:1304,// this is 16x9

},

},

);

// Convert the source image to data URL

constsource=\`data:${image.type};base64,${encode(newUint8Array(awaitimage.arrayBuffer()))}\`;

// Run faceswap model

constoutput=awaitreplicate.run(

"lucataco/faceswap:9a4298548422074c3f57258c5d544497314ae4112df80d116f0d2109e843d20d",

{

input:{

Preview

Note that we encode the uploaded image into a [Data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs). This is so we can pass it from the client to the val without putting it on a server or in blob storage somewhere.

### [Anchor for building-the-ui](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#building-the-ui) Building the UI

Now we'll add the controls to the app: a form to upload a face image and a text input to prompt the model.

When you submit the form, it sends a POST request to the Val Town endpoint with the form data, which will call our Replicate models and get the generated image. Finally the val sends back a fragment of HTML with the generated image, and HTMX updates the DOM by putting the new fragment at the target.

deepfates/hypermedia\_guide\_02 \| Val Town

[![deepfates avatar](https://img.clerk.com/eyJ0eXBlIjoiZGVmYXVsdCIsImlpZCI6Imluc18yTm10cGhQUklwU0tqZHNiOHNnNGd2ZjJURFUiLCJyaWQiOiJ1c2VyXzJZMVVQeXNVejF3OEFlUmFsT0tQUDVsbmxxcCIsImluaXRpYWxzIjoiRCJ9)](https://www.val.town/u/deepfates "deepfates’s profile page")

deepfates

[hypermedia\_guide\_02](https://www.val.town/v/deepfates/hypermedia_guide_02)

HTTP

99

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

/\\*\\* @jsxImportSource https://esm.sh/preact \*/

import{encode}from"https://deno.land/std@0.107.0/encoding/base64.ts";

import{render}from"npm:preact-render-to-string";

importReplicatefrom"npm:replicate";

constreplicate=newReplicate({

auth:Deno.env.get("REPLICATE\_DEMO\_API\_TOKEN"),

});

exportdefaultasyncfunction(req:Request){

if(req.method==="POST"){

constformData=awaitreq.formData();

constimage=formData.get("image");

consttextPrompt=formData.get("textPrompt");

// Run generative model

constgeneratedImage=awaitreplicate.run(

"adirik/realvisxl-v3.0-turbo:6e941e7fe46955afc031f35e84312a792d546b0f434f9008d457eb9deb24575c",

{

input:{

prompt:textPrompt+", cinematic movie still 35mm, film grain",

num\_inference\_steps:20,

guidance\_scale:5,

height:768,

width:1304,// this is 16x9

},

},

);

// Convert the source image to data URL

constsource=\`data:${image.type};base64,${encode(newUint8Array(awaitimage.arrayBuffer()))}\`;

// Run faceswap model

constoutput=awaitreplicate.run(

"lucataco/faceswap:9a4298548422074c3f57258c5d544497314ae4112df80d116f0d2109e843d20d",

{

input:{

Preview

### [Anchor for add-styles](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#add-styles) Add styles

We have a working app! But it's not very pretty. We can make it look nicer by adding some CSS.

Let's use [terminal.css](https://terminalcss.xyz/) to give it a clean retro look. We could import this from npm through Val Town, but it's just a css file that creates utility classes, so to emphasize the power of hypermedia we'll just include it with a style tag like HTML of old.

Once we've added the style tag, we can include the classes in our HTML. Let's give it a fun name too.

deepfates/hypermedia\_guide\_03 \| Val Town

[![deepfates avatar](https://img.clerk.com/eyJ0eXBlIjoiZGVmYXVsdCIsImlpZCI6Imluc18yTm10cGhQUklwU0tqZHNiOHNnNGd2ZjJURFUiLCJyaWQiOiJ1c2VyXzJZMVVQeXNVejF3OEFlUmFsT0tQUDVsbmxxcCIsImluaXRpYWxzIjoiRCJ9)](https://www.val.town/u/deepfates "deepfates’s profile page")

deepfates

[hypermedia\_guide\_03](https://www.val.town/v/deepfates/hypermedia_guide_03)

HTTP

999

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

/\\*\\* @jsxImportSource https://esm.sh/preact \*/

import{encode}from"https://deno.land/std@0.107.0/encoding/base64.ts";

import{render}from"npm:preact-render-to-string";

importReplicatefrom"npm:replicate";

constreplicate=newReplicate({

auth:Deno.env.get("REPLICATE\_DEMO\_API\_TOKEN"),

});

exportdefaultasyncfunction(req:Request){

if(req.method==="POST"){

constformData=awaitreq.formData();

constimage=formData.get("image");

consttextPrompt=formData.get("textPrompt");

// Run generative model

constgeneratedImage=awaitreplicate.run(

"adirik/realvisxl-v3.0-turbo:6e941e7fe46955afc031f35e84312a792d546b0f434f9008d457eb9deb24575c",

{

input:{

prompt:textPrompt+", cinematic movie still 35mm, film grain",

num\_inference\_steps:20,

guidance\_scale:5,

height:768,

width:1304,// this is 16x9

},

},

);

// Convert the source image to data URL

constsource=\`data:${image.type};base64,${encode(newUint8Array(awaitimage.arrayBuffer()))}\`;

// Run faceswap model

constoutput=awaitreplicate.run(

"lucataco/faceswap:9a4298548422074c3f57258c5d544497314ae4112df80d116f0d2109e843d20d",

{

input:{

Preview

### [Anchor for add-a-loading-indicator](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#add-a-loading-indicator) Add a loading indicator

It would also be nice to load more than one image at once. Since we're using hypermedia as the engine of application state, we can do that by retargeting the new content. Using `hx-swap` we can target the element _before_ the most recent image, so they'll be stacked in reverse chronological order.

Finally let's also add a loading indicator so we know when the app is working. We'll add an attribute `hx-indicator` to the form, and HTMX will add a class `.htmx-request` to the element while the request is in progress. We can use a small piece of CSS to hide the indicator when not loading.

deepfates/hypermedia\_guide\_04 \| Val Town

[![deepfates avatar](https://img.clerk.com/eyJ0eXBlIjoiZGVmYXVsdCIsImlpZCI6Imluc18yTm10cGhQUklwU0tqZHNiOHNnNGd2ZjJURFUiLCJyaWQiOiJ1c2VyXzJZMVVQeXNVejF3OEFlUmFsT0tQUDVsbmxxcCIsImluaXRpYWxzIjoiRCJ9)](https://www.val.town/u/deepfates "deepfates’s profile page")

deepfates

[hypermedia\_guide\_04](https://www.val.town/v/deepfates/hypermedia_guide_04)

HTTP

999

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

/\\*\\* @jsxImportSource https://esm.sh/preact \*/

import{encode}from"https://deno.land/std@0.107.0/encoding/base64.ts";

import{render}from"npm:preact-render-to-string";

importReplicatefrom"npm:replicate";

constreplicate=newReplicate({

auth:Deno.env.get("REPLICATE\_DEMO\_API\_TOKEN"),

});

exportdefaultasyncfunction(req:Request){

if(req.method==="POST"){

constformData=awaitreq.formData();

constimage=formData.get("image");

consttextPrompt=formData.get("textPrompt");

// Run generative model

constgeneratedImage=awaitreplicate.run(

"adirik/realvisxl-v3.0-turbo:6e941e7fe46955afc031f35e84312a792d546b0f434f9008d457eb9deb24575c",

{

input:{

prompt:textPrompt+", cinematic movie still 35mm, film grain",

num\_inference\_steps:20,

guidance\_scale:5,

height:768,

width:1304,// this is 16x9

},

},

);

// Convert the source image to data URL

constsource=\`data:${image.type};base64,${encode(newUint8Array(awaitimage.arrayBuffer()))}\`;

// Run faceswap model

constoutput=awaitreplicate.run(

"lucataco/faceswap:9a4298548422074c3f57258c5d544497314ae4112df80d116f0d2109e843d20d",

{

input:{

Preview

## [Anchor for customizing-and-extending-your-app](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#customizing-and-extending-your-app) Customizing and Extending Your App

One of the best things about creating tools with Replicate is the ability to modify and customize them in real time to suit your needs.

### [Anchor for integrating-a-new-ai-model](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#integrating-a-new-ai-model) Integrating a New AI Model

For instance, if the images generated by the app aren't aesthetically pleasing, you don't have to keep tweaking the prompt each time. Instead, you can integrate a language model to engineer the prompt for you. A popular open-source choice with instruction following abilities is [mistralai/mistral-7b-instruct-v0.1](https://replicate.com/mistralai/mistral-7b-instruct-v0.1). This model can transform a simple prompt into a more complex one, resulting in a better image.

We can use a metaprompt like the following to transform our short text suggestions into evocative descriptions that the image generation model can use to create a more interesting image.

Copy

```
Take the description that follows and imagine it vividly as a movie scene, describing character, action, setting, composition, lighting, and mood. Write your answer in the form of a brief terse sentence. Include only the text of your answer, no other information or communication.
"""
${textPrompt}
"""
```

And then we just pass the prompt through the language model before sending it to the image generation model.

deepfates/hypermedia\_guide\_05 \| Val Town

[![deepfates avatar](https://img.clerk.com/eyJ0eXBlIjoiZGVmYXVsdCIsImlpZCI6Imluc18yTm10cGhQUklwU0tqZHNiOHNnNGd2ZjJURFUiLCJyaWQiOiJ1c2VyXzJZMVVQeXNVejF3OEFlUmFsT0tQUDVsbmxxcCIsImluaXRpYWxzIjoiRCJ9)](https://www.val.town/u/deepfates "deepfates’s profile page")

deepfates

[hypermedia\_guide\_05](https://www.val.town/v/deepfates/hypermedia_guide_05)

HTTP

999

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

/\\*\\* @jsxImportSource https://esm.sh/preact \*/

import{encode}from"https://deno.land/std@0.107.0/encoding/base64.ts";

import{render}from"npm:preact-render-to-string";

importReplicatefrom"npm:replicate";

constreplicate=newReplicate({

auth:Deno.env.get("REPLICATE\_API\_TOKEN"),

});

exportdefaultasyncfunction(req:Request){

if(req.method==="POST"){

constformData=awaitreq.formData();

constimage=formData.get("image");

consttextPrompt=formData.get("textPrompt");

constformattedPrompt=

\`Take the description that follows and imagine it vividly as a movie scene, describing character, action, setting, composition, lighting, and mood. Write your answer in the form of a brief terse sentence. Include only the text of your answer, no other information or communication.

"""

${textPrompt}

"""\`;

// Run text model

constinput={

prompt:formattedPrompt,

temperature:0.75,

max\_new\_tokens:500,

min\_new\_tokens:-1,

};

letstreamedText="";

forawait(consteventofreplicate.stream("mistralai/mixtral-8x7b-instruct-v0.1",{input})){

streamedText+=event.toString();

}

console.log(streamedText);

// Run generative model

Preview

### [Anchor for considering-real-world-factors](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#considering-real-world-factors) Considering Real-World Factors

While this might not be a full-fledged app, it's a great balance of simplicity and power for a personal tool. However, in a real-world scenario, you'd want to consider factors like authorization, error handling, security, scalability, performance, and cost. This doesn't mean you have to change approach -- [hypermedia can scale](https://htmx.org/essays/does-hypermedia-scale/).

### [Anchor for forking-the-app-and-further-customization](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#forking-the-app-and-further-customization) Forking the App and Further Customization

One of the key advantages of this paradigm is the ease of iteration and customization. You can fork and extend the API to suit your needs.

You can modify models, prompts, and behaviors with Replicate. The input and output from one stateless endpoint can be managed, and with the ability to have multiple vals, import them, and call their HTTP endpoints, you could even build an entire app with just vals.

The modular nature of the code means that if you need to scale up, you can easily move the code to a different platform. And since you're sending hypermedia, the app will continue to work even if the controls or the data change. The browser will be able to render it, and the user will be able to use it.

## [Anchor for wrapping-up](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#wrapping-up) Wrapping Up

We've journeyed together through the creation of a hypermedia AI app, getting our hands dirty with practical coding and gaining a solid understanding of the key tools and concepts involved. We've seen how these elements can come together to build something that's not just functional, but also fun and imaginative.

### [Anchor for what-lies-ahead](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app\#what-lies-ahead) What Lies Ahead

This guide is your starting point. Experiment with different models, tweak the code, and make it your own. The possibilities are endless, and the power to create is in your hands.