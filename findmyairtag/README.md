# Install

1) Install Meltano [^1]:

- install the pipx package manager:
```
   python3 -m pip install --user pipx
   python3 -m pipx ensurepath
```
- install the meltano package:
```
   pipx install meltano
```
- verify that meltano CLI is available:
```
   meltano --version
```

[^1]: [official guide](https://docs.meltano.com/guide/installation#local-installation)

2) Install the *'findmyairtag'* project:
```
   cd findmyairtag
   meltano install
```

*to be continued !*