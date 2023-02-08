# Dart SDK for openAI Apis (GPT-3 & DALL-E)

An open-source SDK that allows developers to easily integrate the power of OpenAI's state-of-the-art AI models into their Dart applications. This library provides simple and intuitive methods for making requests to OpenAI's various APIs, including the GPT-3 language model, DALL-E image generation, and more.

The package is designed to be lightweight and easy to use, so you can focus on building your application, rather than worrying about the complexities and error caused by dealing with HTTP requests.
</br>
</br>

<i>Unofficial</i>
</br>
<i>OpenAI does not have any official Dart library.</I>

#### Note:

Please note that this client SDK connects directly to openAI APIs using http requests, it doesn't provide any additional APIs than what exists [here](https://platform.openai.com/docs/introduction/overview).

## Code Progress

- [ ] ChatGPT ( as soon as possible when it's released )
- [x] [Authentication](#authentication)
- [x] [Models](#models)
- [x] [Completions](#completions)
  - [x] With `Stream` responses
- [x] [Edits](#edits)
- [x] [Images](#images)
- [x] [Embeddings](#embeddings)
- [x] [Files](#files)
- [x] [Fine-tunes](#fine-tunes)
  - [ ] With events `Stream` responses
- [x] [Moderation](#moderations)

## Testing Progress

- [x] [Authentication](#authentication)
- [x] [Models](#models)
- [x] [Completions](#completions)
- [x] [Edits](#edits)
- [x] [Images](#images)
- [x] [Embeddings](#embeddings)
- [x] [Files](#files)
- [x] [Fine-tunes](#fine-tunes)
- [x] [Moderation](#moderations)</br>

</br>

### Articles:

- [How to generate AI images using Dall-e inside a Flutter/Dart application.
  ](https://medium.com/@ffikhi.aanas/how-to-generate-ai-images-using-dall-e-inside-a-flutter-dart-application-fd66aa031b14)

# Full Documentation:

For the full documentation about all members this library offers, [check here](https://pub.dev/documentation/dart_openai/latest/).

# Authentication

## API key

We highly recommend loading your secret key at runtime from a `.env` file, you can use the [dotenv](https://pub.dev/packages/dotenv) package.

```dart
void main() {
 DotEnv env = DotEnv()..load([".env"]);
 OpenAI.apiKey = env['OPEN_AI_API_KEY'];
 // ..
}
```

## Setting an organization

```dart
 OpenAI.organization = "ORGANIZATION ID";
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/authentication)

</br>

# Models

## List Models

Lists the currently available models, and provides basic information about each one such as the owner and availability.

```dart
 final models = await OpenAI.instance.model.list();
 print(models.first.id);
```

## Retrieve model

Retrieves a model instance, providing basic information about the model such as the owner and permissioning.

```dart
 final model = await OpenAI.instance.model.retrieve("MODEL ID");
 print(model.id)
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/models)

</br>

# Completions

Creates

## Create completion

```dart
 OpenAICompletionModel completion = await OpenAI.instance.completion.create(
   model: "text-davinci-003",
   prompt: "Dart is a ",
   temperature: 0.8,
 );
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/completions)

</br>

# Edits

## Create edit

```dart
 OpenAIEditModel edit = await OpenAI.instance.edit.create(
   model: "text-davinci-edit-001",
   input: " Hi!, I am a bot!!!!,",
   instruction: "remove all ! the input ",
 );
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/edits)

</br>

# Images

## Create image

```dart
 OpenAIImageModel image = await OpenAI.instance.image.create(
   prompt: "A dog",
   n: 1,
 );
```

## Create image edit

```dart
 final result = await OpenAI.instance.image.edit(
   image: File(/* image file path*/),
   mask: File(/* mask file path*/),
   prompt: "change color to green",
   n: 1,
 );

```

## Create image variation

```dart
OpenAIImageVariationModel variation = await OpenAI.instance.image.variation(
 image: File(/*YOUR IMAGE FILE PATH*/),
);
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/images)

</br>

# Embeddings

## Create embeddings

```dart
OpenAIEmbeddingsModel embeddings = await OpenAI.instance.embedding.create(
  model: "text-embedding-ada-002",
  input: "This is a text input just to test",
);;
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/embeddings)

</br>

# Files

## List files

```dart
List<OpenAIFileModel> files = await OpenAI.instance.file.list();
```

## Upload file

```dart
OpenAIFileModel uploadedFile = await OpenAI.instance.file.upload(
 file: File("FILE PATH HERE"),
 purpose: "fine-tuning",
);
```

## Delete file

```dart
bool isFileDeleted = await OpenAI.instance.file.delete("FILE ID");
```

## Retrieve file

```dart
OpenAIFileModel file = await OpenAI.instance.file.retrieve("FILE ID");
```

## Retrieve file content

```dart
dynamic fileContent  = await OpenAI.instance.file.retrieveContent("FILE ID");
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/files)

</br>

# Fine Tunes

## Create fine-tune

```dart
OpenAIFineTuneModel fineTune = await OpenAI.instance.fineTune.create(
 trainingFile: "FILE ID",
);
```

## List fine-tunes

```dart
List<OpenAIFineTuneModel> fineTunes = await OpenAI.instance.fineTune.list();
```

## Retrieve fine-tune

```dart
OpenAIFineTuneModel fineTune = await OpenAI.instance.fineTune.retrieve("FINE TUNE ID");
```

## Cancel fine-tune

```dart
OpenAIFineTuneModel fineTune = await OpenAI.instance.fineTune.cancel("FINE TUNE ID");
```

## List fine-tune events

```dart
 List<OpenAIFineTuneEventModel> events = await OpenAI.instance.fineTune.listEvents("FINE TUNE ID");
```

## Delete fine-tune

```dart
 bool deleted = await OpenAI.instance.fineTune.delete("FINE TUNE ID");
```

[Learn More From Here.](https://platform.openai.com/docs/api-reference/fine-tunes)

</br>
 
# Moderations
## Create moderation
```dart
OpenAIModerationModel moderationResult = await OpenAI.instance.moderation.create(
  input: "I want to kill him",
);
```
[Learn More From Here.](https://platform.openai.com/docs/api-reference/moderations)

<br>

# Error Handling

Any time an error happens from the OpenAI API ends (As Example: when you try to create an image variation from a non-image file ), a `RequestFailedException` will be thrown automatically inside your Flutter / Dart app, you can use a `try-catch` to catch that error, and make an action based on it:

```dart
try {

// This will throw an error.
 final errorVariation = await OpenAI.instance.image.variation(
  image: File(/*PATH OF NON-IMAGE FILE*/),
 );
} on RequestFailedException catch(e) {
 print(e.message);
 print(e.statusCode)
}
```
