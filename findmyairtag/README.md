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

2) Install prerequesites:

First, openssl:
```
  brew install openssl
```
Important: at the end of this installation, the command gives some instructions to follow and execute in your shell. Be sure to respect them:
* Add the openssl to your PATH env variable.
* Set the LDFLAGS and CPPFLAGS env variables to the dedicated openssl folders.

For example, for my fish shell, it gives:
```
  fish_add_path /usr/local/opt/openssl@3/bin
  set -gx LDFLAGS "-L/usr/local/opt/openssl@3/lib"
  set -gx CPPFLAGS "-I/usr/local/opt/openssl@3/include"
```

Then, other packages:
```
  brew install postgresql
  pip3 install numpy
  pip3 install psycopg2
```

2) Install the *'findmyairtag'* project:
```
   cd findmyairtag
   meltano install
   meltano upgrade files
```

3) Configure:

The UI web port:

```
   meltano config meltano set ui bind_port 8080
```

The database:
```
   To be documented here!
```

4) Run:
```
   meltano ui
```

Now, enjoy, the Melatno UI is available at http://localhost:8080 :)

*to be continued !*