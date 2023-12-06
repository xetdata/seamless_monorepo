## Seamless Communication Monorepo

[XetHub hosted](https://about.xethub.com/product/integrations/github) fork of Meta's Samless Communication models in a monorepo design:

- `models\` folder contains all of the model files themselves
- `code\` folder is a Git submodule to Meta's repo containing code and documentation

Large files like the model files are hosted by XetHub while source code is still hosted by GitHub using our [GitHub app](https://github.com/apps/xetdata).

### 🔂 Clone the entire Repo

This repo contains 41 GB of model files so double check your available storage on your target machine.

1. Install our tiny [git-xet](https://xethub.com/assets/docs/getting-started/install) extension for your operating system. This extension lets you pull and push large files in Xet managed GitHub repos. 
2. Then clone the repo locally:

```
git clone git@github.com:xetdata/seamless_monorepo.git
```

3. The download may take a while and you will see output from the git-xet client resembeling the following:

```
git-xet 0.12.5 filter started
Updating files: 100% (39/39), done.
Xet: Retrieving data blocks: 15.34 GiB / 110 MiB/s
Filtering content: 45% (11/24), 4.72 GiB / 70 MiB/s
```

_Bonus tip_: save your SSH passphrase [in your keychain](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases#saving-your-passphrase-in-the-keychain) so you don't have to enter it 4 times every time you git clone or git push.

### 🛋️ Quickly lazy clone just the code

If you have limited storage space or don't want to wait for the full download of all the model files, you can use the [lazy clone feature](https://xethub.com/assets/docs/large-repos/lazy-clone) baked into our [git-xet extension](https://xethub.com/assets/docs/getting-started/install):

```
git xet clone --lazy git@github.com:xetdata/seamless_monorepo.git
```

This command downloads all files managed by GitHub directly (like source code and markdown files) and only downloads pointers to larger binary files managed by XetHub.

Use the following command to materialize specific files:

```
git xet materialize models/seamless-streaming/seamless_streaming_unity.pt
```

View a full list of currently materialized files using:

```
git xet lazy show
```

### 🗻Mount the entire repo locally

You can also mount the entire model repo in just a few seconds. The files you need are fetched behind the scenes as you need them.

```
git xet mount git@github.com:xetdata/seamless_monorepo.git
```

### 🌃 Join our community

Join our [Slack community here](https://communityinviter.com/apps/xetdata/xet).

### 📝 Legal Disclosures

**Seamless Expressive models**

Meta requires that you register your email with them to use the Samless Expressive models. You can fill out [the form here](https://ai.meta.com/resources/models-and-libraries/seamless-downloads/).

**Licenses**

Meta's Seamless models have multiple licenses that you need to comply with.

The following non-generative components are MIT licensed as found in [MIT_LICENSE](MIT_LICENSE):
- Code
- Text only part of the mExpresso dataset found in the [SeamlessExpressive README](docs/expressive/README.md).
- UnitY2 forced alignment extractor found in the [UnitY2 Aligner README](docs/m4t/unity2_aligner_README.md).
- Speech toxicity tool with the etox dataset found in the [Toxicity README](src/seamless_communication/cli/toxicity).

The following models are CC-BY-NC 4.0 licensed as found in the [LICENSE](LICENSE):
- SeamlessM4T models (v1 and v2).
- SeamlessStreaming models.

The following models are Seamless licensed as found in [SEAMLESS_LICENSE](SEAMLESS_LICENSE):
- Seamless models.
- SeamlessExpressive models.