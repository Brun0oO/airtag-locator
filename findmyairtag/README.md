# Install

## 1) Install Meltano [^1]:

- Install the pipx package manager:
```
   python3 -m pip install --user pipx
   python3 -m pipx ensurepath
```
- Install the meltano package:
```
   pipx install meltano
```
- Verify that meltano CLI is available:
```
   meltano --version
```

[^1]: [official guide](https://docs.meltano.com/guide/installation#local-installation)

## 2) Install prerequesites:

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

## 3) Configure:

The UI web port:

```
   meltano config meltano set ui bind_port 8080
```

The database:

- Install the postgresql environment: 
```
   brew install postgresql
```
- Start the psql CLI:
```
   psql postgress
```

- Then at the psql prompt, type:
```
   CREATE DATABASE warehouse;
   CREATE USER meltano WITH ENCRYPTED PASSWORD 'meltano';
   GRANT ALL PRIVILEGES ON DATABASE warehouse TO meltano;
   exit
```


## 4) Run:
```
   meltano ui
```

Now, enjoy, the Melatno UI is available at http://localhost:8080 :)


## 5) Complete the configuration

Before taking full advantage of this beautiful UI, you need to complete the configuration on this web side ;o)

* Complete the **tap-findmy** extractor configuration [^2]:

   * Click on the **Configure** button

   * Under **Item Name** edit box, type the name of the airtag you want to track

      You can verify with the **Test Connection** button.
   * Click on the **Save** button

[^2]: We assume the informations needed to the mac OS **FindMy / Locate** application has been already entered at the OS level (iCloud account).

* Configure the postgresql loader:

   * Click on the **Loaders** entry at the top window near the Meltano logo (or on the *hamburger* menu at the top right window corner if this entry is not visible)
   * Now, you see 2 installed loaders: the JSON one and the POSTGRESQL one, let's take a look at this latter first.
   * Click on the **Configure** button
   * You have to fill the empty required fields:
      * **Defaut Target Schema**: `$MELTANO_EXTRACT__LOAD_SCHEMA` *pay attention to the double underline characters*
      * **User**: `meltano`
      * **Password**: `meltano` *remember how we have created this postgresql user ;o)*
      * **Dbname**: `warehouse`
   * Click on the **Save** button

* Add a test pipeline:

   * Click on the **Pipelines** entry near the **Loaders** one (or on the *hamburger* menu if this entry is not visible)
   * As no pipeline has already been configured, click on the *"Create one now"* suggestion.
   * Select the `tap-findmy` extractor using the combo box located under **Step 1** label
   * Select the `PostgreSQL` loader using the combo box located under **Step 2** label
   * Keep `Skip` transform on the combo box located under **Step 3** label
   * Select `Once (Manual)` Interval using the combo box located under **Step 4** label
   * Change the name of this pipeline to `test` using the edit box located under **Step 5** label 
   * Click on the **Save** button

* Execute the test pipeline:

   * On the **Pipelines** dashboard, pipelines are displayed using a table, each row is a pipeline, take a look at the last (and unique) we juste created. Click on the **Run Now** button (located under the **Actions** column)
   * The run log is available by clicking in the cell contained in the **Last Run** column

* You can check how the table **item** in the **warehouse** database has been populated with your favorite postgreSQL viewer ([pgAdmin](https://www.pgadmin.org/) for example and have a look to this [link](https://www.bigbinary.com/blog/configure-postgresql-to-allow-remote-connection) if you want to configure a remote access to the database).




*to be continued !*