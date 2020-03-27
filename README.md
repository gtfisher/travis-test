# travis-test


run a chaos toolkit experiment on travis

use the following ```.travis.yaml```

```yaml
language: python

python:

  - "3.7"

install:
  - pip install -r requirements.txt

script:

  - chaos run experiment.json
```

This will run the Experiment.json in the local repo

Run with chaosiq

Getting a settings.yml with the required settings.

Encrypt this file as per
https://docs.travis-ci.com/user/encrypting-files/

encrypt file using

```travis encrypt-file settings.yaml --add --com```

Ensure settings.yaml is not pushed to repo

To run with ChaosIQ Plugin and an encrypted Settings.yaml
* add chaosiq-cloud to requirements.txt
* amend ```.travis.yaml``` to:

```yaml
language: python
python:
- '3.7'
install:
- pip install -r requirements.txt
script:
- chaos --settings settings.yaml run experiment.json
before_install:
- openssl aes-256-cbc -K $encrypted_fdb844fae20b_key -iv $encrypted_fdb844fae20b_iv
  -in settings.yaml.enc -out settings.yaml -d
```








