# Geepeetto

Geepeetto is a Python script that automates the process of localizing iOS apps. It uses OpenAI GPT-4 to generate translations of given strings into a list of languages, and then copies the localized strings into the appropriate .lproj folders of your Xcode project.

## Requirements

* Python 3.6 or higher
* OpenAI Python library (<https://github.com/openai/openai>)
* An OpenAI API Key

## Installation

1. Clone the repository:

```bash
git clone https://github.com/yourusername/geepeetto.git
```

2. Install the OpenAI Python library:

```bash
pip install openai
```

## Usage

```bash
python geepeetto.py input_file assets_folder [optional arguments]
```

The first time you run the script, **provide the OpenAI API key via the `--openai-key` argument**. This will be written on disk to `.key` and used in subsequent calls, so you only need to provide it once.

### Positional Arguments

* `input_file`: Path to the input file containing the strings to localize, in English (US).
* `assets_folder`: Path to the assets folder in the Xcode project.
  
### Optional Arguments

* `--openai-key`: API key for OpenAI. If not provided, the script will use the key you provided before.
* `--languages-file`: Path to the file containing the list of languages to translate to. Defaults to `./languages_list.txt`.
* `--extra-information`: Extra information to include in the instructions.
* `--template-file`: Path to the template file. Defaults to `./chatgpt_template.txt`.

## Input Files

### Input Strings File

The input_file should contain the strings to localize in English (US). Each string should be in the format:

```bash
"Key" = "Value";
```

Example:

```bash
"AccountView.SubscriptionSection.RedeemCode" = "Redeem code";
```

### Languages List File

The `languages_file` should be a plain text file containing one language per line, without empty lines. Each line should consist of the language name, followed by a space, a hyphen, another space, and the corresponding language code.

Example:

```bash
* French - fr
* Canadian French - fr-CA
* German - de
* Italian - it
* Malay - ms
* Brazilian Portuguese - pt-BR
* Portugal Portuguese - pt-PT
* Spanish - es
* Latin American Spanish - es-419
* Chinese (Simplified) - zh-Hans
```

Make sure to use the language code for each language the way that Apple expects them.

## Example

```bash
python geepeetto.py input_strings.txt MyProject/Assets --openai-key your_openai_api_key --languages-file languages_list.txt --extra-information "When translating, don't translate the words Superstar, Maccio, or Catapult since they are the App's main words."
```

After running the script, the generated translations will be written to translations.txt, and the localized strings will be copied to the appropriate .lproj folders in the specified Xcode project's assets folder.

## Authors

[@snowzurfer](https://github.com/snowzurfer) - Alberto Taiuti

## License

See LICENSE.
